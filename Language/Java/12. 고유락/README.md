# 고유락

## 고유락(Intrinsic Lock)이란?

자바의 모든 객체는 **lock**을 가지고 있음. 모든 객체가 가지고 있기 떄문에 고유 락이라고 하며, 모니터처럼 동작한다고 하여 monitor lock 혹은 monitor 라고도 함

> 자바의 **_synchronized블록_** 은 이 고유락을 사용해서 락을 다룸

## Synchronized Block

자바 코드에서 동기화 영역은 synchronized 키워드로 표시하고 객체에 대한 동기화가 이루어짐

- 같은 객체에 대한 모든 동기화 블록은 한 시점에 오직 한 쓰레드만이 블록 안으로 접근(실행)하도록 함

### Structured Lock (구조적인 락)

- 고유락을 이용한 동기화

- Synchronized 블록 단위로 락의 획득, 해제가 일어나므로 구조적

- 블록을 진입할 때 락의 획득이, 벗어날 때 락의 해제가 일어남

- Thread-Safe를 보장
  - Thread-Safe 하지 않은 코드
    <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/4c9b6759-5577-4804-a58e-644fa49880c6">
    > 위와 같은 코드에서 동시성 문제가 발생할 수 있기 때문에 count 변수로 접근하는 쓰레드를 제어해야 함
  - Thread-Safe 한 코드
    <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/27b985e7-e49d-40f0-9dab-672016ec3d2d" style="width: 300">
    - lock이라는 객체를 사용하여 count변수에 여러 쓰레드가 동시에 접근하지 못 하도록 제어
    - increase() 메소드는 한 번에 한 스레드만 실행할 수 있음
    ```
    public synchronized int increase() {
        return ++count;
    }
        위 코드로 대체 가능
    ```

<br>

## Reentrancy (고유락 재진입)

- 자바의 고유락은 재진입이 가능
- 락의 획득이 <span style="color: skyblue">**호출 단위가 아닌 쓰레드 단위**</span>로 일어난다는 것을 의미
- 이미 락을 획득한 쓰레드는 같은 락을 얻기 위해 대기할 필요가 없음

    <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/4e8ad876-8ec9-4a39-8f52-93968a76be6b" style="width: 300">

  - b( )가 synchronized로 선언되어 있지만, a( ) 진입시 lock을 획득했기 때문에 b를 호출할 수 있음
  - 고유락 재진입 특성이없었다면 데드락 발생 가능성이 있음

##
