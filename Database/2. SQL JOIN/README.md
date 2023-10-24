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

### 중첩 루프 조인

### 정렬 병합 조인

### 해시 조인

<br>

# 🙌 JOIN 사용 시 고려해야 할 점

- JOIN의 효율성은 JOIN 하는 컬럼과 WHERE 절의 조건에 대한 인덱스에 크게 의존하기 때문에 인덱스를 사용하지 않거나 제대로 생성되지 않으면 JOIN 연산이 크게 느려질 수 있음
- INNER JOIN 의 성능이 LEFT JOIN 과 RIGHT JOIN 보다 좋다는 것을 고려하여 조인 유형 선택
- JOIN 의 대상이 되는 테이블의 크기가 크면 성능에 영향을 미치기 때문에 파티션 또는 샤딩 고려
- 쿼리 실행 계획 분석을 통해 쿼리 최적화

  <br>

> ❔샤딩 <br>

<br>

> ❔파티셔닝 <br>

<br>

> ❔쿼리 실행 계획 분석 <br>
