# 💔 SQL Injection

## SQL Injection 이란?

> 악의적인 사용자가 보안상의 취약점을 이용하여, 임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위
> 공격이 비교적 쉬운 편이고 공격에 성공할 경우 큰 피해를 입힐 수 있는 공격

<br><br>

## 공격 목적

- 정보 유출
- 저장된 데이터 유출 및 조작
- 원격 코드 실행
  - 확장 프로시저를 이용하여 원격으로 시스템 명령의 실행이 가능
  - 시스템 명령의 실행은 원격 자원 접근 및 데이터 유출, 삭제가 가능
- 인증 우회
  - 공격의 대표적인 경우로 로그인 폼 등에서 발생
  - 상위 권한을 가진 사용자의 권한으로 인증 절차를 우회하여 로그인 정보 없이 로그인 가능

<br><br>

## 공격 종류 및 방법

### 💦 Error based SQL Injection

**논리적 에러를 이용한 SQL Injection**

- 가장 많이 쓰이는 방법이며 대중적인 공격 기법
- 입력값에 대한 검증이 없음을 확인하고, 악의적인 사용자가 임의의 SQL 구문 주입

<br>

### 💦 Union based SQL Injection

**Union 명령어를 이용한 SQL Injection**

- Union 키워드는 두 개의 뭐리문에 대한 결과를 통합해서 하나의 테이블로 보여주게 하는 키워드
- 정상적인 쿼리문에 Union 키워드를 사용하여 인젝션에 성공하면 원하는 쿼리문 실행 가능
- Union Injection을 성공하기 위해서는 두 가지의 조건이 필요
  - Union 하는 두 테이블의 컬럼 수가 같아야 함
  - 데이터 형이 같아야 함
- 입력값에 대한 검증이 없기 때문에 발생

<br>

### 💦 Blind SQL Injection

**Boolean based SQL**

- 데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고 단순히 참과 거짓의 정보만 알 수 있을 때 사용
- 서버의 응답을 이용하여 DB의 테이블 정보 등 추출 가능
- 로그인 폼에 SQL Injection이 가능하다고 가정 했을 때, 서버가 응답하는 로그인 성공, 실패 메시지를 이용하여 DB의 테이블 정보 등 추출 가능

**Time based SQL**

- 서버로부터 특정한 응답 대신에 참 혹은 거짓의 응답을 통해서 데이터베이스의 정보를 유추하는 기법
- 사용되는 함수는 MySQL 기준으로 SLEEP과 BENCHMARK

<br>

### 💦 Stored Procedure SQL Injection

**저장된 프로시저에서의 SQL Injection**

- 일련의 쿼리들을 모아 하나의 함수처럼 사용하기 위한 것
- 공격에 사용되는 대표적인 저장 프로시저는 MSSQL에 있는 xp_cmdshell로 윈도우 명령어 사용 가능
- 공격자가 시스템 권한을 획득해야 하므로 공격 난이도가 높으나 성공한다면 서버에 직접적인 피해를 입힐 수 있음

<br>

### 💦 Mass SQL Injection

**다량의 SQL Injection 공격**

- 한 번의 공격으로 다량의 데이터베이스가 조작되어 큰 피해를 입히는 것
- 데이터베이스 값을 변조하여 데이터베이스에 악성 스크립트를 삽입하고, 사용자들이 변조된 사이트에 접속 시 좀비PC로 감염되며 감염된 좀비 PC들은 DDoS 공격에 사용

<br>

> ❔ DDoS 공격 <br>
> 응용 프로그램의 리소스를 소진하려는 시도로 네트워크 서비스를 중단시킴으로써 웹 사이트 및 서버를 공격합니다. <br>
> 공격자는 사이트가 비정상 트래픽으로 넘치게 하여 웹 사이트 기능 저하 혹은 오프라인 상태로 만듭니다.

<br><br>

## 대응 방안

### 입력 값에 대한 검증

- 서버 단에서 화이트리스트 기반으로 검증

> ❔ 화이트리스트<br> **안전**이 증명된 것만을 허용하는 것으로 **악의성**이 입증된 것을 차단하는 블랙리스트 보안과 상반되는 보안 방식입니다. <br>
> 특정한 업무만 수행하는 특수 서버와 같이 변화가 적고 운용되는 애플리케이션 숫자가 많지 않은 기기에서 효용 가치가 높습니다.

### Prepared Statement 구문 사용

- 해당 구문을 사용하게 되면, 사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에 DBMS가 미리 컴파일 하여 실행하지 않고 대기 <br>
- 그 후 공격쿼리가 들어간다고 하더라도, 사용자의 입력은 이미 의미 없는 단순 문자열이기 때문에 전체 쿼리문도 공격자의 의도대로 작동하지 않는다.

### Error Message 노출 금지

### 웹 방화벽 사용
