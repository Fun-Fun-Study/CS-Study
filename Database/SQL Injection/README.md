# 💔 SQL Injection

## SQL Injection 이란?

> 악의적인 사용자가 보안상의 취약점을 이용하여, 임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위
> 공격이 비교적 쉬운 편이고 공격에 성공할 경우 큰 피해를 입힐 수 있는 공격

<br><br>

## 공격 종류 및 방법

### 💦 Error based SQL Injection

**논리적 에러를 이용한 SQL Injection**

- 가장 많이 쓰이는 방법이며 대중적인 공격 기법

<br>

### 💦 Union based SQL Injection

**Union 명령어를 이용한 SQL Injection**

- Union은 두 개의 뭐리문에 대한 결과를 통합해서 하나의 테이블로 보여주게 하는 키워드
- 정상적인 쿼리문에 Union 키워드를 사용하여 인젝션에 성공하면 원하는 쿼리문 실행 가능
- Union Injection을 성공하기 위해서는 두 가지의 조건이 필요
  - Union 하는 두 테이블의 컬럼 수가 같아야 함
  - 데이터 형이 같아야 함

<br>

### 💦 Blind SQL Injection

**Boolean based SQL**

- 데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고 단순히 참과 거짓의 정보만 알 수 있을 때 사용
- 서버의 응답을 이용하여 DB의 테이블 정보 등 추출 가능

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
> 이런 공격입니다.

<br><br>

## 대응 방안

### 입력 값에 대한 검증

### Error Message 노출 금지

### 웹 방화벽 사용
