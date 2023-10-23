# 🙌 SQL JOIN

    둘 이상의 테이블을 연결해서 데이터를 검색하는 방법 <br>
    연결을 위해서 테이블은 적어도 하나의 컬럼을 공유하고 있어야 하며 공유하고 있는 컬럼을 PK 혹은 FK로 서용

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
