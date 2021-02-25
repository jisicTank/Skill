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



StoreTest.java(JUnit)

```java
class StoreTest {

	@Test
	void test() {
		Payment cashPerf = new Cash();
		Store store = new Store(cashPerf);
		store.buySomething(100);
	}
}
```



> 이 계산하는 과정에 시간 성능을 보고 싶은데.. 기능을 추가해볼까?



CashPerf.java

```java
public class CashPerf implements Payment{
	
	Payment cash = new Cash();

	@Override
	public void pay(int amount) {
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
		
		System.out.println(amount+ " 현금 결제");
		
		stopWatch.stop();
		System.out.println(stopWatch.prettyPrint());
	}
}
```



**기존 코드를 변경하지 않고, CashPerf를 생성하면 기능을 더할 수 있다.** (의존성 주입 IoC 컨테이너)

CashPerf는 Cash의 Proxy이다. CashPerf는 Cash의 기능에 더불어 부가적인 기능을 더해 갖고 있기 때문이다. Store에서는 Cash를 직접 사용하지 않고, Cash에 부가적인 기능을 더한 CashPerf 를 사용한다. 

스프링에서는 이처럼 Proxy Pattern으로 AOP를 구현하고 있다.



### Spring에서 AOP 사용하기

@LogExecutionTime 을 원하는 기능에 붙여보자

