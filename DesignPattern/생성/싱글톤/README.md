# 싱글톤 패턴



### 싱글톤 패턴이란?

- **인스턴스가 오직 1개만 생성**되어야 하는 경우에 사용하는 패턴이다.
- 하나의 인스턴스를 메모리에 등록해서 여러 스레드가 동시에 공유하여 사용하므로 요청이 많은 곳에서 효율을 높일 수 있다.
- getInstance 메서드를 통해 모든 클라이언트에게 동일한 인스턴스를 반환하는 작업을 수행한다.



### 싱글톤 패턴 예제

```java
/*
	Printer 생성자를 외부에서 사용 불하도록 private으로 선언
	자기자신에 대한 인스턴스를 하나 만들어 외부에 제공해 줄 메서드가 필요하기때문에
	static메서드 / static 변수를 사용
	(클래스의 인스턴스를 통하지 않고서도 메서드를 실행할 수 있고 변수를 참조할 수 있다)
	만약 new Printer()가 호출 되기 전이면 인스턴스 메서드인 print()메서드는 호출불가
*/
public class Printer {
  // 외부에 제공할 자기 자신의 인스턴스
  private static Printer printer = null;
  private Printer() { }
  // 자기 자신의 인스턴스를 외부에 제공
  public static Printer getPrinter(){
    if (printer == null) {
      // Printer 인스턴스 생성
      printer = new Printer();
    }
    return printer;
  }
  public void print(String str) {
    System.out.println(str);
  }
}
```

```java
// Client에서의 사용 코드
public class User {
  private String name;
  public User(String name) { this.name = name; }
  public void print() {
    Printer printer = printer.getPrinter();
    printer.print(this.name + " print using " + printer.toString());
  }
}
public class Client {
  private static final int USER_NUM = 5;
  public static void main(String[] args) {
    User[] user = new User[USER_NUM];
    for (int i = 0; i < USER_NUM; i++) {
      // User 인스턴스 생성
      user[i] = new User((i+1))
      user[i].print();
    }
  }
}
```

### 문제점

다중 스레드에서 Printer 클래스를 이용할 때 인스턴스가 1개 이상 생성되는 경우가 발생할 수 있다.

이를 해결하기 위해선 다음과 같은 방법이 있다.

1. 정적 변수에 인스턴스를 만들어 바로 초기화 하는 방법
2. 인스턴스를 만드는 메서드에 동기화하는 방법

<br>

1. 정적 변수에 인스턴스를 만들어 바로 초기화 하는 방법

```java
public class Printer {
   // 기존 위의 싱글톤 방식
   private static Printer printer = null; // --> X
    
   // static 변수에 외부에 제공할 자기 자신의 인스턴스를 만들어 초기화
   private static Printer printer = new Printer(); // --> O
   private Printer() { }
   // 자기 자신의 인스턴스를 외부에 제공
   public static Printer getPrinter(){
     return printer;
   }
   public void print(String str) {
     System.out.println(str);
   }
}
```



2. 인스턴스를 만드는 메서드에 동기화하는 방법

```java
public class Printer {
   // 외부에 제공할 자기 자신의 인스턴스
   private static Printer printer = null;
   private int counter = 0;
   private Printer() { }
   // 인스턴스를 만드는 메서드 동기화 (임계 구역, synchronized)
   public synchronized static Printer getPrinter(){
     if (printer == null) {
       printer = new Printer(); // Printer 인스턴스 생성
     }
     return printer;
   }
   public void print(String str) {
     // 오직 하나의 스레드만 접근을 허용함 (임계 구역)
     // 성능을 위해 필요한 부분만을 임계 구역으로 설정한다.
     synchronized(this) {
       counter++;
       System.out.println(str + counter);
     }
   }
}
```