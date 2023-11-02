# 🙄 Thread

## Thred 란?

- 프로세스보다 더 작은 단위로, 한 개 이상의 스레드가 작동해야 프로세스가 작동한다.
- Java는 보통 한 개의 스레드, 프로세스만 사용하며 한 개의 작업이 실행되는 동안 다른 작업의 실행은 할 수 없다.
  - 이를 해결하기 위해 JAVA는 Thread를 활용하여 여러개의 기능을 동시에 사용할 수 있다.

<br>

## Thread 사용 방법

1. Thread 상속 받기
   - Thread는 언제든지 상속이 가능하며, 이를 위해 run이라는 메서드가 필요하다.

```java
public class ThreadEx {
    public static void main(String[] args){
        ThreadEx1 th = new ThreadEx1();

        th.start();
    }
}
class ThreadEx1 extends Thread{
    @Override
    public void run(){
        for(int i=0;i<10;i++){
            System.out.println(getName());
        }
    }
}
```

<br>

2. Runnable을 implements 하기
   - Runnable이란, Thread를 상속받고 있는 Class이며, 스레드를 사용할 수 있게 도와준다.

```java
public class ThreadEx {
    public static void main(String[] args){
        Runnable r = new ThreadEx2();
        Thread th = new Thread(r);

        th.start();
    }
}
class ThreadEx2 implements Runnable{
    @Override
    public void run(){
        for(int i=0;i<10;i++){
            System.out.println(Thread.currentThread().getName());
        }
    }
}

```

> 보통 2번 방법을 선호하는데 JAVA의 extends는 하나만 가능하기 때문에 <br>
> Thread를 사용하기 위해 이 한 번의 상속을 사용한다면 기능에 제한이 생기기 때문이다.

<br>

## 동기화

    여러 스레드가 같은 프로세스 내의 자원을 공유하면서 작업할 때
    서로의 작업이 다른 작업에 영향을 주기 때문에 동기화가 필수적!!

### Synchronized 활용

- 서로 다른 두 객체가 동기화를 하지 않은 메소드를 같이 오버라이딩해서 이용하면, 두 스레드가 동시에 진행되므로 원하는 출력 값을 얻지 못한다.
- 오버라이딩 되는 부모 클래스의 메소드에 synchronized 키워드로 임계영역을 설정하면 된다.
- sleep 사용 -> Running 상태에서 Runnable 상태로

```java
public synchronized void saveMoney(int save){
    int m = money;
    try{
        Thread.sleep(2000); // 지연시간 2초
    } catch (Exception e){}
    money = m + save;
}

public synchronized void minusMoney(int minus){
    int m = money;
    try{
        Thread.sleep(3000); // 지연시간 3초
    } catch (Exception e){}
    money = m - minus;
}

```

<br>

### wait() & notify()

- 스레드가 서로 협력관계일 경우 위처럼 무작정 대기시키는 것은 올바르지 않은 방법이므로 wait과 notify를 사용한다.
- Synchronized 블록 내에서 실행 되어야 한다.
- wait() : 스레드가 lock을 가지고 있으면 lock 권한을 반납하고 대기하게 만든다.
- notify() : 대기 상태인 스레드에게 다시 lock 권한을 부여하고 수행하게 만든다.
- notifyAll() : 잠들어있던 스레드를 모두 깨운다.

[출처](https://velog.io/@kimmy/CS-%EC%A7%80%EC%8B%9D-Java-Thread)
