## 🎃클린코드

얼마나 코드가 잘 읽히는 지, 코드가 지저분하지 않고 정리된 코드인지를 나타내는 것이 바로 '클린 코드'

###### 가독성을 높이려면

- 네이밍이 잘 되어야 함
- 오류가 없어야 함
- 중복이 없어야 함
- 의존성을 최대한 줄여야 함
- 클래스 혹은 메소드가 한가지 일만 처리해야 함

## 🎃리팩토링

프로그램의 외부 동작은 그대로 둔 채, 내부의 코드를 정리하면서 개선하는 것을 말함<br>
프로젝트가 끝나면, 지저분한 코드를 볼 때 가독성이 떨어지는 부분이 존재한다.<br>
이 부분을 개선시키기 위해 필요한 것이 바로 '리팩토링 기법'

리팩토링 작업은 코드의 가독성을 높이고, 향후 이루어질 유지보수에 큰 도움이 된다.

###### 리팩토링이 필요한 코드는?

- 중복 코드
- 긴 메소드
- 거대한 클래스
- Switch 문
- 절차지향으로 구현한 코드

## 🎃시큐어코딩[📎](https://yozm.wishket.com/magazine/detail/1822/)

안전한 소프트웨어를 개발하기 위해, 소스코드 등에 존재할 수 있는 잠재적인 보안약점을 제거하는 것

#### 보안 약점을 노려 발생하는 사고사례들

- SQL 인젝션 취약점으로 개인유출 사고 발생
- URL 파라미터 조작 개인정보 노출
- 무작위 대입공격 기프트카드 정보 유출

##### 안전하지 않은 코드

```java
String query "SELECT * FROM users WHERE userid = '" + userid + "'" + "AND password = '" + password + "'";

Statement stmt = connection.createStatement();
ResultSet rs = stmt.executeQuery(query);
```

##### 안전한 코드

```java
String query "SELECT * FROM users WHERE userid = ? AND password = ?";

PrepareStatement stmt = connection.prepareStatement(query);
stmt.setString(1, userid);
stmt.setString(2, password);
ResultSet rs = stmt.executeQuery();
```

#### 클린코드와 리팩토링의 차이?

리팩토링이 더 큰 의미를 가진 것 같다. 클린 코드는 단순히 가독성을 높이기 위한 작업으로 이루어져 있다면, 리팩토링은 클린 코드를 포함한 유지보수를 위한 코드 개선이 이루어진다.

클린코드와 같은 부분은 설계부터 잘 이루어져 있는 것이 중요하고, 리팩토링은 결과물이 나온 이후 수정이나 추가 작업이 진행될 때 개선해나가는 것이 올바른 방향이다.
