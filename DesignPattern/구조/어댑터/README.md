# 어댑터 패턴 (Adapter Pattern)

> 이미 만들어진 것을 그대로 사용할 수 없을 때, 필요한 형태로 사용할 수 있게 해주는 패턴 <br>
> 한 클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 변환 <br>
> 어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있다.

<br>

- 호환되지 않는 인터페이스를 사용하는 클라이언트를 그대로 활용할 수 있다.
- 클라이언트와 구현된 인터페이스를 분리시킬 수 있고, 향후 인터페이스가 바뀌더라도 그 변경 내역은 어댑터에 캡슐화 되기 때문에 클라이언트는 바뀔 필요가 없어진다.

<br>

EX) 한국의 플러그를 일본의 전원 소켓에 끼우려면 동그란 모양을 일자로 바꿔주는 어댑터를 끼워줘야 한다. 이와 같이 어댑터는 소켓의 인터페이스를 플러그에서 필요로 하는 인터페이스로 바꾸어 준다고 할 수 있다.

<br>

```java
public interface MailSenderA {
    public void send(String sendInfo);
}

public class CompanyA implements MailSenderA {
    @Override
    public void send(String sendInfo) {
        System.out.println("A 회사에서 메일 전송" + sendInfo);
    }
}

```

```java
public interface MailSenderB {
    public void sendApi(String sendInfo);
}

public class CompanyB implements MailSenderB {
    @Override
    public void sendApi(String sendInfo) {
        System.out.println("B 회사에서 메일 전송" + sendInfo);
    }
}

```

<br>

```java
public class Adapter implements MailSenderA {
    // Adapter(B회사) 생성자 주입
    private final MailSenderB mailSenderB;

    public Adapter(CompanyB companyB){
        this.mailSenderB = companyB;
    }

    @Override
    public void send(String sendInfo){ // MailSenderA에 있는 함수
        System.out.println("Using Adapter");
        // 기존 send를 호출 -> 솔루션 B의 sendApi 호출 연결
        mailSenderB.sendApi(sendInfo);
    }
}

```

```java
// client
public class Client{
    public static void main(String[] args){
        MailSenderA mailSenderA = new CompanyA();
        mailSenderA.send("기존 발송 메일");

        mailSenderA = new Adapter(new CompanyB());
        mailSenderA.send("To-Be 발송 메일");
    }
}

// 실행 결과
// A 회사에서 메일 발송 : 기존 발송 메일
// Using Adapter B 회사에서 메일 발성 : To-Be 발송 메일

```

<br>

- 기존에 있는 시스템의 레거시 인터페이스를 새로운 인터페이스로 교체하는 경우에 기존 코드를 수정하지 않고 재사용성을 높일 수 있다.
- 새로운 써드파티 라이브러리가 추가되어도 어댑터 패턴은 유용하게 사용된다.

<br>

### 클라이언트에서 어댑터를 사용하는 방법

1. 클라이언트에서 타겟 인터페이스를 사용하여 메소드를 호출함으로써 어댑터에 요청
2. 어댑터에서는 어댑티 인터페이스를 사용하여 그 요청을 어댑티에 대한 하나 이상의 메소드를 호출로 변환
3. 클라이언트에서는 호출 결과를 받긴 하지만 중간에 어댑터가 껴 있는지는 알지 못한다.

<br>

## 객체 어댑터

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/9cef70ef-8b61-4509-87b0-3ee36a8d5d2d">

객체 어댑터에서는 구성을 통해서 어댑티에 요청을 전달한다.
<br>

## 클래스 어댑터

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/a7db1541-34c0-41ed-bcb9-6b5d4ce1eb61">

클래스 어댑터에서는 어댑터를 만들 때 타겟과 어댑티 모두의 서브 클래스로 만든다.
