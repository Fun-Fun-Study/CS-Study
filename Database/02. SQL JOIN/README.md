# 🙌 SQL JOIN

둘 이상의 테이블을 연결해서 데이터를 검색하는 방법으로 <br>
연결을 위해서 테이블은 적어도 하나의 컬럼을 공유하고 있어야 하며 공유하고 있는 컬럼을 PK 혹은 FK로 사용합니다.

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/b786ad70-7640-40d0-88da-397848b3cdad" alt="sql조인" />

<br><br>

## INNER JOIN (내부조인, 교집합)

- 공통적인 부분만 SELECT

```sql
SELECT A.ID, A.NAME
FROM A INNER JOIN B ON A.ID = B.ID;
```

<br>

## LEFT/RIGHT JOIN (부분집합)

**LEFT JOIN**

- 조인 기준 왼쪽에 있는거 전부 SELECT (교집합 + LEFT)

```sql
SELECT A.ID, A.NAME
FROM A LEFT OUTER JOIN B ON A.ID = B.ID;
```

- 조인 기준 왼쪽에 있는것 **만** SELECT (LEFT - 교집합)

```sql
SELECT A.ID, A.NAME
FROM A LEFT OUTER JOIN B ON A.ID = B.ID
WHERE B.IS IS NULL;
```

<br>

**RIGHT JOIN**

- 조인 기준 오른쪽에 있는거 전부 SELECT (교집합 + RIGHT)

```sql
SELECT A.ID, A.NAME
FROM A RIGHT OUTER JOIN B ON A.ID = B.ID;
```

- 조인 기준 오른쪽에 있는것 **만** SELECT (RIGHT - 교집합)

```sql
SELECT A.ID, A.NAME
FROM A RIGHT OUTER JOIN B ON A.ID = B.ID
WHERE A.ID IS NULL;
```

<br>

## OUTER JOIN (외부조인, 합집합)

- A테이블과 B테이블이 가지고 있는것 전부 SELECT

```sql
SELECT A.ID, A.NAME
FROM A FULL OUTER JOIN B ON A.ID = B.ID;
```

- 전체에서 공통적인 부분 제외한 것 SELECT

```sql
SELECT A.ID, A.NAME
FROM A FULL OUTER JOIN B ON A.ID = B.ID
WHERE A.ID IS NULL OR B.ID IS NULL;
```

<br>

# 🙌 JOIN의 원리

### 중첩 루프 조인 NESTED LOOPS JOIN

- 2개 이상의 테이블에서 하나의 집합을 기준으로 순차적으로 상대방 ROW를 결합하여 원하는 결과를 조인하는 방식
- 조인해야 할 데이터가 많지 않은 경우에 유용하게 사용
- 인덱스에 의한 랜덤 엑세스 기반으므로 대량의 데이터 처리 시 적합하지 않음

### 정렬 병합 조인 SORT MERGE JOIN

- 조회의 범위가 많을 때 주로 사용하는 조인
- 양쪽 테이블을 각 Access 하여 그 결과를 정렬하고 그 정렬한 결과를 차례로 스캔해 나가면서 연결고리의 조건으로 Merge 하는 방식
- 조인 조건에 인덱스가 없거나 출력해야 할 결과 값이 많을 때 사용
- 대용량의 자료를 조인할 때 유리
- 범위 비교 연산자가 사용된 경우

### 해시 조인

- 조인될 두 테이블 중 하나를 해시 테이블로 선정하여 조인 될 테이블의 조인 키 값을 해시 알고리즘으로 비교하여 매치되는 결과값을 얻는 방식
- '=' 비교를 통한 조인에서만 사용될 수 있음
- 수행 빈도가 낮고 쿼리 수행시간이 오래 걸리는 많은 양의 데이터를 조인해야 하는 경우 주로 사용
- Sort 부하가 심할 때

<br>

# 🙌 JOIN 사용 시 고려해야 할 점

- JOIN의 효율성은 JOIN 하는 컬럼과 WHERE 절의 조건에 대한 인덱스에 크게 의존하기 때문에 인덱스를 사용하지 않거나 제대로 생성되지 않으면 JOIN 연산이 크게 느려질 수 있음
- INNER JOIN 의 성능이 LEFT JOIN 과 RIGHT JOIN 보다 좋다는 것을 고려하여 조인 유형 선택
- JOIN 의 대상이 되는 테이블의 크기가 크면 성능에 영향을 미치기 때문에 파티션 또는 샤딩 고려
- 쿼리 실행 계획 분석을 통해 쿼리 최적화

  <br>

> ❔샤딩 <br>
> 동일한 스키마를 가지고 있는 여러대의 데이터베이스 서버들에 데이터를 작은 단위로 나누어 분산 저장하는 기법 <br>
> 데이터베이스 차원의 수평 확장 (수평 파티셔닝의 일종) <br>
> 모든 데이터를 동일한 컴퓨터에 저장

<br>

> ❔파티셔닝 <br>
> 매우 큰 테이블을 여러개의 테이블로 분할하는 작업으로 큰 데이터를 여러 테이블로 나눠 저장하기 때문에 쿼리 성능이 개선될 수 있다. <br>
> 물리적으로는 여러 테이블로 분산하여 저장하지만 사용자는 마치 하나의 테이블에 접근하는 것과 같이 사용 가능 <br>
> 모든 데이터를 동일한 컴퓨터에 저장

<br>
