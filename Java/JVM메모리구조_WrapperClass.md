# JVM과 메모리 구조 & Wrapper Class



## JVM

자바 가상 머신으로 **자바 바이트 코드를 실행할 수 있는 주체**다.

운영체제 위에서 동작하는 프로세스로 **자바 코드를 컴파일해서 얻은 바이트 코드를 해당 운영체제가 이해할 수 있는 기계어로 바꿔 실행시켜주는 역할을** 한다.

JVM의 구성을 살펴보면 크게 4가지(Class Loader, Execution Engine, Garbage Collector, Runtime Data Area)로 나뉜다.

<br><br>

<img width="766" alt="스크린샷 2021-03-26 오전 1 31 34" src="https://user-images.githubusercontent.com/46706670/112575370-8a516b00-8e33-11eb-8a07-98ff51ef5a64.png">



<br><br>

### 1. Class Loader

자바로 소스를 작성했다면 소스 파일 ex. Person.java 파일이 생성되고, 컴파일러는 이 파일에 대한 컴파일 과정을 통해 Person.class(바이트코드) 파일을 생성한다. 이렇게 **<u>생성된 class 파일들을 엮어, JVM이 운영체제로부터 할당받은 메모리 영역인 Runtime Data Area로 적재</u>**하는 역할을 Class Loader가 수행한다.

<br><br><br>

### 2. Execution Engine

Class Loader에 의해 메모리에 적재된 클래스(바이트코드)들을 기계어로 변경해 명령어 단위로 실행하는 역할을 한다. 

<br><br><br>

### 3. Garbage Collector

Heap 메모리 영역에 생성(적재)된 객체들 중에 참조되지 않는 객체들을 탐색 후 제거하는 역할을 한다.

GC가 역할을 하는 시간은 정확히 언제인지를 알 수 없다. (참조가 없어지자마자 해제되는 것을 보장하지 않음)

또 다른 특징은 GC가 수행되는 동안 GC를 수행하는 쓰레드가 아닌 다른 모든 쓰레드가 일시정지 된다.(Stop the world)

자세한 내용은 별도 문서로 기술

<br><br><br>

### 4. Runtime Data Area

운영체제로부터 할당받은 메모리 영역이며, 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역이다.

크게 Method Area, Heap Area, Stack Area, PC Register, Native Method Stack로 나눌 수 있다.

<br><br><br>

#### Method Area

클래스 멤버 변수의 이름, 데이터 타입, 접근 제어자 정보같은 `필드 정보`와 메소드의 이름, 리턴 타입, 파라미터, 접근 제어자 정보 같은 `메소드 정보`,` Type정보`(Interface인지 class인지), `Constant Pool`(상수 풀: 문자 상수, 타입, 필드, 객체 참조가 저장됌), `static 변수`, `final class 변수` 등이 생성되는 영역이다.

<br><br>

#### Heap Area(아래에 Stack Area와 상세 비교)

* 동적으로 할당한 메모리 영역
* 모든 Object 타입의 데이터가 할당
* Heap 영역의 Object를 가리키는 참조 변수가 Stack에 할당

new 키워드로 생성된 객체와 배열이 생성되는 영역이다.

메소드 영역에 로드된 클래스만 생성이 가능하고 Garbage Collector가 참조되지 않는 메모리를 확인하고 제거하는 주 대상 영역이다.

<br><br>

#### Stack Area(아래에 Heap Area와 상세 비교)

* 정적으로 할당한 메모리 영역
* 원시 타입의 데이터가 값과 함께 할당
* Heap 영역에 생성된 Object 타입의 참조 값 할당

지역 변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값등이 생성되는 영역이다.

<br><br>

#### PC Register

쓰레드가 생성될 때마다 생성되는 영역으로 Program Counter, 현재 쓰레드가 실행되는 부분의 주소와 명령어를 저장하고 있는 영역이다.(* CPU의 레지스터와 다름)

이를 이용해서 쓰레드를 돌아가면서 수행할 수 있게 한다.

<br><br>

#### Native Method Stack

자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역이다. 

보통 C/C++ 등의 코드를 수행하기 위한 스택이다.(`JNI`)

쓰레드가 생성되었을 때 기준으로 1, 2번인 메소드 영역과 힙 영역을 모든 쓰레드가 공유하고,

3, 4, 5 번인 스택 영역과 PC 레지스터, Native method stack은 각각의 쓰레드마다 생성되고 공유되지 않는다.

> JNI(Java Native Interface)?
>
> **자바 네이티브 인터페이스**(Java Native Interface, JNI)는 [자바 가상 머신](https://ko.wikipedia.org/wiki/자바_가상_머신)(JVM)위에서 실행되고 있는 자바코드가 네이티브 응용 프로그램(하드웨어와 운영 체제 플랫폼에 종속된 프로그램들) 그리고 C, C++ 그리고 어샘블리 같은 다른 언어들로 작성된 라이브러리들을 호출하거나 반대로 호출되는 것을 가능하게 하는 프로그래밍 프레임워크이다.



<br><br><br><br>



## Wrapper Class

* 8개의 기본형 변수를 객체로 다루기 위한 클래스

> 객체지향 개념에서 모든 것은 객체로 다뤄져야 한다. 그러나 자바에서는 8개의 기본형을 객체로 다루지 않는데, 이것이 바로 자바가 완전한 객체지향 언어가 아니라는 얘기를 듣는 이유이다. 그 대신 보다 높은 성능을 얻을 수 있었다.
>
> 때로는 기본형(primitive type) 변수도 어쩔 수 없이 객체로 다뤄야 하는 경우가 있다. 예를 들면 매개변수로 객체를 요구할 때, 기본형 값이 아닌 객체로 저장해야할 때, 객체간의 비교가 필요할 때 등등의 경우에는 기본형 값들을 객체로 변환해 작업을 수행해야 한다.
>
> 이 때 사용되는 것이 래퍼(wrapper) 클래스이다. 8개의 기본형을 대표하는 래퍼클래스가 있는데, 이 클래스들을 이용하면 기본형 값을 객체로 다룰 수 있다. 

<br><br>

| 기본형  | 래퍼클래스 |
| ------- | ---------- |
| boolean | Boolean    |
| char    | Character  |
| byte    | Byte       |
| short   | Short      |
| int     | Integer    |
| long    | Long       |
| float   | Float      |
| double  | Double     |



<br><br><br><br><br><br>

## Stack Area & Heap Area 상세 비교

### Stack Area

* 원시 타입의 데이터가 값과 함께 할당
* Heap 영역에 생성된 Object 타입의 참조 값 할당

<br><br>

```java
public class Main {
    public static void main(String[] args) {
        int argument = 4;
        argument = someOperation(argument);
    }

    private static int someOperation(int param){
        int tmp = param * 3;
        int result = tmp / 2;
        return result;
    }
}
```

<br><br>

```java
int argument = 4;
```

<img width="236" alt="스크린샷 2021-03-26 오전 2 27 51" src="https://user-images.githubusercontent.com/46706670/112575375-8cb3c500-8e33-11eb-9531-e185d6e05e9e.png">



<br><br>

```java
argument = someOperation(argument);
```

<img width="246" alt="스크린샷 2021-03-26 오전 2 28 03" src="https://user-images.githubusercontent.com/46706670/112575406-9c330e00-8e33-11eb-9ddf-890650e134f2.png">



<br><br>

```java
int tmp = param * 3;
int result = tmp / 2;
```

<img width="249" alt="스크린샷 2021-03-26 오전 2 28 29" src="https://user-images.githubusercontent.com/46706670/112575498-c4bb0800-8e33-11eb-98fc-e6bf123658c1.png">



<br><br>

* `someOperation()` 함수 종료!

<img width="252" alt="스크린샷 2021-03-26 오전 2 28 49" src="https://user-images.githubusercontent.com/46706670/112575511-c71d6200-8e33-11eb-8da6-ba5073517330.png">



<br><br><br>

### Heap Area

* 모든 Object 타입의 데이터가 할당
* Heap 영역의 Object를 가리키는 참조 변수가 Stack에 할당

<br><br><br>

* 기본적인 Heap Area 동작 방식

```java
public class Main {
    public static void main(String[] args) {
        int port = 4000;
        String host = "localhost";
    }
}
```

<br>

<img width="684" alt="java-memory-management_heap-1-20210326023015414" src="https://user-images.githubusercontent.com/46706670/112575807-63dfff80-8e34-11eb-9ec6-5444acbc95fb.png">



<img width="675" alt="java-memory-management_heap-2" src="https://user-images.githubusercontent.com/46706670/112575817-68a4b380-8e34-11eb-8117-8a9c3b6f14e2.png">





<br><br>

* Heap Area와 Stack Area의 연동

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> listArgument = new ArrayList<>();
        listArgument.add("jaeuk");
        listArgument.add("github");

        print(listArgument);
    }

    private static void print(List<String> listParam) {
        String value = listParam.get(0);
        listParam.add("io");
        System.out.println(value);
    }
}
```

<br><br>

```java
List<String> listArgument = new ArrayList<>();
```



<img width="698" alt="java-memory-management_heap-3" src="https://user-images.githubusercontent.com/46706670/115541622-4d658080-a2da-11eb-9501-c2dfaec5cab1.png">



<br><br>

```java
listArgument.add("jaeuk");
listArgument.add("github");
```

<img width="683" alt="java-memory-management_heap-5" src="https://user-images.githubusercontent.com/46706670/112575873-840fbe80-8e34-11eb-80ad-9b3de1955198.png">

(그림의 yaboong == jaeuk)



<br><br>



```java
print(listArgument);
```

<img width="694" alt="java-memory-management_heap-6" src="https://user-images.githubusercontent.com/46706670/112575995-bcaf9800-8e34-11eb-88f9-ef733d8ac1e6.png">



<br><br>

```java
String value = listParam.get(0);
listParam.add("io");
System.out.println(value);
```

<img width="678" alt="java-memory-management_heap-7" src="https://user-images.githubusercontent.com/46706670/112576000-be795b80-8e34-11eb-8b64-f822601b2e83.png">



<br><br>

* print(listArgument); 함수 호출 종료!

<img width="703" alt="java-memory-management_heap-8" src="https://user-images.githubusercontent.com/46706670/112576025-ce913b00-8e34-11eb-9e3f-ff7e355864d1.png">



<br><br>

* Heap Area와 Stack Area의 연동2

```java
public class Main {
    public static void main(String[] args) {
        Integer a = 10;
        System.out.println("Before: " + a);
        changeInteger(a);
        System.out.println("After: " + a);
    }

    public static void changeInteger(Integer param) {
        param += 10;
    }
}
```

> Integer 도 Object 를 상속받아 구현되었으니… Object 타입이고…
>
> 당연히 20이 나오지 않을까?
>
> .
>
> .
>
> .
>
> 20이 아닌 10이 그대로 출력된다.

아래 예시로 왜 20으로 변경되지 않는지 더 쉽게 이해할 수 있다.

<br><br>

```java
public class Main {
    public static void main(String[] args) {
        String s = "hello";
        changeString(s);
        System.out.println(s);
    }
    public static void changeString(String param) {
        param += " world";
    }
}
```

<br><br>

```java
String s = "hello";
```

<img width="760" alt="스크린샷 2021-03-26 오전 2 44 16" src="https://user-images.githubusercontent.com/46706670/112576065-e4066500-8e34-11eb-8d29-591cdaa3e8dc.png">



<br><br>

```java
changeString(s);
```

<img width="718" alt="스크린샷 2021-03-26 오전 2 47 29" src="https://user-images.githubusercontent.com/46706670/112576069-e5d02880-8e34-11eb-822f-64a2d1991d86.png">



<br><br>



```java
param += "world";
```

<img width="739" alt="스크린샷 2021-03-26 오전 2 48 05" src="https://user-images.githubusercontent.com/46706670/112576074-e799ec00-8e34-11eb-9440-1053f7f033b8.png">



<br><br>

* changeString(s) 함수 호출 종료!

<img width="729" alt="스크린샷 2021-03-26 오전 2 49 27" src="https://user-images.githubusercontent.com/46706670/112576131-0a2c0500-8e35-11eb-8399-8aef95b9a9e5.png">





새롭게 생성된 "hello world" 오브젝트를 레퍼런스 하는 param 이라는 변수는 스택에서 pop되므로, **"hello world" 오브젝트는 어느 변수도 레퍼런스 하지 않는 상태**가 된다.

> 그러므로, changeString() 메소드를 수행하고 돌아가도 기존에 “hello” 를 레퍼런스하고 있던 s 변수의 값은 그대로이다. Immutable Object 는 불변객체로써, 값이 변하지 않는다. (String은 Immutable한 객체!) 변경하는 연산이 수행되면 변경하는 것 처럼 보이더라도 실제 메모리에는 새로운 객체가 할당되는 것이다.
>
> Java에서 Wrapper class에 해당하는 Integer, Character, Byte, Boolean, Long, Double, Float, Short 클래스는 모두 Immutable이다. 그래서 heap에 있는 같은 오브젝트를 레퍼런스 하고 있는 경우라도, 새로운 연산이 적용되는 순간 새로운 오브젝트가 heap에 새롭게 할당된다.
>
> Integer 클래스를 까보면 내부에서 사용하는 실제 값인 value 라는 변수가 있는데, 이 변수는 private final int value; 로 선언 되어있다. 즉, 생성자에 의해 생성되는 순간에만 초기화되고 변경불가능한 값이 된다. 이것 때문에 Wrapper class 들도 String 처럼 Immutable 한 오브젝트가 되는 것이다.



이런 경우 **<u>"hello world" 오브젝트는 garbage로 분류</u>**된다.

<br><br><br><br>

# Quiz

* Primititive type과 Reference type은 무엇입니까?
* Wrapper Class는 무엇입니까?
* 자바의 메모리 영역은 어떻게 구성되어 있나요?

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

# 출처(참고 자료)

* [JVM 구조와 자바 런타임 메모리 구조](https://jeong-pro.tistory.com/148)
* [던의 JVM Garbage Collector - 우아한Tech(Youtube)](https://www.youtube.com/watch?v=vZRmCbl871I&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=64)
* 자바의 정석 - 남궁성
* [자바 메모리 관리 - 스택 & 힙](https://yaboong.github.io/java/2018/05/26/java-memory-management/)
* [신입개발자 기술면접 #1 - Java 질문 모음](https://sas-study.tistory.com/53)

# Quiz 답안

* **Primititive type과 Reference type은 무엇입니까?**

Primitive type – 변수에 값 자체를 저장(정수형, 실수형, 문자형, 논리형) – Wrapper Class를 통해 객체로 변환 가능

Reference type – 메모리상에 객체가 있는 위치를 저장

종류 – Class, Interface, Array 등



* **Wrapper Class는 무엇입니까?**

Primitive type으로 표현할 수 있는 간단한 데이터를 객체로 만들어야 할 경우가 있는데 그러한 기능을 지원



* **자바의 메모리 영역은 어떻게 구성되어 있나요?**

\- 메서드 영역 : static 변수, 전역변수, 코드에서 사용되는 Class 정보 등이 올라간다. 코드에서 사용되는 class들을 로더로 읽어 클래스별로 런타임 필드데이터, 메서드 데이터 등을 분류해 저장한다.

\- 스택(Stack) : 지역변수, 함수(메서드) 등이 할당되는 LIFO(Last In First Out) 방식의 메모리

\- 힙(Heap) : new 연산자를 통한 동적 할당된 객체들이 저장되며, Garbage 컬렉션에 의해 메모리가 관리되어 진다.

이외 PC 레지스터와 Native Method Stack이 있습니다.