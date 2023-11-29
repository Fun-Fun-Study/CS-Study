# ✨ REST API

Representational State Transfer

> REST 아키텍처 스타일의 제약 조건을 준수하고 RESTful 웹 서비스와 상호 작용할 수 있도록 하는 애플리케이션 프로그래밍 인터페이스

> 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것

> 컴퓨터 프로그램끼리 소통하기 위한 규칙

<br>

### REST

HTTP URI를 통해 자원을 명시하고, <br>
HTTP Method (POST, GET, PUT, DELETE, PATCH 등) 을 통해 <br>
해당 자원에 대한 CRUD Operation을 적용하는 것

<br>

🎈 REST 구성요소

1. 자원 : HTTP URI
2. 자원에 대한 행위 : HTTP Method
3. 자원에 대한 행위의 내용 : HTTP Message Pay Load

<br>

🎈 REST의 특징

1. 서버-클라이언트 구조
2. 무상태 Stateless
3. 캐시 처리 가능
4. 계층화
5. 인터페이스 일관성

<br>

🎈 REST의 장점

- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악 가능하다.
- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

<br>

🎈 REST의 단점

- 표준이 존재하지 않아 정의가 필요하다.
- HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL 보다 Header 정보의 값을 처리해야 하므로 전문성이 요구ㄷ힌다.
- 구형 브라우저에서 호환이 되지 않아 지원해주지 못하는 동작이 많다.

<br>

### RESTful

    RESTFul이란 REST의 원리를 따르는 시스템을 의미한다.
    즉, REST를 사용했다 하여 모두가 RESTFul 한 것이 아니라 REST API의 설계 규칙을 올바르게 자킨 시스템을 RESTFUL 하다 말할 수 있다.

<br>

### REST API의 설계 규칙

1. URI는 동사보다 명사를, 대문자보다는 소문자를 사용하여야 한다. <br>
   > BAD : /api/Running <br>
   > GOOD : /api/run

<br>

2. 마지막에 슬래시를 포함하지 않는다. <br>
   > BAD : /api/test/ <br>
   > GOOD : /api/test

<br>

3. 언더바 대신 하이픈을 사용한다. <br>
   > BAD : /api/test_run <br>
   > GOOD : /api/test-run

<br>

4. 파일 확장자는 URI에 포함하지 않는다. <br>
   > BAD : /api/photo.png <br>
   > GOOD : /api/photo

<br>

5. 행위를 포함하지 않는다. <br>
   > BAD : /api/delete-info/1 <br>
   > GOOD : /api/info/1
