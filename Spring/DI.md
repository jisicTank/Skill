# DI(Dependency Injection, 의존성 주입)

> 객체간의 의존성을 자신이 아닌 외부에서 주입하는 개념



## IoC(Inversion of Control, 제어의 역전)

DI 이전에 IoC의 개념을 알고 넘어가야할 필요가 있다. Spring을 쓰기 전에는 개발짜가 프로그램의 흐름(애플리케이션 코드)을 제어하는 주체였다. 스프링에서는 프로그램의 흐름을 프레임워크가 주도하게 된다.(ex. @Autowired 등으로 Bean을 자동 주입) 객체의 생성~ 생명주기 관리를 컨테이너가 도맡아서 하게 된 것이다.

즉, **<u>제어권이 컨테이너로 넘어가게 되고</u>**, 이것을 제어권의 흐름이 바뀌었다고 해 IoC라고 하게 된다. **<u>제어권이 컨테이너로 넘어옴으로써 DI, AOP등이 가능하게 된다.</u>**

반대로 말하면 스프링에게 애플리케이션의 흐름을 제어하는 권한이 없다면, Autowired를 통한 의존성 주입을 할 수 없을 것이다.



의존성 주입 방법 3가지

>  Inversion of Control Containers and the Dependency Injection pattern - 마틴 파울러

* 생성자를 이용한 의존성 주입
* setter 메소드를 이용한 의존성 주입
* 초기화 인터페이스를 이용한 의존성 주입





실행 결과: Hello, Spring

```java
/*
* Created by james on 16. 2. 10.
*/

public class HelloApp{
  public static void main(String[] args){
    MessageBeanEn bean = new MessageBeanEn();
    bean.sayHello("Spring");
  }
}
```

```java
/*
* Created by james on 16. 2. 10.
*/
public class MessageBeanEn{
  public void sayHello(String name){
    System.out.println("Hello, "+name+"!");
  }
}
```



HelloApp은 MessageBeanEn 클래스의 sayHello 메소드를 호출해 `"Hello, Spring!"` 이라는 문장을 출력한다.

>  여기서 조금 바꿔, 한글로 출력하려면 어떻게 해야할까?

```java
/*
* Created by james on 16. 2. 10.
*/

public class HelloApp{
  public static void main(String[] args){
    MessageBeanKr bean = new MessageBeanKr(); // MessageBeanEn -> MessageBeanKr로 변경
    bean.sayHello("Spring");
  }
}
```

```java
/*
* Created by james on 16. 2. 10.
*/
public class MessageBeanKr{
  public void sayHello(String name){
    System.out.println("안녕, "+name+"!");
  }
}
```



MessageBean을 호출하던 main에서 En을 Kr로 바꿔줘야한다.
이런 경우 `HelloApp이 MessageBean에 의존성을 가지고 있다`고 한다.
HelloApp의 기능을 바꾸고자 할 때, MessageBean도 함께 바꿔줘야 하기 때문이다.

>  의존성을 낮추고 싶다...(프로그램의 유지보수를 쉽게 하고 싶다...)



이러한 의존성을 해결하기 위해서 객체의 인스턴스를 외부에서 생성받으면 어떨까?





초기화 인터페이스를 사용해보자.

MessageBeanKr과 MessageBeanEn에 대한 인터페이스를 구현해 그 전보다 HelloApp의 소스 변경을 줄였다.

```java
public interface MessageBean{
  public void sayHello(String name);
}
```

```java
/*
* Created by james on 16. 2. 10.
*/
public class MessageBeanKr implements MessageBean{
  public void sayHello(String name){
    System.out.println("안녕, "+name+"!");
  }
}
```

```java
/*
* Created by james on 16. 2. 10.
*/
public class MessageBeanEn implements MessageBean{
  public void sayHello(String name){
    System.out.println("Hello, "+name+"!");
  }
}
```

```java
/*
* Created by james on 16. 2. 10.
*/

public class HelloApp{
  public static void main(String[] args){
		MessageBean bean = new MessageBeanKr(); // 대입문을 En으로 바꿔주면 영문이 출력된다.
    bean.sayHello("Spring");
  }
}
```

그러나, 이 역시 대입문에서 약간의 소스코드 변경이 필요하다.



이번엔 설정 파일을 만들어, 외부에서 MessageBean에 주입할 객체에 대한 설정 정보를 담아 사용해 본다.



- beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<bean id = "messageBean" class = "sample1.MessageBeanKr"/>
</beans>
```



- HelloApp.java

```java
package sample1;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.FileSystemResource;

public class HelloApp{
  public static void main(String[] args){
    BeanFactory factory = new XmlBeanFactory(new FileSystemResource("resources/beans.xml"));
    
    // bean이 사용하는 클래스 이름을 코드에 직접 기술하지 않는다. 즉 의존성이 없다.
    MessageBean bean = factory.getBean("messageBean", MessageBean.class);
    bean.sayHello("Spring");
  }
}
```



이렇게 소스 코드의 변경 없이 환경설정만으로도 프로그램을 제어할 수 있다.

이것이 가능한 이유는, 객체의 생명주기를 스프링 컨테이너가 관리하는 IoC 개념이 있기 때문이다.



결론: 스프링에서의 의존성 주입은 객체의 실체를 외부 환경설정(spring config xml, Bean 객체 등) 에서 컨트롤 할 수 있게 하는 것

왜? : 모듈 간의 결합도를 낮춰서 유연한 변경을 가능하게 하기 위하여











## Quiz

* Spring에서 DI란 무엇입니까?

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>







## 출처

 https://jhleed.tistory.com/61





## Quiz 모범 답안

* Spring에서 DI란 무엇입니까?

https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]

DI는 Dependency Injection(의존성 주입)의 약자로, 객체들 간의 의존성을 줄이기 위해 사용되는 Spring의 IOC 컨테이너의 구체적인 구현 방식입니다.

DI는 기존처럼 개발코드 부분에서 객체를 생성하는 것이 아니라, 팩토리 패턴처럼 객체의 생성과, 데이터를 주입만 담당하는 Factory에 해당 하는 별도의 공간에서 객체를 생성하고 데이터간의 의존성을 주입해 개발코드에서는 이를 가져다 씀으로서 의존성을 줄이는 방식입니다. 이때, Factory 패턴의 Factory Class의 역할을 스프링의 환경설정 파일이 담당합니다. 설정 파일을 통해 객체간의 의존관계를 설정함으로써 외부 Assembler가 객체간의 의존 관계를 정의하게 되며, 객체는 직접 의존하고 있는 객체를 생성하거나 검색할 필요가 없어지므로 코드의 관리가 쉬워진다.