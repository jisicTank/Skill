# Java에서의 Thread



## Process

* 실행 중인 프로그램
* OS로부터 실행에 필요한 자원(메모리)를 할당받아 프로세스가 된다.

## Thread

* 프로세스의 자원을 이용해서 실제로 작업을 수행하는 것
* 모든 프로세스에는 최소한 하나 이상의 쓰레드가 존재
* 둘 이상의 쓰레드를 가진 프로세스를 `멀티쓰레드 프로세스`라고 한다.



요즘 OS는 모두 멀티태스킹을 지원한다.

도스와 같은 OS는 한 번에 한 가지 작업만 할 수 있었지만, Windows, Mac 등은 멀티태스킹을 지원해 동시에 여러 작업을 수행할 수 있다. 싱글쓰레드 프로그램과 멀티쓰레드 프로그램도 이와 같다.



## 멀티 쓰레딩과 멀티 프로세스

|      | 멀티 쓰레드                                                  | 멀티 프로세스                                      |
| ---- | ------------------------------------------------------------ | -------------------------------------------------- |
| 특징 | * CPU의 사용률을 향상시킨다.<br />* 자원을 보다 효율적으로 사용할 수 있다.<br />* 사용자에 대한 응답성이 향상된다.<br />* 작업이 분리되어 코드가 간결해진다. | * 동기화, 교착상태 문제를 원천적으로 피할 수 있다. |



메신저로 채팅하면서 파일을 다운로드 받거나 음성대화를 나눌 수 있는 것이 가능한 이유는 바로 멀티쓰레드로 작성되어 있기 때문이다. 만일 싱글쓰레드로 작성되어 있다면 파일을 다운로드 받는 동안에는 다른 일을 할 수 없다. 여러 사용자에게 서비스를 해주는 서버 프로그램의 경우 멀티쓰레드로 작성하는 것은 필수적이어서 하나의 서버 프로세스가 여러 개의 쓰레드를 생성해서 쓰레드와 사용자의 요청이 일대일로 처리되도록 프로그래밍해야 한다.

만약 싱글쓰레드로 서버 프로그램을 작성한다면 사용자의 요청마다 새로운 프로세스를 생성해야 한다. **<u>프로세스를 생성하는 것은 쓰레드를 생성하는 것에 비해 더 많은 시간과 메모리 공간이 필요</u>**하기 때문에 많은 수의 사용자 요청을 서비스하기 어렵다.

그러나 멀티쓰레드 프로세스는 프로세스 내 자원을 공유하면서 작업을 하기 때문에 발생할 수 있는 **<u>동기화(Synchronization), 교착상태(DeadLock)와 같은 문제</u>**들을 고려해 신중히 프로그래밍해야 한다.

> * Thread는 경량 프로세스(LWP, Light-Weight Process)라고 부르기도 한다.



## Thread 구현과 실행

Thread를 구현하는 방법은 2가지가 있다.

* Thread 클래스를 상속받는 방법
* Runnable 인터페이스를 구현하는 방법

어느 쪽을 선택해도 별 차이는 없으나, Thread 클래스를 상속받으면 다른 클래스를 상속받을 수 없기 때문에, Runnable 인터페이스를 구현하는 방법이 일반적이다.



* Thread 생성

```java
class MyThread extends Thread{
  public void run(){/* 작업 내용 */}	// Thread 클래스의 run()을 오버라이딩
}
```



```java
class MyThread implements Runnable{
  public void run(){/* 작업 내용 */}	// Runnable 인터페이스의 run()을 구현
}
```





* Thread 실행

```java
public class Thread1 {
	
	public static void main(String[] args) {
		// t1(ThreadExtends) 생성 
		ThreadExtends t1 = new ThreadExtends();
		
		// t2(ThreadImplements) 생성
		Runnable r = new ThreadImplements();
		Thread t2 = new Thread(r);
		
		t1.start();
		t2.start();
	}
}

class ThreadExtends extends Thread{
	@Override
	public void run() {
		for(int i =0; i< 5; i++) {
			// 조상인 Thread의 getName()을 호출 
			System.out.println(getName());
		}
	}
}

class ThreadImplements implements Runnable{
	@Override
	public void run() {
		for(int i =0; i< 5; i++) {
			// Thread.currentThread() - 현재 실행중인 Thread를 반환 
			System.out.println(Thread.currentThread().getName());
		}
	}
}
```



한 번 실행이 종료된 쓰레드는 다시 실행할 수 없다. 하나의 쓰레드에 대해 start()가 한 번만 호출될 수 있다는 뜻이다. 그래서 만일 쓰레드의 작업을 한 번 더 수행해야 한다면 아래와 같이 새로운 쓰레드를 생성한 다음에 start()를 호출해야 한다. 

```java
ThreadEx1_1 t1 = new ThreadEx1_1();
t1.start();
t1.start();	// 예외 발생!!! IllegalThreadStateException
```

```java
ThreadEx1_1 t1 = new ThreadEx1_1();
t1.start();
t1 = new ThreadEx1_1();	// 다시 생성
t1.start();	// OK
```



## start()와 run()

> 왜 기껏 run() 메소드에 코드를 작성하고 실행은 start()로 할까..?

run()으로 작업 지시를 하면 실행되지 않을까? 그렇지 않다. 두 메소드 모두 같은 작업을 한다. 하지만 run() 메소드를 사용한다면, 의도대로 쓰레드를 사용하는 것이 아니다.

![스크린샷 2021-04-09 오전 1.21.42]($md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-09%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.21.42.png)

main 메서드에서 run()을 호출하는 것은 생성된 쓰레드를 실행시키는 것이 아니라 단순히 클래스에 선언된 메서드를 호출하는 것일 뿐이다.

반면에 start()는 새로운 쓰레드가 작업을 실행하는데 필요한 호출스택(call stack)을 생성한 다음에 run()을 호출해서, 생성된 호출스택에 run()이 첫 번째로 올라가게 한다.



![스크린샷 2021-04-09 오전 1.27.12]($md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-09%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.27.12.png)

1. main 메서드에서 쓰레드의 start()를 호출한다.
2. start()는 새로운 쓰레드를 생성하고, 쓰레드가 작업하는데 사용될 호출스택을 생성한다.
3. 새로 생성된 호출스택에 run()이 호출되어, 쓰레드가 독립된 공간에서 작업을 수행한다.
4. 이제는 호출스택이 2개이므로 스케줄러가 정한 순서에 의해서 번갈아 가면서 실행된다.

> 사실은 start()가 호출되었다고 해서 바로 실행되는 것이 아니라, 일단 실행대기 상태에 있다가 자신의 차례가 되어야 실행된다. 물론 실행대기중인 쓰레드가 하나도 없으면 곧바로 실행 상태가 된다.
>
> 쓰레드의 실행순서는 OS의 스케쥴러가 작성한 스케쥴에 의해 결정된다.
> (쓰레드의 상태는 뒤에 자세히 서술한다.)



## 싱글쓰레드와 멀티쓰레드



![스크린샷 2021-04-09 오전 1.54.16]($md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-09%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.54.16.png)

싱글코어 상황에서 비교해보면, 하나의 쓰레드로 두 개의 작업을 수행하거나, 두 개의 쓰레드로 두 개의 작업을 수행한 경우의 소요시간이 거의 유사하다. 오히려 두 개의 쓰레드를 사용한 시간이 더 걸리는데 이유는 **쓰레드 간의 작업 전환(Context Switching)**에 시간이 걸리기 때문이다.

작업 전환을 할 때는 진행 중인 작업의 상태, 다음에 실행해야할 위치(PC: 프로그램 카운터) 등의 정보를 저장하고 읽어 오는 시간이 소요된다. 물론 프로세스 스위칭이 더 많은 정보를 저장해야하므로 더 많이 소요되지만 쓰레드도 시간 소요를 피할 수는 없다.



## 쓰레드의 상태와 실행제어

### 쓰레드의 상태

|         상태          |                             설명                             |
| :-------------------: | :----------------------------------------------------------: |
|          NEW          |     쓰레드가 생성되고 아직 start()가 호출되지 않은 상태      |
|       RUNNABLE        |                실행 중 또는 실행 가능한 상태                 |
|        BLOCKED        | 동기화블럭에 의해서 일시정지된 상태(lock이 풀릴 때까지 기다리는 상태) |
| WATING, TIMED_WAITING | 쓰레드의 작업이 종료되지는 않았지만 실행가능하지 않은(unrunnable) 일시정지 상태. TIMED_WATING은 일시정지 시간이 지정된 경우를 의미 |
|      TERMINATED       |                 쓰레드의 작업이 종료된 상태                  |



![스크린샷 2021-04-09 오전 2.16.25]($md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-09%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.16.25.png)

1. 쓰레드를 생성하고 start()를 호출하면 바로 실행되는 것이 아니라 실행대기열에 저장되어 자신의 차례가 될 때까지 기다린다. 실행대기열은 큐와 같은 구조로 먼저 실행대기열에 들어온 쓰레드가 먼저 실행된다.
2. 실행대기상태에 있다가 자신의 차례가 되면 실행상태가 된다.
3. 주어진 실행시간이 다되거나 yield()를 만나면 다시 실행대기 상태가 되고 다음 차례의 쓰레드가 실행상태가 된다.
4. 실행 중에 suspend(), sleep(), wait(), join(), I/O block에 의해 일시정지상태가 될 수 있다. I/O block은 입출력작업에서 발생하는 지연상태를 말한다. 사용자의 입력을 기다리는 경우를 예로 들ㅇ 수 있는데, 이런 경우 일시정지 상태에 있다가 사용자가 입력을 마치면 다시 실행대기상태가 된다.
5. 지정된 일시정지 시간이 다되거나, notify(), resume(), interrupt()가 호출되면 일시정지상태를 벗어나 다시 실행대기열에 저장되어 자신의 차례를 기다리게 된다.
6. 실행을 모두 마치거나 stop()이 호출되면 쓰레드는 소멸된다.



### 쓰레드의 실행제어

쓰레드 프로그래밍이 어려운 이유는 동기화(Synchronization)와 스케줄링(Scheduling) 때문이다. 효율적인 멀티쓰레드 프로그램을 개발하기 위해서는 보다 정교한 스케쥴링을 통해 프로세스에 주어진 자원과 시간을 여러 쓰레드가 낭비없이 잘 사용하도록 프로그래밍 해야 한다.

| Methods                                                      | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| static void sleep(long millis)<br />static void sleep(long millis, int nanos) | 지정된 시간(천 분의 일 초 단위)동안 쓰레드를 일시정지시킨다. 지정한 시간이 지나고 나면, 자동적으로 다시 실행대기상태가 된다. |
| void join()<br />void join(long millis)<br />void join(long millis, int nanos) | 지정된 시간동안 쓰레드가 실행되도록 한다. 지정된 시간이 지나거나 작업이 종료되면 join()을 호출한 쓰레드로 다시 돌아와 실행을 계속한다. |
| void interrupt()                                             | sleep()이나 join()에 의해 일시정지상태인 쓰레드를 깨워서 실행대기상태로 만든다. 해당 쓰레드에서는 Interrupted Exception이 발생함으로써 일시정지상태를 벗어나게 된다. |
| void stop()                                                  | 쓰레드를 즉시 종료시킨다.                                    |
| void suspend()                                               | 쓰레드를 일시정지시킨다. resume()을 호출하면 다시 실행대기상태가 된다. |
| void resume()                                                | suspend()에 의해 일시정지상태에 있는 쓰레드를 실행대기상태로 만든다. |
| static void yield()                                          | 실행 중에 자신에게 주어진 실행시간을 다른 쓰레드에게 양보하고 자신은 실행대기상태가 된다. |

> stop(), resume(), suspend()는 쓰레드를 교착상태(DeadLock)로 만들기 쉬워 deprecated됐다.



## 쓰레드의 동기화(Synchronization)

* **<u>한 쓰레드가 진행중인 작업을 다른 쓰레드가 간섭하지 못하게 막는 것</u>**
* `임계 영역(Critical Section)`과 `잠금(Lock)`

멀티쓰레드 프로세스의 경우 여러 쓰레드가 같은 프로세스 내의 자원을 공유해서 작업하기 때문에 서로의 작업에 영향을 주게 된다. 만일 쓰레드A가 작업하던 도중에 다른 쓰레드B에게 제어권이 넘어갔을 때, 쓰레드 A가 작업하던 공유데이터를 쓰레드B가 임의로 변경했다면, 다시 쓰레드A가 제어권을 받아서 나머지 작업을 마쳤을 때 원래 의도했던 것과 다른 결과를 얻을 수 있다.

이런 일이 발생하는 것을 방지하기 위해 한 쓰레드가 특정 작업을 끝마치기 전까지 다른 쓰레드에 의해 방해받지 않도록 하는 것이 필요하다. 그래서 도입된 개념이 바로 `임계영역(Critical Section)`과 `잠금(Lock)`이다.

**<u>공유 데이터를 사용하는 코드 영역을 임계 영역으로 지정</u>**해놓고, **<u>공유 데이터(객체)가 가지고 있는 Lock을 획득한 단 하나의 쓰레드만 이 영역 내의 코드를 수행</u>**할 수 있게 한다. 그리고 해당 쓰레드가 임계 영역 내의 모든 코드를 수행하고 벗어나서 lock을 반납해야만 다른 쓰레드가 반납된 lock을 획득하여 임계 영역의 코드를 수행할 수 있게 된다.

Java에서는 `synchronized`블럭을 이용해 쓰레드의 동기화를 지원했지만 JDK1.5부터는 `java.util.concurrent.locks`와 `java.util.concurrent.atomic`패키지를 통해 다양한 방식으로 동기화를 구현할 수 있도록 지원한다.



가장 간단한 동기화 방법: synchronized 키워드

```java
// 1. 메서드 전체를 임계 영역으로 지정
public synchronized void calcSum(){
  /**/
}

// 2. 특정한 영역을 임계 영역으로 지정
synchronized(){
  /**/
}
```



* **첫 번째 방법은 메서드 앞에 `synchronized`를 붙이는 것, 메서드 전체가 임계 영역으로 설정된다.**

  쓰레드는 synchronized 메서드가 호출된 시점부터 해당 메서드가 포함된 객체의 lock을 얻어 작업을 수행하고, 메서드가 종료되면 lock을 반환한다.

* **두 번째 방법은 메서드 내의 코드 일부를 블럭{}으로 감싸고 블럭 앞에 `synchronized(참조변수)`를 붙이는 것**
  이때 참조변수는 락을 걸고자 하는 객체를 참조하는 것이어야 한다. 이 블럭을 synchronized블럭이라 하며, 이 블럭의 영역 안으로 들어가면서부터 쓰레드는 지정된 객체의 lock을 얻게 되고, 이 블럭을 벗어나면 lock을 반납한다.

* 모든 객체는 lock을 하나씩 가지고 있으며, 해당 객체의 lock을 가지고 있는 쓰레드만 임계 영역의 코드를 수행할 수 있다.

* **임계 영역은 멀티쓰레드 프로그램의 성능을 좌우하기 때문에 가능하면 메서드 전체에 락을 거는 것보다 synchronized 블럭으로 임계 영역을 최소화해서 보다 효율적인 프로그램이 되도록 해야 한다.**



```java
public class SynchronizedEx {

	public static void main(String[] args) {
		Runnable r = new RunnableEx();
		new Thread(r).start();
		new Thread(r).start();
	}

}
class Account{
	private int balance = 1000;
	
	public int getBalance() {
		return balance;
	}
	
	public void withdraw(int money) {
		if(balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			
			balance -= money;
		}
	}
}

class RunnableEx implements Runnable{
	Account acc = new Account();
	
	public void run() {
		while(acc.getBalance() > 0) {
			// 100, 200, 300 중 임의의 한 값을 선택해서 출금 
			int money = (int)(Math.random() * 3 + 1) * 100;
			acc.withdraw(money);
			System.out.println("balance:"+acc.getBalance());
		}
	}
}
```

> 실행결과
>
> balance:500
> balance:500
> balance:300
> balance:300
> balance:100
> balance:-100

반드시 출금하려는 금액보다 많은 상황에서만 출금하도록 했지만 음수가 출력된 것을 보면 의도대로 작동하지 않았다. 쓰레드 2개 중 하나가 if문을 통과한 이후 출금을 하기 전 사이에 다른 쓰레드가 출금을 했기 때문이다.



```java
public class SynchronizedEx2 {

	public static void main(String[] args) {
		Runnable r = new RunnableEx2();
		new Thread(r).start();
		new Thread(r).start();
	}

}
class Account2{
	private int balance = 1000;
	
	public int getBalance() {
		return balance;
	}
	
	public synchronized void withdraw(int money) {
		if(balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			
			balance -= money;
		}
	}
}

class RunnableEx2 implements Runnable{
	Account acc = new Account();
	
	public void run() {
		while(acc.getBalance() > 0) {
			// 100, 200, 300 중 임의의 한 값을 선택해서 출금 
			int money = (int)(Math.random() * 3 + 1) * 100;
			acc.withdraw(money);
			System.out.println("balance:"+acc.getBalance());
		}
	}
}
```

> 실행결과
>
> balance:600
> balance:600
> balance:300
> balance:300
> balance:100
> balance:0

이처럼 출금 메서드에 synchronized 만 붙이면 문제를 해결할 수 있다.

<br><br>

>Thread 동기화 방법
>
>- 임계 영역(critical section) : 공유 자원에 단 하나의 스레드만 접근하도록(하나의 프로세스에 속한 스레드만 가능)
>- 뮤텍스(mutex) : 공유 자원에 단 하나의 스레드만 접근하도록(서로 다른 프로세스에 속한 스레드도 가능)
>- 이벤트(event) : 특정한 사건 발생을 다른 스레드에게 알림
>- 세마포어(semaphore) : 한정된 개수의 자원을 여러 스레드가 사용하려고 할 때 접근 제한
>- 대기 가능 타이머(waitable timer) : 특정 시간이 되면 대기 중이던 스레드 깨움



### wait()와 notify()

---

synchronized로 동기화해 공유 데이터를 보호하는 것 까지는 좋은데 특정 쓰레드가 객체의 락을 가진 상태로 오랜 시간을 보내지 않도록 하는 것도 중요하다. 이러한 상황을 개선하기 위해 고안된 것이 바로 `wait()`와 `notify()`이다.

**임계 영역에서 코드를 수행하다가 작업을 더 이상 진행할 상황이 아니면, 일단 wait()을 호출**해 쓰레드가 락을 반납하고 기다리게한다. 그러면 다른 쓰레드가 락을 얻어 해당 객체에 대한 작업을 수행할 수 있게 된다. **나중에 작업을 진행할 수 있는 상황이 되면 notify()를 호출**해, 작업을 중단했던 쓰레드가 다시 락을 얻어 작업을 진행할 수 있게 한다.

이 두 메소드는 동기화 된 영역(임계 영역)내에서 사용되어야 한다.

동기화 처리한 메소드들이 반복문에서 활용된다면, 의도한대로 결과가 나오지 않는다. 이때 wait()과 notify()를 try-catch 문에서 적절히 활용해 해결할 수 있다.

```java
/**
* 스레드 동기화 중 협력관계 처리작업 : wait() notify()
* 스레드 간 협력 작업 강화
*/

public synchronized void makeBread(){
    if (breadCount >= 10){
        try {
            System.out.println("빵 생산 초과");
            wait();    // Thread를 Not Runnable 상태로 전환
        } catch (Exception e) {

        }
    }
    breadCount++;    // 빵 생산
    System.out.println("빵을 만듦. 총 " + breadCount + "개");
    notify();    // Thread를 Runnable 상태로 전환
}

public synchronized void eatBread(){
    if (breadCount < 1){
        try {
            System.out.println("빵이 없어 기다림");
            wait();
        } catch (Exception e) {

        }
    }
    breadCount--;
    System.out.println("빵을 먹음. 총 " + breadCount + "개");
    notify();
}
```

조건 만족 안할 시 wait(), 만족 시 notify()를 받아 수행한다.

<br><br><br><br><br><br><br>

# Quiz

* **Thread와 Process의 차이점은 무엇입니까?**
* **Multi-Thread의 장단점은 무엇입니까?**

<br><br><br><br><br><br><br><br><br><br><br><br>

# 참고 자료

* [신입 개발자 전공 지식 & 기술 면접 백과사전 - 자바에서의 Thread](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Java%EC%97%90%EC%84%9C%EC%9D%98%20Thread.md)
* 자바의 정석 - 남궁성
* [신입개발자 기술면접 #1 - Java 질문 모음](https://sas-study.tistory.com/53)

# Quiz 답안

* **Thread와 Process의 차이점은 무엇입니까?**

여러 분야에서 ‘과정’ 또는 ‘처리’라는 뜻으로 사용되는 용어로 컴퓨터 분야에서는 ‘실행중인 프로그램’이라는 뜻으로 쓰인다. 이 프로세스 내에서 실행되는 각각의 일을 스레드라고 한다. 프로세스 내에서 실행되는 세부 작업 단위로 여러 개의 스레드가 하나의 프로세스를 이루게 되는 것이다.





* **Multi-Thread의 장단점은 무엇입니까?**

![스크린샷 2021-04-09 오후 2.21.00]($md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-09%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.21.00.png)