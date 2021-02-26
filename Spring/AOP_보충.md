

# AOP, 프록시 패턴 보충

## AOP

```java
class A {
    method a() {
        AAAA
				탐앤탐스에서 커피를 주문하세요.
        BBBB
    }
 
    method b() {
        AAAA
        상관에게 보고서를 전달합니다.
        BBBB
    }
}

class B {
    method c() {
        AAAA
        설거지를 합니다.
        BBBB
    }
}
```

-----> AAAA or BBBB 수정에서 모든 코드를 수정해야 하는 문제

```java
class A {
    method a() {
        탐앤탐스에서 커피를 주문하세요.
    }
 
    method b() {
        상관에게 보고서를 전달합니다.
    }
}
 
class B {
    method c() {
        설거지를 합니다.
    }
}
class AAAABBBB{
  	method aaaabbbb(JoinPoint point){
      	AAAA
      	point.execute()
        BBBB
    }
}
```



<br>



### 다양한 AOP 구현 방법

* **컴파일**

A.java --- (AOP) ---> A.class(AspectJ 컴파일러)

* **바이트코드 조작**

A.java -> A.class, Class loader가 클래스 파일을 읽어서 메모리에 올릴 때 AOP를 적용(AspectJ)

* **프록시 패턴**

Spring AOP가 사용하는 방법!

기존의 코드를 거의 수정하지 않고, 기능을 추가하는 방법..

참고: https://refactoring.guru/design-patterns/proxy



<br>

### Eody 프로젝트에 적용된 AOP

Biz.java

```java
public interface Biz<K1, K2, V> { //K1: STRING, K2: INTEGER
        @Transactional
        public void register(V v) throws Exception;
        @Transactional
        public void remove1(K1 k) throws Exception;
        @Transactional
        public void remove2(K2 k) throws Exception;
        @Transactional
        public void modify(V v) throws Exception;
.
.
.(후략)
```

@Transactional Annotation은 JDBC트랜잭션 연산에 사용되는 autoCommit(false), 예외처리 rollback 등과 같은 기능들을 Annotation 하나로 지원해준다.

<br>

<br>



## 프록시(Proxy) 패턴

* Proxy ==> 대리인
* 기존 코드 변경하지 않고 새 기능 추가하기

<br>

proxy 패키지 생성 - Payment 인터페이스

```java
public interface Payment {
	public void pay(int amount);
}

```

<br>

Cash.java

```java
public class Cash implements Payment{

	@Override
	public void pay(int amount) {
		System.out.println(amount+" 현금 결제");
	}

}
```

<br>

Store.java(Client code)

```java
public class Store {
	Payment payment;

	public Store(Payment payment) {
		this.payment = payment;
	}
	
	public void buySomething(int amount) {
		payment.pay(amount);
	}
}
```

<br>

StoreTest.java(JUnit)

```java
class StoreTest {

	@Test
	void test() {
		Payment cashPerf = new CashPerf();
		Store store = new Store(cashPerf);
		store.buySomething(100);
	}
}
```

<br>

> 이 계산하는 과정에 시간 성능을 보고 싶은데.. 기능을 추가해볼까?

<br>

CashPerf.java

```java
public class CashPerf implements Payment{
	
	Payment cash = new Cash();

	@Override
	public void pay(int amount) {
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
		
		cash.pay();
    SQL
		
		stopWatch.stop();
		System.out.println(stopWatch.prettyPrint());
	}
}
```

<br>

**기존 코드를 변경하지 않고, CashPerf를 생성하면 기능을 더할 수 있다.** (의존성 주입 IoC 컨테이너)

CashPerf는 Cash의 Proxy이다. CashPerf는 Cash의 기능에 더불어 부가적인 기능을 더해 갖고 있기 때문이다. Store에서는 Cash를 직접 사용하지 않고, Cash에 부가적인 기능을 더한 CashPerf 를 사용한다. 

스프링에서는 이처럼 Proxy Pattern으로 AOP를 구현하고 있다.

<br>

### Spring에서 AOP 사용하기

@LogExecutionTime 을 원하는 기능에 붙여보자

이번 실습은 Spring boot를 활용하기때문에 eody 프로젝트가 아닌 스프링 공식 프로젝트인 petclinic으로 보여줌.

<br>

* 원하는 위치에 @LogExecutionTime을 붙여주고, Annotation File 자동생성

<br>

**LogExecutionTime Annotation File**

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

// JAVA ANNOTATION
@Target(ElementType.METHOD) // 어디에 쓸 수 있는지 -> 메서드에 쓰겠다
@Retention(RetentionPolicy.RUNTIME) // 애너테이션 정보를 언제까지 유지할 것인가 -> RUNTIME
public @interface LogExecutionTime {
}
```

<br>

**LogAspect**

```java
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import org.springframework.util.StopWatch;


@Component
@Aspect
public class LogAspect {
	Logger logger = LoggerFactory.getLogger(LogAspect.class);

	@Around("@annotation(LogExecutionTime)")
	public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();

		Object proceed = joinPoint.proceed();

		stopWatch.stop();
		logger.info(stopWatch.prettyPrint());

		return proceed;
	}
}
```

<br>

**테스트 결과 콘솔**

![스크린샷 2021-02-26 오전 12.10.41]($md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-02-26%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.10.41.png)



http://localhost:8080/



