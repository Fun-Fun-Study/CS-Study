# Test 코드

## 왜 Spring에서 Test 코드를 작성하는가?

### 비용 측면

- Test 코드 사용 X

  1. 검증 코드 작성 2.애플리케이션 실행
  2. PostMan 혹은 브라우저 Request 요청
  3. log 혹은 print로 결과 검증
  4. 원하지 않는 결과 발생 시 애플리케이션 종료
  5. 다시 코드 작성

  > 원하는 결과를 얻을 때까지 위의 로테이션을 돌림. 간단한 애플리케이션도 실행하교 종료하는데 비용이 많이 들기 때문에 비용적으로 불리함

<br>

- Test 코드 사용 O

  1. Test 코드 작성
  2. Test 코드 실행
  3. 결과 검증
  4. Test 코드 수정

  > 💡 전체 애플리케이션을 실행, 종료할 필요가 없음. 따라서 비용이 줄어들고 Test를 통해 명확한 검증이 가능

### 구조적 측면

#### 일반적인 Spring의 계층 구조

- **Controller** : 클라이언트 요청을 받고 클라이언트에게 결과를 반환 (Presentation Layer)
- **Service** : 비즈니스 로직을 실행하고 결과 반환(Service Layer)
- **Repository** : database에 쿼리를 이용해서 CRUD를 하는 계층(Data Access Layer)
- **Domain** : Entity 클래스

  > 애플리케이션을 실행해서 Test 하면 어느 계층에서 코드가 잘못된 것인지 파악하는데 많은 비용이 듬<br>
  > 💡 Test 코드를 통해서 계층별로 진행하면 파악이 쉬워 비용을 줄일 수 있음

<br>

## Spring에서의 Test

### JUnit

- Java에서 독립된 단위 테스트를 지원해주는 프레임워크
- AssertJ(검증)을 이용해서 결과 기댓값과 실제 값을 비교
- @Test 어노테이션마다 독립적인 테스트 가능

### 단위 테스트와 통합 테스트

#### 단위 테스트

> 하나의 모듈을 기준으로 독립적으로 진행되는 가장 작은 단위 테스트 -> 쉽게 말하면 <span style="color: skyblue">**하나의 기능 혹은 메서드**</span>

- 장점
  - 새로운 기능에 대해서 빠르게 작성 가능
  - Test 코드 자체가 하나의 문서
  - 시간과 비용의 절감
- 단점
  - 독립적인 테스트이므로 다른 객체와 상호작용 처리를 위해서 가짜 객체 정의 필요함
  - 가짜 객체의 답변 작성 필요함
  - 실제 운영 환경과 다른 답변을 내놓을 수 있는 가능성이 있음

##### 💡 좋은 단위 테스트

- **1개의 테스트는 1개의 기능**에 대해서 테스트
- 테스트 주체와 협력자를 구분
- Given, When, Then을 명확하게 작성
  - Given : 테스트를 진행할 행위를 위한 사전 준비
  - When : 테스트를 진행할 행위
  - Then : 테스트를 진행할 행위에 대한 결과 검증

#### 통합 테스트

> 모듈을 통합화는 과정에서 **모듈 간의 호환성을 확인**하는 테스트 -> unit이 하나였다면 반대로 여러 개의 계층이 테스트에 참여한 것

- 장점
  - 실제 객체를 사용하므로 가짜 객체 사용하지 않아 정의하지 않아도 됨
  - 실제 운영 환경과 같은 값을 도출 가능함
- 단점
  - 테스트 하나의 많은 비용이 들어감
  - 어느 계층에서 발생한 문제인지 파악하기 힘듦

####
