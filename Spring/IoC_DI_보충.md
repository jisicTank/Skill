# Spring IoC, DI 보충



Spring Framework를 활용해 경험했던, eody 프로젝트를 가지고 실습해보며 IoC와 Di의 개념을 다시 학습한다.

<br><br>

## Inversion of Control

> 제어권이 뒤바꼈다고...?

일반적인(의존성에 대한) 제어권 : "내가 사용할 의존성은 내가 만든다."

```java
class OwnerController{
  private OwnerRepository repo = new OwnerRepository();
}
```



> 자기가 사용할 의존성은 자기가 만들어 사용하는 것이 일반적인데, 만약 이 클래스가 아닌 다른 곳에서 받아 사용한다면..?(ex. 생성자, setter, IoC 컨테이너....)
>
> -> 의존성이 역전됐다!!



IoC: " 내가 사용할 의존성을 누군가 알아서 주겠지..."(IoC)

* 내가 쓸 놈의 타입만 맞으면 어떤거든 상관없지 뭐..
* 그래야 내 코드 테스트 하기도 편하지.

<br><br>

## IoC

SampleController

```java
public class SampleController {

	SampleRepository sampleRepository;

	public SampleController(SampleRepository sampleRepository) {
		this.sampleRepository = sampleRepository;
	}
	
	public void doSomething() {
		sampleRepository.save();
	}
	
	
}
```

<br>

SampleRepository

```java
public class SampleRepository {

	public void save() {
		
	}
}

```

<br>

SampleControllerTest(JUnit Test Class)

```java
import static org.junit.Assert.*;

import org.junit.Test;

public class SampleControllerTest {

	@Test
	public void testDoSomething() {
		SampleRepository sampleRepository = new SampleRepository();
		SampleController sampleController = new SampleController(sampleRepository);
		
		sampleController.doSomething();
	}
}
```

<br>

<br>

Sample Controller는 Sample Repository 객체의 인스턴스를 사용하는 클래스다. 그런데 자기가 직접 인스턴스를 생성하지 않고, 생성자를 통해 받아 사용하고 있다. 하나뿐인 생성자가 인자로 SampleRepository를 갖고 있는 형태이므로 SampleContoller를 생성하려면 반드시 SampleRepository를 먼저 생성하고 인자로 넣어 만들어줘야 한다.

현재 코드에서는 SampleControllerTest에서 SampleRepository를 먼저 생성해서 주입해주고 있다. 

이처럼 Dependency Injection이란 말 그대로 의존성을 외부에서 만들어 넣어주는 행위이며 **<u>반드시 항상 해야 하는 것은 아니다</u>**. 필요한 상황에 따라 사용할 수 있는 것이고, 이는 **<u>개발자가 직접 해줄 수도 있지만 Spring Framework가 대신 해주기도 한다.</u>**

<br>

*** jUnit Test Class 생성하기

* Project 우클릭 - Properties - Java Build Path - Libraries 에서 Add Library - JUnit Import
* 원하는 경로에서 JUnit Test Case 생성

<br>

> 개발자가 직접 만들어서 DI를 할 수 있지만, 스프링 프레임워크가 제공하는 풍부한 DI 관련 기능과, 컨테이너의 라이프 사이클 인터페이스를 통한 기능 확장이 가능하기 때문에 Spring Framework의 DI를 많이들 사용한다...

<br><br>

## IoC 컨테이너

### ApplicationContext(BeanFactory)

> ApplicationContext나 BeanFactory는 가장 핵심적인 클래스들이지만, **<u>아이러니하게 실제 코드에서 구현해 사용할 일은 거의 없다.</u>** IoC 컨테이너는 ApplicationContext나 BeanFactory중 하나를 사용하게 될 것인데, 여기서는 ApplicationContext를 주로 사용한다.  BeanFactory가 사실상 IoC컨테이너이고, ApplicationContext Interface가 BeanFactory를 상속받고 있기 때문에 사실상 같다고 볼 수 있다. ApplicationContext는 이외에도 다양한 인터페이스를 상속받고 있어서 더 많은 기능을 갖고 있다.

<br>

#### IoC 컨테이너의 대략적인 역할

* 빈(Bean)을 만들고, Bean들 사이의 의존성을 엮어주고, 만든 Bean을 제공해준다.

<br>

#### Bean 설정

* 이름 또는 ID
* 타입
* 스코프

<br>

#### 특징

* IoC컨테이너는 Bean 끼리만 서로 의존성을 주입해 줄 수 있다.
* 기본적으로 Singletone Scope로 객체를 생성해 관리한다.

<br><br>

### Eody 프로젝트 코드로 IoC, DI, IoC 컨테이너 살펴보기

<br>

Searcher Contoller

```java
@Controller
public class SearcherController {

       @Resource(name = "sbiz")
        Biz<String, Integer, SearcherVO> biz;
        
        @Resource(name = "shopbiz")
        Biz<String, Integer, ShopVO> shbiz;
        
        @Resource(name = "bookingbiz")
        Biz<String, Integer, BookingVO> bbiz;
        
        @Resource(name = "hbiz")
        Biz<String, Integer, HotPlaceVO> hotbiz;
        
        @Resource(name = "rbiz")
        Biz<String, Integer, ReviewVO> reviewbiz;
        

        // 메인 접속
        @RequestMapping("/main.mc")
        public ModelAndView main() {
                ModelAndView mv = new ModelAndView();
                ArrayList<ShopVO> list = null;
                try {
                    list = shbiz.get();                      
                } catch (Exception e) {                	
                    e.printStackTrace();
                }        
                mv.addObject("shoplist", list);                
                mv.setViewName("searcher/main");  
                return mv;
        }
.
.
.(후략)
```

<br>

> SearcherController는 여러 biz 객체 의존성을 갖고 있고, 이를 활용해 여러 기능을 제공하는데 **<u>biz 인스턴스들을 생성하는 부분이 없다!</u>**

<br>

SearcherBiz

```java
@Service("sbiz")
public class SearcherBiz implements Biz<String, Integer, SearcherVO> {

        @Resource(name="sdao")
        Dao<String, Integer, SearcherVO> dao;
        
        @Override
        public void register(SearcherVO v) throws Exception {
                dao.insert(v);
        }

        @Override
        public void remove1(String k) throws Exception {
                int result = dao.delete1(k);
                if(result == 0) {
                        throw new Exception();
                }
        }

        @Override
        public void modify(SearcherVO v) throws Exception {
                dao.update(v);
        }

        @Override
        public SearcherVO get1(String k) throws Exception {
                return dao.select1(k);
        }

        @Override
        public ArrayList<SearcherVO> get() throws Exception {
                return dao.selectall();
        }
.
.
.(후략)
```

<br>

SearcherDao

``` java
@Repository("sdao")
public interface SearcherDao extends Dao<String,Integer,SearcherVO> {
        
}
```

<br>

Dao

```java
public interface Dao<K1, K2, V> { //K1: STRING, K2: INTEGER
        public void insert(V v) throws Exception;
        public int delete1(K1 k) throws Exception;
        public int delete2(K2 k) throws Exception;
        public int update(V v) throws Exception;
        public V select1(K1 k) throws Exception;
        public V select2(K2 k) throws Exception;
        public ArrayList<V> selectall() throws Exception;
        public ArrayList<V> shop_select(K1 k) throws Exception;
        public ArrayList<V> bookingselect_shop(K1 k) throws Exception;          // 가게 이름 중심으로 예약리스트 출력 
        public ArrayList<V> bookingget_searcher(K1 k) throws Exception;			//searcher id로 예약 리스트 출력 
        public ArrayList<V> bookingupdate_reviewstat(K1 k) throws Exception;
        public ArrayList<V> review_select(K1 k) throws Exception;
        public ArrayList<V> shop_hotplace_select(K1 k) throws Exception;        //핫플 기준으로 가게 출력
        public void shop_hitcnt(K1 k) throws Exception;                         //가게 조회수
        public int shop_score_avg(K1 k) throws Exception;
        public int update_reviewstat2(V v) throws Exception;
        public void bookingcheck_bookstat(K2 k) throws Exception;				//Manager 예약 승인으로 booking stat변경
}
```

<br>

SearcherDao역시 Dao 객체에 대한 의존성을 갖고 있지만, 직접 인스턴스를 생성하지 않는다. Searcher Controller - SearcherBiz - SearcherDao는 모두 bean으로 등록되어 IoC컨테이너가 직접 생성, 의존성 주입, lifeCycle 관리를 제공하고 있다.

<br><br>

## Bean

* 스프링 IoC 컨테이너가 관리하는 객체

<br>

### Bean을 등록하는 방법

<br>

#### * Component Scanning

* **@Component**

  * Repository(SearcherDao)

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.RUNTIME)
  @Documented
  @Component
  public @interface Repository {
  
  	/**
  	 * The value may indicate a suggestion for a logical component name,
  	 * to be turned into a Spring bean in case of an autodetected component.
  	 * @return the suggested component name, if any
  	 */
  	String value() default "";
  
  }
  ```

  <br>

  * Service(SearcherBiz)

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.RUNTIME)
  @Documented
  @Component
  public @interface Service {
  
  	/**
  	 * The value may indicate a suggestion for a logical component name,
  	 * to be turned into a Spring bean in case of an autodetected component.
  	 * @return the suggested component name, if any
  	 */
  	String value() default "";
  
  }
  ```

  <br>

  * Controller(SearcherController)

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.RUNTIME)
  @Documented
  @Component
  public @interface Controller {
  
  	/**
  	 * The value may indicate a suggestion for a logical component name,
  	 * to be turned into a Spring bean in case of an autodetected component.
  	 * @return the suggested component name, if any
  	 */
  	String value() default "";
  
  }
  ```

<br>

Eody 프로젝트에서 사용했던 Controller, Service, Repository **<u>각각의 Annotation은 사실 여러 Annotion을 합친 것</u>**인데, 각 Annotation을 적어주는 것 만으로 Bean으로 사용되고 받아올 수 있었던 것은 **<u>공통적으로 Component Annotation을 포함</u>**하고 있기 때문이다.

Eody 프로젝트에서는 src/com/myspring.xml, web/WEB-INF/config/myspring에서 각각 component를 scan할 범위를 지정해 사용했다.

<br>

**myspring.xml**

<img width="746" alt="myspring" src="https://user-images.githubusercontent.com/46706670/109028387-1709eb80-7705-11eb-9a46-376635192263.png">



<br>

**spring.xml**

<img width="758" alt="spring" src="https://user-images.githubusercontent.com/46706670/109028343-0b1e2980-7705-11eb-9b66-af4f4b62736d.png">



<br>

<br>

#### * 직접 등록

* XML
* 자바 설정 파일

**SampleConfig 생성**

```java
@Configuration
public class SampleConfig {

	@Bean
	public SampleController sampleController() {
		return new SampleController(sampleRepository());
	}
	
	@Bean
	public SampleRepository sampleRepository(){
		return new SampleRepository();
	}
}
```

이후, SampleController나 SampleRepository는 Bean으로 등록되었으므로, @Controller, @Repository를 지워도 정상적으로 인식된다. 



## DI(의존성 주입)

필요한 의존성을 어떻게 받아올 것인가?

<br>

### @Autowired / @ Inject를 어디에 붙일까?

* 생성자
* 필드
* Setter

<br>

*** 참고

* 스프링 프레임워크에서 **권장하는 방법은 생성자를 사용한 의존성 주입**

> 필요한 의존성을 없는 상태로 의존성이 생성되어 Null Point Exception이 발생할 수 있다. 반드시 생성자 Injection 방법이 필요한 것은 아니고, 특정 상황(순환 참조 등)에 한해 Setter나 Field 방법으로 해결할 수 있다.

* 스프링 4.3버전부터 클래스에 생성자가 하나이고, 생성자로 주입받는 레퍼런스 변수들이  모두 Bean으로 관리되고 있다면 @Autowired를 작성하지 않아도 자동으로 인식해준다.

# 참고 자료

* 예제로 배우는 스프링 입문 개정판(2019.02) 교재 - 백기선