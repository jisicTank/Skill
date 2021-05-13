## Call by Value와 Call by Reference

---

<br><br>

### Call by Value

* 함수 호출 시 전달되는 변수 값을 복사해서 함수 인자로 전달하는 방법
* 이때 복사된 인자는 함수 안에서 지역적으로 사용되기 때문에 Local Value 속성을 가짐
* 따라서, 함수 안에서 인자 값이 변경되더라도, 외부 변수 값은 변경되지 않음

<br><br>

### Call by Reference

* 함수 호출 시 인자로 전달되는 변수의 레퍼런스를 전달함
* 따라서, 함수 안에서 인자 값이 변경되면, 전달된 객체의 값도 변경됌

<br><br>

### Java의 함수 호출 방식

* 항상 Call by Value로 함수를 호출함
* Reference Type(참조 자료형)을 넘길 때는 해당 객체의 주소값을 복사해 이를 가지고 사용함
* 따라서 원본 객체의 프로퍼티까지는 접근이 가능하지만, 원본 객체 자체를 변경할 수는 없음

<br><br>

### Java Call by Value 예시

```java
public class Test {
	
	public static void swap(int x, int y) {
		int temp = x;
		x = y;
		y = temp;
		}

	public static void main(String[] args) {
		int a = 10;
		int b = 20;

		System.out.println("swap() 호출 전 : a = " + a + ", b = " + b);
		swap(a, b);
		System.out.println("swap() 호출 후 : a = " + a + ", b = " + b);
	}
}
```

a, b 변수가 swap 함수를 호출한 후, 서로 값이 바꼈을 거라 기대할 수 있지만, 결과는 그렇지 않다.

```
swap() 호출 전 : a = 10, b = 20
swap() 호출 후 : a = 10, b = 20
```

<br><br>

메모리 구조 상에서 이를 자세히 보면 아래와 같다.

<img width="543" alt="스크린샷 2021-04-16 오전 11 42 13" src="https://user-images.githubusercontent.com/46706670/115022753-c9398480-9ef8-11eb-8463-094f7538bcac.png">

main함수에서 swap 함수를 호출할 때, 변수 x, y가 a, b의 값을 각각 복사해서 갖고 있게 되고, 서로 값 교환을 수행하게 된다. 그러나 이는 swap 함수 내에서 사용되는 x, y에만 적용되고 swap함수가 종료된 후에도 a, b는 값 변경 없이 그대로 10, 20을 갖고 있다.

<br><br>

> 직접 값을 가지고 있는 primitive type이라 그런가?, Reference Type은 다르지 않을까?



```java
public class Test {
	
	public static void swap(String x, String y) {
		String temp = x;
		x = y;
		y = temp;
		}

	public static void main(String[] args) {
		String a = "Red";
		String b = "Blue";

		System.out.println("swap() 호출 전 : a = " + a + ", b = " + b);
		swap(a, b);
		System.out.println("swap() 호출 후 : a = " + a + ", b = " + b);
	}
}
```

int로 테스트했던 코드와 동일하되, 변수 타입만 String으로 변경했다. (String은 Reference Type)



```
swap() 호출 전 : a = Red, b = Blue
swap() 호출 후 : a = Red, b = Blue
```

<br><br>

이 또한 메모리 구조를 살펴보면 다음과 같다.

<img width="635" alt="스크린샷 2021-04-16 오전 11 53 12" src="https://user-images.githubusercontent.com/46706670/115022928-0a319900-9ef9-11eb-88e8-70b226fd87d2.png">

초기 main 함수의 변수인 a, b가 각각 Red, Blue의 주소값을 가지고 있을 때, swap()을 호출하면 x, y는 각각 a, b가 갖고 있던 주소값인 Red와 Blue를 가리키는 주소값을 복사한다. (주소<u>**값**</u>을 복사한다는 것에 주의) 

<br><br>

<img width="649" alt="스크린샷 2021-04-16 오전 11 53 33" src="https://user-images.githubusercontent.com/46706670/115022938-0bfb5c80-9ef9-11eb-8b3e-3e092e03949e.png">

이후 swap함수에서 변경이 일어나면 x, y가 각각 가리키는 주소값 교환만 일어날 뿐 a, b가 갖고 있는 주소값에는 변동이 없다. 

<br><br>

<img width="641" alt="스크린샷 2021-04-16 오전 11 59 11" src="https://user-images.githubusercontent.com/46706670/115023063-3ea55500-9ef9-11eb-841a-3568516af3e9.png">

이 상태에서, swap()이 끝나고 main()으로 돌아오면 여전히 a, b 는 각각 Red, Blue를 가리키고 있다. 교환이 일어나지 않은 것이다. 이는 x, y가 각각 주소값을 복사하는 Call by Value 방식으로 swap()함수가 호출됐기 때문이다. 

<br>

만약 Call by Reference 방식으로 동작한다면, x와 y는 각각 a, b의 주소값을 받아 x = a, y = b 이고 swap 안에서 값이 바뀌므로 수행된 이후에도 a, b가 바뀌어 있을 것이다. 주소값을 그대로 호출하는 것은 C/C++ 에서 포인터가 존재했기에 가능하지만 Java에서는 이를 그대로 구현하는 것이 불가능하다.

<br>

그러나, 이와 유사하게 효과를 내는 방법은 있다.

```java
public class Test {
	int value;
	
	public Test(int value) {
		this.value = value;
	}

	public static void swap(Test x, Test y) {
		int temp = x.value;
		x.value = y.value;
		y.value = temp;
		}

	public static void main(String[] args) {
		Test a = new Test(10);
		Test b = new Test(20);

		System.out.println("swap() 호출 전 : a = " + a.value + ", b = " + b.value);
		swap(a, b);
		System.out.println("swap() 호출 후 : a = " + a.value + ", b = " + b.value);
	}
}
```

```
swap() 호출 전 : a = 10, b = 20
swap() 호출 후 : a = 20, b = 10
```

이번에는 값이 교환된 것을 볼 수 있다. 

<br><br>

<img width="543" alt="스크린샷 2021-04-16 오후 12 08 49" src="https://user-images.githubusercontent.com/46706670/115023078-41a04580-9ef9-11eb-81d9-08c80ee3782d.png">

<img width="559" alt="스크린샷 2021-04-16 오후 12 08 57" src="https://user-images.githubusercontent.com/46706670/115023123-5086f800-9ef9-11eb-80ca-97d759a1c568.png">

<img width="567" alt="스크린샷 2021-04-16 오후 12 09 09" src="https://user-images.githubusercontent.com/46706670/115023129-52e95200-9ef9-11eb-80d0-70b3b398f71b.png">

Heap area에 있는 값 자체를 바꿔서 마치 call by reference가 이뤄진 것처럼 보이게 하는 것이다.

<br><br><br><br>

### 정리

* Call by Value? 값에 의한 호출

* Call by Reference? 레퍼런스에 의한 호출

**Call by value**의 경우, 데이터 값을 복사해서 함수로 전달하기 때문에 **원본의 데이터가 변경될 가능성이 없다.** 하지만 **인자를 넘겨줄 때마다 메모리 공간을 할당해야해서(Stack) 메모리 공간을 더 잡아먹는다.**

**Call by reference**의 경우 메모리 공간 할당 문제는 해결했지만, **원본 값이 변경될 수 있다는 위험이 존재**한다.

<br><br><br><br>

## Quiz

* Call by Reference, Call by Value의 차이점은?

<br><br><br><br><br><br><br><br><br><br><br>

## 출처

* [신입 개발자 전공 지식 & 기술 면접 백과사전](https://github.com/gyoogle/tech-interview-for-developer)
* [Call by value와 Call by reference](https://re-build.tistory.com/3)
* [자바 Call by value Call by reference](https://sleepyeyes.tistory.com/11)

<br><br><br><br><br><br><br><br><br><br><br>

## Qiuz 답안

* Call by Reference, Call by Value의 차이점은?

Call by Value = 값에 의한 호출
Call by Reference? 레퍼런스에 의한 호출

**Call by value**의 경우, 데이터 값을 복사해서 함수로 전달하기 때문에 **원본의 데이터가 변경될 가능성이 없다.** 하지만 **인자를 넘겨줄 때마다 메모리 공간을 할당해야해서(Stack) 메모리 공간을 더 잡아먹는다.**

**Call by reference**의 경우 메모리 공간 할당 문제는 해결했지만, **원본 값이 변경될 수 있다는 위험이 존재**한다.