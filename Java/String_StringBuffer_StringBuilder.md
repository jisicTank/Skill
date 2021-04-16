# String, StringBuffer, StringBuilder

 <br> <br>

|      분류      |  String   |           StringBuffer           |    StringBuilder    |
| :------------: | :-------: | :------------------------------: | :-----------------: |
| 변경 가능 여부 | Immutable |             Mutable              |       Mutable       |
|     동기화     |           | Synchronizerd 가능(Multi-Thread) | Synchronized 불가능 |



<br><br>

---

## String

* new 연산을 통해 생성된 인스턴스의 메모리 공간은 변하지 않음(Immutable)
* Garbage Collector로 제거되어야 함
* 문자열 연산시 새로 객체를 만드는 Overhead 발생
* 객체가 불변하므로, Multi-Thread에서 동기화를 신경 쓸 필요가 없음(조회 연산에 매우 큰 장점)

> 동기화(Synchronize)?
>
> 한 쓰레드가 진행중인 작업을 다른 쓰레드가 간섭하지 못하게 막는 것

<br><br><br><br>

<img width="729" alt="스크린샷 2021-03-26 오전 2 49 27" src="https://user-images.githubusercontent.com/46706670/115023407-b6737f80-9ef9-11eb-9897-7dce31ad9cdd.png">

문자열 연산으로 "hello" +" world"를 시행하면 메모리 공간에서 직접적으로 저장된 값을 변경하는 것이 아니라, 새로 인스턴스를 생성한 뒤 새로 생성한 인스턴스의 주소값을 s가 저장하는 방식으로 연산이 진행된다. 

<br><br><br>

## StringBuffer

* 인스턴스에 저장된 문자열을 직접 변경할 수 있는 클래스
* 문자열 편집을 위한 버퍼를 가지고 있고, StringBuffer 인스턴스를 생성할 때 그 크기를 지정할 수 있음
* StringBuffer 인스턴스가 생성될 때, char형 배열이 생성됨
* 생성된 char형 배열을 인스턴스변수 value가 참조함

```java
public final class StringBuffer
    extends AbstractStringBuilder
    implements java.io.Serializable, CharSequence
{...
```

StringBuffer 클래스는 AbstractStringBuilder클래스를 상속받고 있다. 이 AbstractStringBuilder를 살펴보면 char형 배열 value를 확인할 수 있다.(Java 1.8.0_261 기준)

```java
abstract class AbstractStringBuilder implements Appendable, CharSequence {
    /**
     * The value is used for character storage.
     */
    char[] value;

    /**
     * The count is the number of characters used.
     */
    int count;
  ...
```



StringBuffer 클래스는 이를 상속받으며 생성자를 통해 이 value 값을 설정하고 있는데, 이를 살펴보면 다음과 같다.

```java
    /**
     * Constructs a string buffer with no characters in it and an
     * initial capacity of 16 characters.
     */
    public StringBuffer() {
        super(16);
    }

    /**
     * Constructs a string buffer with no characters in it and
     * the specified initial capacity.
     *
     * @param      capacity  the initial capacity.
     * @exception  NegativeArraySizeException  if the {@code capacity}
     *               argument is less than {@code 0}.
     */
    public StringBuffer(int capacity) {
        super(capacity);
    }

    /**
     * Constructs a string buffer initialized to the contents of the
     * specified string. The initial capacity of the string buffer is
     * {@code 16} plus the length of the string argument.
     *
     * @param   str   the initial contents of the buffer.
     */
    public StringBuffer(String str) {
        super(str.length() + 16);
        append(str);
    }

    /**
     * Constructs a string buffer that contains the same characters
     * as the specified {@code CharSequence}. The initial capacity of
     * the string buffer is {@code 16} plus the length of the
     * {@code CharSequence} argument.
     * <p>
     * If the length of the specified {@code CharSequence} is
     * less than or equal to zero, then an empty buffer of capacity
     * {@code 16} is returned.
     *
     * @param      seq   the sequence to copy.
     * @since 1.5
     */
    public StringBuffer(CharSequence seq) {
        this(seq.length() + 16);
        append(seq);
    }
```

약간씩 차이가 있으나, 기본적으로 16 길이로 설정하는 것을 알 수 있으며, 생성자에 String을 직접 넣어주거나 CharSequence를 넣어 생성할 때도 여분으로 16만큼 길이를 설정해 생성하고 있음을 볼 수 있다.

<br><br>

### StringBuffer의 비교 연산

```java
StringBuffer sb = new StringBuffer("abc");
StringBuffer sb2 = new StringBuffer("abc");

System.out.println(sb==sb2);	// false
System.out.println(sb.equals(sb2));	//false
```

StringBuffer클래스는 equals 메서드를 오버라이딩하지 않아 StringBuffer 클래스의 equals 메서드를 사용해도 등가비교연산자(==)로 비교한 것과 같은 결과를 얻는다.

<br><br>

```java
String s = sb.toString();
String s2 = sb2.toString();

System.out.println(s.equals(s2)); // true
```

반면 toString()은 오버라이딩 되어 있어 StringBuffer 인스턴스에 toString()으로 String 타입으로 변환한 뒤, equals() 메서드를 사용해 문자열을 비교해야 한다.

<br><br><br><br>

## StringBuilder

* 싱글쓰레드에 최적화되어 있는 클래스
* 멀티쓰레드를 사용하지 않는 경우 StringBuffer의 동기화가 성능만 떨어뜨리는 문제를 개선
* 메서드는 StringBuffer와 거의 유사



<br><br><br><br>

## StringBuffer, StringBuilder 비교

- 공통점
  - new 연산으로 클래스를 한 번만 만듬 (Mutable)
  - 문자열 연산시 새로 객체를 만들지 않고, 크기를 변경시킴
  - StringBuffer와 StringBuilder 클래스의 메서드가 동일함.
- 차이점
  - StringBuffer는 Thread-Safe함 / StringBuilder는 Thread-safe하지 않음 (불가능)



*StringBuffer 클래스 : 문자열 연산이 많은 Multi-Thread 환경*

*StringBuilder 클래스 : 문자열 연산이 많은 Single-Thread 또는 Thread 신경 안쓰는 환경*

<br><br><br><br>

# Quiz

* String, StringBuffer, StringBuilder 차이?

<br><br><br><br><br><br><br><br><br><br><br><br><br>

# 출처

* [신입 개발자 전공 지식 & 기술 면접 백과사전](https://github.com/gyoogle/tech-interview-for-developer)
* 자바의 정석 -남궁성
* [신입 개발자 면접 준비(2) : 기술면접](https://coding-restaurant.tistory.com/136)



<br><br><br>

# Quiz 답안

* String, StringBuffer, StringBuilder 차이?

<img width="800" alt="스크린샷 2021-04-16 오후 2 02 27" src="https://user-images.githubusercontent.com/46706670/115023441-c3906e80-9ef9-11eb-93f3-4061737857b8.png">