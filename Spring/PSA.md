# PSA(Portable Service Abstraction)



## PSA 개요



SearcherController - Eody 프로젝트

<img width="572" alt="스크린샷 2021-03-03 오후 6 06 42" src="https://user-images.githubusercontent.com/46706670/109986765-66759a80-7d49-11eb-95ad-6ec4b784554b.png">



Spring을 사용하며 @RequsetMapping Annotation을 이용해 Request 처리를 시켰다. 

>  Spring을 사용하기 전에는 동적 웹을 어떻게 구현했지..?

Spring을 사용하지 않고 동적 웹을 구성할 때, Servlet 기반으로 직접 Servlet이나 JSP를 이용해 구성했다. Spring도 Servlet을 기반으로 동적 서버 기능을 구현하지만, 개발자는 `@GetMapping`, `@PostMapping`, `@RequsetMapping`을 통해 직접 Servlet을 구현하지 않아도 Method 단위로 클라이언트의 요청을 Mapping 시키는 것이 가능하다.

<br>

[Servlet 복습하기](https://github.com/socialDe/TIL/blob/master/Learned_Contents/Web/Servlet_%EA%B0%9C%EC%9A%94%EC%99%80_%EA%B5%AC%ED%98%84.md)

> **<u>JSP(Java Server Page)</u>**
>
> * HTML 또는 XML 기반의 동적인 웹 콘텐츠를 개발하는 기술
> * 정적인 내용은 HTML, XML로 작성하고, 동적인 내용은 JSP태그와 스크립트 코드로 작성
> * Servlet은 Java 코드 안에 HTML이 들어가는 구조지만, JSP는 HTML안에 자바 코드가 들어가는 구조(ex. JSTL)
> * JSP는 JSP컨테이너에 의해 Servlet 소스 -> Servlet 클래스 -> Servlet 객체로 변환되어 **결과적으로 Servlet 컨테이너에 의해 관리**됌.

<br>

=> 이처럼 내부에서는 Servlet 기반으로 코드가 동작하지만 Servlet 기술은 숨겨져 있는 Service Abstraction을 Spring은 제공하고 있다.

<br>

* **Service Abstraction**: 추상화 계층을 사용해 어떤 기술을 내부에 숨기고 개발자에게 편의성을 제공하는 것
* **<u>Portable Service Abstraction</u>**: 서비스 추상화로 제공되는 기술을 **<u>다른 기술 스택으로 간편하게 바꿀 수 있는 확장성</u>**

=> Spring은 Spring Web MVC, Spring Transaction, Spring Cache등의 다양한 PSA를 제공함.



<br><br><br>

## 사례

### 1. Spring Web MVC 환경 교체

**(Spring Web MVC -> Spring 5 webflux)**

<img width="1385" alt="스크린샷 2021-03-04 오후 11 36 10" src="https://user-images.githubusercontent.com/46706670/109986857-78efd400-7d49-11eb-9d14-431f97c158d9.png">

>  PetClinic 예제를 실행해보면 Tomcat을 기반으로 기존 실행

<br>

<img width="629" alt="스크린샷 2021-03-04 오후 11 40 26" src="https://user-images.githubusercontent.com/46706670/109986908-84db9600-7d49-11eb-8805-9a3d195dd5c2.png">



>  pom.xml에서 spring dependency를 수정

<br>

<img width="1165" alt="스크린샷 2021-03-04 오후 11 42 50" src="https://user-images.githubusercontent.com/46706670/109986925-8907b380-7d49-11eb-8aba-5df9ab70e765.png">



> 기존 Tomcat 기반 실행에서 Netty 기반으로 변경을 확인

<br>

[기존 Netty 기반 HttpServer 생성하기 예제](https://netty.io/4.1/xref/io/netty/example/http/snoop/HttpSnoopServer.html)

기존 소스코드의 수정을 하지 않고 손쉽게 dependency를 교체함으로써 다른 기술 스택으로 변경!

<br><br>

### 2. Spring Transaction

Low level로 트랜잭션 처리를 하려면 setAutoCommit()과 commit(), rollback()을 명시적으로 호출해야 하지만, Spring에서는 `@Transactional` Annotation으로 단순하게 메서드에 트랜잭션 처리를 할 수 있다.

**이런 Spring Transaction도 PSA로 다양한 기술 스택으로 구현체를 변경할 수 있다.**

예를 들어 아래와 같은 트랜잭션을 실제로 처리하는 구현체를 유연하게 바꿔서 사용할 수 있다.

* JDBC를 사용하는 DatasourceTransactionManager
* JPA를 사용하는 JpaTransactionManager
* Hibernate를 사용하는 HibernateTransactionManager



**<u>소스코드에는 @Transactional 애너테이션을 붙여놓은 상태로 소스코드를 수정하지 않고 자유롭게 구현체를 수정할 수 있다.</u>**

<br>

### 3. Spring Cache

Cache도 마찬가지로 아래와 같은 여러가지 구현체를 사용할 수 있다.

* JCacheManager
* ConcurrentMapCacheManager
* EhCacheCacheManager

<img width="628" alt="스크린샷 2021-03-04 오후 11 57 29" src="https://user-images.githubusercontent.com/46706670/109987014-9a50c000-7d49-11eb-9888-7a321a8ddd2a.png">



<br>

petClinic 예제 cache 관련 pom.xml source

<img width="237" alt="스크린샷 2021-03-05 오전 12 04 11" src="https://user-images.githubusercontent.com/46706670/109987060-a472be80-7d49-11eb-8c4d-f99c73e87ceb.png">



**<u>결과적으로 사용자는 실제 구현체를 크게 신경쓰지 않고 `@Cacheable` Annotation을 메서드에 붙임으로써 사용하고, 수정할 수 있다.</u>**



# 출처

* [예제로 배우는 스프링 입문(ver 2019.02) - 백기선(Youtube)](https://www.youtube.com/watch?v=iAvOv5Xsn0M&list=PLfI752FpVCS8_5t29DWnsrL9NudvKDAKY&index=13)



