**19일차 주요목차**

- Thread 개념
- Thread 생성 방법
- Thread 동작 원리 :``start()``와 ``run()``
- Multi-Threading

- synchronized(동기화 처리)

-----------

# Thread

> 프로세스 내부의 세부적 실행단위

- 사전적 의미
  - 실 (실이 여러개 모여서 옷을 만든다)
- 프로세스
  - 현재 실행 중인 프로그램
  - 하나의 프로세스는 여러 개의 스레드가 실행되면서 구성될 수 있다
- 멀티 스레드
  - 동시에 여러 서비스를 제공하기 위함
- Thread 별로 Stack 메모리가 생성된다 
  - :point_right: **스레드 별로 지역변수를 별도**로 가지게 된다
- Thread는 우선 순위 방식을 채택 
  - 가장 낮은 우선 순위: 1 / 기본 우선순위: 5 / 가장 높은 우선순위: 10
  - 운영체제별로 우선 순위가 적용되는 여부는 다르므로 참고로 한다
- Thread 의`` setDaemon(true)``
  - 해당 스레드를 실행시킨 **스레드가 종료되면 해당 스레드도 종료**되도록 처리





### 1) 예시 🗝

- 동영상 플레이어가 현재 실행 중이다

- 동영상 서비스를 위해서는 영상서비스(Thread), 음향서비스 (Thread), 자막서비스 (Thread)가 필요함

  :point_right: 이러한 동영상 플레이어 **프로세스 내의 세부적 실행단위를 스레드**라고 한다

  :point_right: 이 스레드들이 동시에 실행되는 것을 **멀티 스레딩**이라고 함



### 2) Thread 생성 방법 2가지

1. extends Thread
2. implements Runnable(-> 상속이 가능해서 더 선호되는 편)





## :one: Thread  동작원리

> ``start()``와 ``run()``

- ``start()``
  - 스레드를 실행가능상태(Runnable) 로 보낸다
  - 이후 JVM이 스케줄링을 해서 실행상태로 전이된다
    - 실제 실행은 jvm이 한다!
- ``run()``
  - 스레드의 실행 내용을 정의한다
  - JVM이 스케줄링을 하면 실행되는 메서드
  - ``run()`` 메서드가 수행을 종료하면 스레드는 종료된다



-------

# 방과후 자습시간 :pencil:



## Daemon Thread란? :thinking:

- 기본적인 daemon의 정의

  - 사용자가 **직접적으로 제어하지 않고**, **백그라운드**에서 돌면서 여러 작업을 하는 프로그램

- 자바의 Daemon Thread

  - 주 스레드의 작업을 돕는 **보조적인 역할**을 수행

  - **주 스레드가 종료되면 데몬 스레드는 강제적으로 자동 종료됨**

    :point_right: 주 스레드의 **보조 역할**을 수행하므로 메인 스레드가 종료되면 **데몬 스레드의 존재 의미가 없어지기 때문**

```java
package step07;
// 문서 작업 스레드가 실행되는 시점에 백업 작업 슬드를 함께 실행시킨다
public class Word implements Runnable{

	@Override
	public void run() {
		// TODO Auto-generated method stub
		try {
			//백업스레드를 생성해서 start 시킨다
			BackupWorker w =  new BackupWorker();
			Thread backThread = new Thread(w);
			//백업스레드를 daemon thread 로 처리해서 현 Word 스레드가 종료되면 함께 종료되도록 한다
			backThread.setDaemon(true);
			backThread.start();
			execute();
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public void execute() throws InterruptedException{
		for(int i=0;i<10;i++) {
			System.out.println("워드문서작업 "+i);
			Thread.sleep(1000);
		}
	}
	
}

```

```java
package step07;
//DaemonThread Test 예제
////백업스레드를 daemon thread 로 처리해서 현 Word 스레드가 종료되면 함께 종료되도록 한다
//backThread.setDaemon(true);
public class TestThread7 {
	public static void main(String[] args) {
		Thread t = new Thread(new Word());
		t.start();
	}
}

```

```java
package step07;

public class BackupWorker implements Runnable {

	@Override
	public void run() {
		while (true) {
			// TODO Auto-generated method stub
			try {
				backup();
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}

	public void backup() throws InterruptedException {
		Thread.sleep(3000);// 3초간격으로 백업
		System.out.println("백업스레드가 워드문서를 백업처리");
	}
}

```

결과창

```java
워드문서작업 0
워드문서작업 1
워드문서작업 2
백업스레드가 워드문서를 백업처리
워드문서작업 3
워드문서작업 4
워드문서작업 5
백업스레드가 워드문서를 백업처리
워드문서작업 6
워드문서작업 7
워드문서작업 8
백업스레드가 워드문서를 백업처리
워드문서작업 9
```

:point_right: ``setDaemon(true)`` 가 있으면 워드문서작업이 종료되면 ``BackupWorker``도 같이 종료되게 할 수 있음



## InterruptedException ? :thinking:

- `InterruptedException`은 자바 스레드의 **인터럽트 메커니즘의 일부**

- 스레드에 **하던 일을 멈추라는 신호**를 보내기 위해 인터럽트를 사용

  - 한 스레드가 **다른 스레드를 인터럽트 할 수 있음**
  - 각 스레드는 자신이 인터럽트 되었는지 **확인 할 수 있음**
  - 스레드가 **자기 자신을 인터럽트** 할 수 있음

  ❗️ Interrupted Thread 에서는 이를 어떻게 처리해야 한다는 **규칙 :x:**

  ❗️ 대부분의 경우 인터럽트는 **하던 일을 멈추라는 신호**

  ​	:point_right: 해당 스레드는 이를 **적절히 처리**해야 함

###  Thread 를 Interrupt 하고싶다면:question:

- 대상 스레드의 ``Thread.interrupt()`` 메서드 호출

  :point_right: 현재 스레드가 대상 스레드를 수정할 수 있는 권한이 없다면 ``SecurityException``발생

  :point_right: 대상 스레드가 `Object.wait()`, `Thread.sleep()`, `Thread.join()`, `Future.get(), BlockingQueue.take()` 등의 메서드에 의해 블로킹된 경우, **interrupt state가 사라지고** **`InterruptedException`이 발생**

  :point_right: 대상 스레드가 [InterruptibleChannel](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/InterruptibleChannel.html)을 이용한 I/O 작업에 의해 블로킹된 경우, **interrupt state가 설정되고** [ClosedByInterruptException](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/ClosedByInterruptException.html)이 발생

  :point_right: 대상 스레드가 [Selector](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/Selector.html)에서 블로킹된 경우, **interrupt state가 설정되고 selection 작업에서 리턴**

  :point_right: 이외의 경우에는 **interrupt state가 설정**



**interrupt state는 대상 스레드가 자신이 인터럽트 되었는지 확인할 수 있는 상태 값**

#### 상태 값 확인 방법

1. [Thread.interrupted()](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#interrupted--)
   - 정적 메서드
   - 호출 후에 ``interrupt state`` 사라짐
2. [Thread.isInterrupted()](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#isInterrupted--) 
   - 인스턴스 메서드
   - 호출 후에도 ``interrupt state``는 유지됨

:point_right: 스레드는 자신이 인터럽트 되었는지 확인하는 방법 2가지

	1. interrupt state 설정 확인
	2.  ``InterruptedException`` 발생 확인

- 멀티스레드로 동작하는 코드에 무한 루프 혹은 `InterruptedException`을 던지는 **메서드 호출이 존재**한다면, 아래 코드를 관용구처럼 사용하자.

```java
while (!Thread.currentThread().isInterrupted()) {
  try {
    // Thread.sleep(), Future.get(),
    // BlockingQueue.take() 등이 여기올 수 있다.
  } catch (InterruptedException ex) {
    Thread.currentThread().interrupt();
  }
}
```

http://happinessoncode.com/2017/10/09/java-thread-interrupt/(참고자료)

(또 궁금해서 찾아봄)





## 함수와 메서드의 차이?:thinking:

- ### 함수

  - 특정 작업을 수행하는 코드조각
  - 전역, 지역 상관없이 독립된 기능을 수행하는 단위
  - 함수는 메소드를 포함
  - 함수의 길이와는 상관없이 하나의 기능
  - 함수로 구현된 기능은 필요한 여러곳에서 호출되어서 사용
  - 재사용이 가능하고, 기능이 분리되어서 작성

  

- ### 메소드

  - 객체의 기능을 구현하기 위해 클래스 내부에서 구현되는 함수
  - 클래스, 구조체, 열거형 **내부에 작성**되어있는 함수를 메소드라고 한다
  - 메소드 = 클래스 함수
  - 메소드 구현 = 객체의 기능 구현
  - 메소드 이름 = 클라이언트 코드에 맞게 명명하기



## currentThread()? :thinking:

```
 /**
     * A hint to the scheduler that the current thread is willing to yield
     * its current use of a processor. The scheduler is free to ignore this
     * hint.
     *
     * <p> Yield is a heuristic attempt to improve relative progression
     * between threads that would otherwise over-utilise a CPU. Its use
     * should be combined with detailed profiling and benchmarking to
     * ensure that it actually has the desired effect.
     *
     * <p> It is rarely appropriate to use this method. It may be useful
     * for debugging or testing purposes, where it may help to reproduce
     * bugs due to race conditions. It may also be useful when designing
     * concurrency control constructs such as the ones in the
     * {@link java.util.concurrent.locks} package.
     */
```

- 현재 스레드가 프로세서의 현재 사용을 양보할 의사가 있음을 스케줄러에 암시합니다. 

- 스케줄러는 이 힌트를 무시해도 됩니다.

  

-> 아 주로 디버깅이나 테스팅 환경에서 사용되고 실제로 사용되는 일이 많지는 않구나..

사용된다면 세부적으로 프로파일링되었거나 원하는 영향을 확실하게 벤치마킹 할 수 있는 상황에서 사용되어야 하는듯!

### 접근제어자 차이!

![image-20210824203753987](C:\Users\MIN\TIL\JAVA\KOSTA_0824.assets\image-20210824203753987.png)
