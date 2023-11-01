### 🚨 **컴파일 오류와 런타임 오류**

프로그램을 실행하다가 보면 어떠한 원인때문에 비정상적인 동작을 일으시켜 프로그램이 종료되는 상황을 자주 볼 수 있다. 이를 우리는 프로그램에 오류가 발생했다고 말한다. 에러의 종류로는 컴파일할 때 발생할 수 있는 **컴파일 오류**와 실행 중에 발생하는 **런타임 오류** 두 종류가 있다.

**컴파일 오류**

컴파일 오류는 소스코드를 **.class 파일을 컴파일하는 과정에서 JVM이 던지는 오류**로, 대부분 소스코드 자체의 **문법적 오류**로 인해 발생하는 경우가 대부분이며, 프로그램 자체에서 처리할 수 있는 방법은 없다.

컴파일 오류의 예로는 `ClassNotFoundException`, `IllegalAccessException`, `NoSuchMethodException` 등이 있다.

**런타임 오류**

런타임 오류는 문법적인 오류가 없어 컴파일 시에는 정상적으로 컴파일됐지만 **프로그램을 실행하는 과정에서 발생하는 오류**를 말한다. 이는 개발자가 직접 오류를 확인하여 처리해야 한다.

런타임 오류의 예로는 `NullPointerException`, `ArithmeticException`, `IndexOutOfBoundsException` 등이 있다.

### 🚨 Error와 Exception

- 어떤 원인에 의해 오동작 하거나 비정상적으로 종료되는 경우
- 심각도에 따른 분류
  - Error
    - 메모리 부족, stack overflow와 같이 일단 발생하면 복구할 수 없는 상황
    - 프로그램의 비 정상적 종료를 막을 수 없음 → 디버깅 필요
  - Exception
    - 읽으려는 파일이 없거나 네트워크 연걸이 안되는 등 수습될 수 있는 비교적 상태가 약한 것들
    - 프로그램 코드에 의해 수습될 수 있는 상황
- exception handling(예외 처리)란
  - 예외 발생 시 프로그램의 비 정상 종료를 막고 정상적인 실행 상태를 유지하는 것
    - 예외의 감지 및 예외 발생 시 동작할 코드 작성 필요

<aside>
💡 오류와 예외 모두 Object 클래스를 상속 받는 `Throwable` 클래스를 상속 받는다.
Throwable 객체는 오류나 예외에 대한 메시지를 담고, 예외가 연결될 때 연결된 예외의 정보를 기록한다.
이를 위해 Throwable 클래스에는 `getMessage()`와 `printStackTrace()` 함수가 구현되어 있다.

| 메서드                        | 설명                                                                                                |
| ----------------------------- | --------------------------------------------------------------------------------------------------- |
| public String getMessage()    | 발생된 예외에 대한 구체적인 메세지를 반환한다.                                                      |
| public Throwable getCause()   | 예외의 원인이 되는 Throwable 객체 또는 null을 반환한다.                                             |
| public void printStackTrace() | 예외가 발생된 메서드가 호출되기까지의 메서드 호출 스택을 출력한다. 디버깅의 수단으로 주로 사용된다. |

</aside>

```java
public static void main(String[] args) {
        int[] intArray = { 10 };
        System.out.println(intArray[2]);
        try {
        	System.out.println(intArray[2]);
        } catch(ArrayIndexOutOfBoundsException e) {
        	System.out.println("예외 처리 완료" + e.getMessage());
        	e.printStackTrace();
        }
        System.out.println("프로그램 종료합니다.");
    }
```

**예외 클래스의 계층**

![exception](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/ad06c998-6b11-4bd4-a681-0066256770bd)

- checked exception
  - 예외에 대한 대처 코드가 없으면 컴파일이 진행되지 않음
- unchecked exception (`RuntimeException`의 하위 클래스)
  - 예외에 대한 대처 코드가 없더라도 컴파일은 진행됨

| 구분          | Checked Exception                      | Unchecked Exception                         |
| ------------- | -------------------------------------- | ------------------------------------------- |
| 확인 시점     | 컴파일(Compile) 시점                   | 런타임(Runtime) 시점                        |
| 처리 여부     | 반드시 예외 처리해야 함                | 명시적으로 하지 않아도 됨                   |
| 트랜잭션 처리 | 예외 발생 시 롤백(rollback)하지 않음   | 예외 발생 시 롤백(rollback)해야 함          |
| 종류          | IOException, ClassNotFoundException 등 | NullPointerException, ClassCastException 등 |

### 🚨 예외 처리 방법

**예외 복구**

예외 복구는 예외 상황을 파악하고 **문제를 해결하여 정상 상태로 돌려놓는 방법**이다.

예외를 잡아서 일정 시간이나 조건만큼 대기하고 재시도를 반복한다.

최대 재시도 횟수를 넘기게 될 경우에 예외를 발생한다.

<details>
<summary>💻 코드</summary>
<div markdown="1">

```java
final int MAX_RETRY = 100;
int maxRetry = MAX_RETRY;
while(maxRetry > 0) {
    try {
        ...
    } catch(SomeException e) {
    // 로그 출력. 정해진 시간만큼 대기한다.
    } finally {
    // 리소스 반납 및 정리 작업
    }
}
// 최대 재시도 횟수를 넘기면 직접 예외를 발생시킨다.throw new RetryFailedException();
```

</div>
</details>
<br>

**예외 회피**

예외 회피는 예외 처리를 직접 담당하지 않고 **호출한 메서드로 위임해 회피하는 방법**이다.

예외 처리의 필요성이 있다면 어느 정도는 처리하고 위임하는 것이 좋다.

<details>
<summary>💻 코드</summary>
<div markdown="1">

```java
// 예시 1
public void add() throws SQLException {
// ...생략
}

// 예시 2public void add() throws SQLException {
    try {
// ... 생략
    } catch(SQLException e) {
// 로그를 출력하고 다시 날린다!throw e;
    }
}
```

</div>
</details>
<br>

**예외 전환**

예외 회피와 비슷하게 메서드 밖으로 예외를 위임하지만, 그냥 위임하지 않고 **적절한 예외로 전환해서 넘기는 방법**이다. 조금 더 명확한 의미를 전달하기 위해 **적합한 의미를 가지는 예외로 변경**한다.

예외 처리를 단순하게 만들기 위해 **포장(wrap)** 할 수도 있다.

<details>
<summary>💻 코드</summary>
<div markdown="1">

```java
  // 조금 더 명확한 예외로 던진다.public void add(User user) throws DuplicateUserIdException, SQLException {
      try {
  // ...생략
      } catch(SQLException e) {
          if(e.getErrorCode() == MysqlErrorNumbers.ER_DUP_ENTRY) {
              throw DuplicateUserIdException();
          }
          else throw e;
      }
  }

  // 예외를 단순하게 포장한다.public void someMethod() {
      try {
  // ...생략
      }
      catch(NamingException ne) {
          throw new EJBException(ne);
          }
      catch(SQLException se) {
          throw new EJBException(se);
          }
      catch(RemoteException re) {
          throw new EJBException(re);
          }
  }
```

</div>
</details>
<br>

**try ~ catch 구문**

```java
try{
	//예외가 발생할 수 있는 코드
} catch(XXException e){ // 던진 예외를 받음
	//예외가 발생했을 때 처리할 코드
}
```

```java
int[] intArray = {10};
try{
	System.out.println(intArray[2]);
} catch(ArrayIndexOutOfBoundsException e){
	System.out.println("예외 처리 완료");
}
```

**try-catch 문에서의 흐름**

- try 블록에서 예외가 발생하면
  - JVM이 해당 Exception 클래스의 객체 생성 후 던짐(throw)
    - `throw new XXException()`
  - 던져진 exception 을 처리할 수 있는 catch 블록에서 받은 후 처리
    - 적당한 catch 블록을 만나지 못하면 예외처리는 실패
  - 정상적으로 처리되면 try-catch 블록을 벗어나 다음 문장 진행
- try 블록에서 어떠한 예외도 발생하지 않은 경우

  - catch 문을 거치지 않고 try-catch 블록의 다음 흐름 문장을 실행

  ```java
  public static void main(String[] args){
  	int num = new Random().nextInt(2);

  	try{
  		System.out.println("1" + num);
  		int i = 1/num;
  		System.out.println("2");
  } catch(ArithmeticException e){
  		System.out.println("3");
  }
  System.out.println("4");
  }
  num이 0일 때 출력되는 내용은? 1 3 4
  num이 1일 때 출력되는 내용은? 1 2 4
  ```

**다중 exception handling**

- try 블록에서 여러 종류의 예외가 발생할 경우

  - 하나의 try 블록에 여러 개의 catch 블록 추가 가능

  ```java
  try{
  	// exception이 발생할 만한 코드
  }catch(XXException e){
  	// XXException 발생 시 처리 코드
  }catch(YYException e){
  	// YYException 발생 시 처리 코드
  }catch(Exception e){
  	// Exception 발생 시 처리 코드
  }

  Exception이 가장 위로 간다면 나머지 catch구문은 사용하지 않음

  ```

- 다중 catch 문장 작성 순서 유의 사항
  - JVM이 던진 예외는 catch 문장을 찾을 때는 다형성이 적용됨
  - 상위 타입의 예외가 먼저 선언되는 경우 뒤에 등장하는 catch 블럭은 동작할 기회가 없음
  - 상속 관계가 없는 경우는 무관
  - 상속 관게에서는 작은 범위에서 큰 범위 순으로 정의

**다중 예외 처리를 이용한 Checked Exception 처리**

- 처리하지 않으면 컴파일 불가: Checked Exception
- 예외 처리는 가능한 구체적으로 진행
- 발생하는 예외를 하나로 처리하기
  - 예외 상황 별 처리가 쉽지 않음
  - 가급적 예외 상황 별로 처리하는 것을 권장
- 심각하지 않은 예외를 굳이 세분화 해서 처리하는 것도 낭비
  - ‘|’를 이용해 하나의 catch 구문에서 상속관계가 없는 여러 개의 exception 처리

**try ~ catch ~ finally 구문을 이용한 예외 처리**

- finally는 예외 발생 여부와 관계없이 언제나 실행
  - 중간에 `return` 을 만나는 경우에도 finally 블록을 먼저 수행 후 리턴 but `System.exit(0)`는 수행 안함
  ```java
  try{
  	// exception이 발생할 만한 코드 - System 자원 사용
  } catch(Exception e){
  	// XXException 발생 시 처리 코드
  } finally{
  	//try block에서 접근했던 System 자원의 안전한 원상복구
  }
  ```

**메서드 재정의와 throws**

- 메서드 재정의 시 조상 클래스 메서드가 던지는 예외보다 부모예외를 던질 수 없다.
  1. `IOException`
  2. `FileNotFoundException`, `EOFException`
  3. `throws`를 하지 않거나

**사용자 정의 예외 작성**

- class로 정의할 때 extends를 이용
- throw를 통해 새로운 Exception을 던짐
- 새로운 함수에도 throws를 통해 사용자 정의 예외처리 가능
