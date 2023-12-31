## 데이터 베이스란?

컴퓨터 시스템에 저장되는 조직화된 데이터의 모음으로 데이터를 조직화하면 데이터에 의미가 생기고 대량의 데이터를 효율적으로 관리할 수 있다.</br>
이러한 데이터를 조직화하는 방식은 여러가지가 있고, **관리하는 방식에 따라 데이터베이스 유형을 구분**한다.

## 데이터베이스 관리시스템 (Database Management System, DBMS)

데이터베이스를 실질적으로 구현하기 위해 DBMS를 사용</br>
연결할 애플리케이션, 데이터, DBMS솔루션을 하나로 묶어 데이터베이스 시스템 or 데이터베이스라고도 한다.

## SQL (관계형 데이터베이스)

SQL을 사용하면 RDBMS에서 데이터를 저장, 수정, 삭제 및 검색을 할 수 있다.

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/b13f4284-de85-49cf-8801-b9d2ebba0af0">

### 특징

- 고정된 행과 열로 구성된 테이블에 데이터를 저장하는 DB
  - 열은 하나의 속성에 대한 정보를 저장
  - 행에는 각 열의 데이터 형식에 맞는 데이터가 저장
- 스키마를 준수하지 않은 레코드는 테이블에 저장 불가
  - 데이터는 테이블에 레코드로 저장 되며 각 테이블마다 명확하게 정의된 구조(필드 이름 + 데이터 유형)가 있다.
- 관계를 통해 여러 테이블에 분산
  - 데이터의 중복을 피하기 위해 관계를 이용

### 관계형 데이터베이스 관리 시스템 (Relational Database Management System)

- MySQL
- Oracle
- SQLite
- MariaDB
- PostgresSQL

### 장점

- 데이터 무결성 보장(명확하게 정의된 스키마)
- 관계는 각 데이터를 중복없이 한번만 저장

### 단점

- 데이터 스키마를 사전에 계획해야해서 유연성이 떨어짐
- 관계로 인해 JOIN이 많은 복잡한 쿼리가 만들어질 수 있다.
- 대체로 수직적 확장만 가능

### ✔️관계형 데이터베이스를 SQL이라고 부르는 이유

관계형 데이터베이스는 데이터베이스의 한 유형으로 문법이 조금씩 다르지만 모두 **초창기 관계 데이터베이스 시스템을 위해 만들어진 SQL이라는 언어를 사용**하여 관계형 데이터베이스를 SQL이라고 부른다.

## NoSQL (비관계형 데이터베이스)

관계형 데이터베이스를 제외한 나머지 유형의 데이터베이스<br>
대량의 분산된 데이터를 저장하고 조회하는 데 특화되었으며, 스키마 없이 사용 가능하거나 느슨한 스키마를 제공하는 저장소<br>
관계형 데이터베이스의 한계를 극복하기 위한 데이터 저장소의 새로운 형태

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/97a5b4e8-ea09-41d4-9f3d-faa742bc650e">

### 특징

- 데이터 간 관계를 저장하지 않지만 관계 데이터를 저장 가능
- 유연한 스키마를 제공
- 대량의 데이터와 높은 사용자 부하에서도 손쉽게 확장이 가능
- 분산형 구조
  - 여러 서버에 데이터를 분산 저장해 특정 서버에 장애가 발생했을 때에도 데이터 유실 혹은 서비스 중지 예방
- Schema on Read
  - 스키마에 따라 데이터를 읽어온다

### 장점

- 스키마가 없어 언제든지 저장된 데이터를 조정하고 새로운 필드 추가 가능
- 데이터는 애플리케이션이 요구하는 형식으로 저장되며 데이터를 읽어오는 속도가 빠라진다.
- 수직/수평적 확장이 가능하며 애플리케이션이 발생시키는 모든 읽기/쓰기 요청 처리 가능

### 단점

- 유연성으로 인해 데이터 구조 결정을 미루게 될 수 있음
- 데이터 중복을 계속 업데이트 해야함
- 데이터가 여러 컬렉션에 중복되어 있기 때문에 수정 시 모든 컬렉션에서 수행해야 함

### NoSQL 데이터베이스 유형

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/5d561efd-f475-49f9-ba9d-ab19b323dab7">

<br>

1. Key-Value 타입

    - 속성을 Key-Value의 쌍으로 나타내는 데이터를 배열 형태로 저장
    - Key : 속성 이름, Value : 속성에 연결된 데이터 값
    - Redis, Amazon DynamoDB 등
  </br></br>

2. 문서형 데이터베이스

   - 데이터를 테이블이 아닌 문서처럼 저장하는 데이터베이스
   - JSON과 유사한 형식의 데이터를 문서화하여 저장
   - 각각의 문서는 하나의 속성에 대한 데이터를 가지고 있고, 컬렉션이라는 구룹으로 묶어서 관리
   - MongoDB 등
     </br></br>

3. Wide-Column Store 데이터베이스

   - 데이터베이스의 열에 대한 데이터를 집중적으로 관리하는 DB
   - 각 열에는 Key-Value 형식으로 데이터가 저장되고, 컬럼 패밀리(column families)라고 하는 열의 집합체 단위로 데이터를 처리할 수 있다
   - 하나의 행에 많은 열을 포함할 수 있어서 유연성이 높다
   - 데이터 처리에 필요한 열을 유연하게 선택 할 수 있다는 점에서 규모가 큰 데이터 분석에 주로 사용
   - Apache Cassandra, Apache HBase 등
     </br></br>

4. 그래프 데이터베이스
   - 자료구조의 그래프와 비슷한 형식으로 데이터 간의 관계를 구성하는 데이터베이스
   - 노드에 속성별 데이터를 저장
   - 각 노드간 관계는 선으로 표현
   - Neo4J, InfiniteGraph 등
     </br></br>

### 확장성

DB 서버의 확장성은 **수직적** 확장과 **수평적** 확장으로 나뉜다

- 수직적 확장 : 데이터 베이스 서버의 성능 향상(ex. CPU 업그레이드)
- 수평적 확장 : 서버가 추가되고, 데이터베이스가 전체적으로 분산됨을 의미

**SQL**

- 일반적으로 수직적으로 확장
- DB가 구축된 하드웨어의 성능을 많이 이용하기 떄문에 비용이 많이 든다.
- 여러 서버에 걸쳐 DB의 관계를 정의할 수 있지만 매우 복잡하고 시간이 많이 소모 된다.

**NoSQL**

- 일반적으로 수평적으로 확장
- 서버를 추가적으로 구축하면 많은 트래픽을 편리하게 처리할 수 있다.
- 저렴한 범용 하드웨어나 클라우드 기반의 인스턴스에 호스팅 할 수 있어서 수직적 확장보다 상대적으로 비용이 저렴하다

## SQL vs NoSQL

**✔️SQL 기반의 RDBS를 사용하기 좋은 경우**

- DB의 ACID 성질을 준수해야하는 경우
  - SQL은 DB와 상호작용하는 방식을 정확하게 규정하기 떄문에 데이터를 처리할 떄 발생할 수 있는 예외적인 상황을 줄이고 무결성을 보호
- 소프트웨어에 사용되는 데이터가 구조적이고 일관적인 경우
  - 다양한 데이터 유형과 높은 트래픽을 지원하도록 설계된 NoSQL 데이터베이스를 사용해야만 하는 이유가 없음
- 관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션의 경우
  - NoSQL에서는 여러 컬렉션을 모두 수정해야 하기 때문에 비효율적

**ACID**<br>
데이터베이스에서 실행되는 하나의 트랜잭션(Transaction)에 의한 상태의 변화를 수행하는 과정에서, 안전성을 보장하기 위해 필요한 성질

- Atomicity(원자성)
- Consistency(일관성)
- Isolation(격리성)
- Durability(지속성)

**✔️NoSQL 기반의 DB를 사용하기 좋은 경우**

- 정형화 되지 않은 대용량의 데이터를 저장하는 경우
- 클라우드 컴퓨팅 및 저장공간을 최대한 활용하는 경우
  - 클라우드 기반으로 데이터베이스 저장소를 구축하면, 저렴한 비용의 솔루션을 제공받을 수 있다.
- 빠르게 서비스를 구축하는 과정에서 데이터 구조를 자주 업데이트 하는 경우
  - 스키마를 미리 준비할 필요가 없기 때문에 빠르게 개발하는 과정에 매우 유리
- 읽기를 자주하지만, 데이터 변경은 자주 없는 경우
  - 성능과 비용적 측면에서 효율적

### 용어 비교

| SQL    | MongoDB  | DynamoDB   | Cassandra | Couchbase  |
| ------ | -------- | ---------- | --------- | ---------- |
| 테이블 | 컬렉션   | 테이블     | 테이블    | 데이터버킷 |
| 열     | 문서     | 항목       | 열        | 문서       |
| 컬럼   | 필드     | 속성       | 컬럼      | 필드       |
| 기본키 | ObjectId | 기본키     | 기본키    | 문서 ID    |
| 인덱스 | 인덱스   | 보조인덱스 | 인덱스    | 인덱스     |

> 참고<br>[NoSQL 의 종류별 특징](https://velog.io/@swhan9404/NoSQL-%EC%9D%98-%EC%A2%85%EB%A5%98%EB%B3%84-%ED%8A%B9%EC%A7%95)<br>[NoSQL이란?](https://aws.amazon.com/ko/nosql/)
