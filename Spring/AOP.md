## AOP(Aspect Oriented Programming, 관점지향프로그래밍)

Spring은 Spring Triangle이라고 부르는 세 가지 개념을 제공해준다. 각각 IoC, AOP, PSA를 일컫는다.

AOP는 Aspect Oriented Programming의 약자로 '측면/양상 지향적인 프로그래밍'이라는 의미이다.

<u>**'측면/양상 지향 프로그래밍'이 무엇을 의미하는가?**</u>



```java
class A {
 
    method a() {
        AAAA
        method a가 하는 일들
        BBBB
    }
 
    method b() {
        AAAA
        method b가 하는 일들
        BBBB
    }
}
 
class B {
    method c() {
        AAAA
        method c가 하는 일들 
        BBBB
    }
}
```



위와 같이 동일한 일을 하는 코드 AAAA, BBBB가 여기저기서 사용되고 이렇게 흩어져있으면 코드 변경이 필요한 경우 일일이 다 찾아서 바꿔야한다.

AOP는 그렇게 하지 않고 여러군데서 사용되는 중복되는 코드를 떼어내서 분리하고, method a, b, c는 자신이 해야할 작업만 갖고있자는 개념이다.

여기서 '여러군데서 사용되는 중복되는 코드'가 AOP에서 말하는 'aspect'라고 이해하면 된다.



## Proxy Pattern

Spring AOP는 프록시 패턴이라는 디자인 패턴을 사용해서 AOP 효과를 낸다.

프록시 패턴을 사용하면 어떤 기능을 추가하려 할때 기존 코드를 변경하지 않고 기능을 추가할수 있다.

어떤 클래스가 Spring AOP의 대상이라면 그 기존 클래스의 빈이 만들어질때 Spring AOP가 프록시(기능이 추가된 클래스)를 자동으로 만들고 원본 클래스 대신 프록시를 빈으로 등록한다. 

그리고 원본 클래스가 사용되는 지점에서 프록시를 대신 사용한다.

Spring의 PetClinic 예제에서 OwnerRepository 인터페이스의 @Transactional 애노테이션이 이에 해당한다.



![?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fm6bz7%2FbtqChF76rtt%2F9HIQs3eFYUVgKgQo7juWbk%2Fimg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fm6bz7%2FbtqChF76rtt%2F9HIQs3eFYUVgKgQo7juWbk%2Fimg.png)



@Transactional 애노테이션이 붙어있으면 OwnerRepository 타입의 프록시가 새로 만들어지고 Spring AOP에 의해 자동으로 생성되는 OwnerRepository의 프록시에는 @Transactional 애노테이션이 지시하는 코드가 삽입된다 

@Transactional 애노테이션에 의해 추가되는 기능은 다음과 같다.

JDBC에서 트랜잭션 처리를 하려면 SQL 실행문 앞뒤에 setAutoCommit()와 commit()/rollback() 코드가 항상 붙는데 @Transactional 애노테이션은 **<u>프록시에 자동으로 그 코드를 넣어서 반복, 중복되는 코드를 생략</u>**할 수 있게하는 것이다.

<u>**이로 인해 개발자는 비즈니스 로직에만 집중할 수 있게 된다.**</u>





## Quiz

* OOP와 AOP의 차이는 무엇입니까?



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

https://atoz-develop.tistory.com/entry/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-AOP-%EA%B0%9C%EB%85%90-%EC%9D%B4%ED%95%B4-%EB%B0%8F-%EC%A0%81%EC%9A%A9-%EB%B0%A9%EB%B2%95

## Quiz 모범 답안

* OOP와 AOP의 차이는 무엇입니까?

https://geminihoroscope.tistory.com/104?category=824966

<img width="596" alt="스크린샷 2021-02-19 오전 10 37 09" src="https://user-images.githubusercontent.com/46706670/108456486-c5e89a80-72b3-11eb-94d3-e63a56a7d930.png">

