### 해시는 해시(Hash), 해시 함수(Hash Function), 해싱(Hashing), 해시 테이블(Hash table)로 구분한다.

## 해시(Hash)

- 검색과 저장을 아주 빠르게하는 자료구조
- 데이터를 저장할 때 Key-Value형태로 데이터가 존재
- Key값이 배열의 인덱스로 저장되어 검색과 저장이 빠르게 일어남

## 해시 함수(Hash Function) & 해싱(Hashing)

- 해시 함수는 Key값을 고정된 길이의 Hash로 변환하는 역할
- 해시 충돌을 일으킬 확률을 최대한 줄이는 함수를 만드는 것이 중요
- **해싱(Hashing)** : Key값을 Hash로 변환하는 과정
- **해시 값(Hash Value), 해시 코드(Hash code)** : 해시 함수에서 Key값을 해싱 과정을 통해 나온 결과
- **해시 충돌(Hash Collision)** : 서로 다른 키가 같은 Hash되는 경우

## 해시 테이블(Hash table)

- 연관 배열구조를 이용하여 데이터를 Key와 Value로 저장하는 자료구조
- 해시 함수를 사용하여 index를 버킷(bucket)이나 슬롯(slot)의 배열로 계산

```
[연관 배열구조]
키 하나와 값 하나가 연관되어 있으며 키를 통해 연관되는 값을 얻을 수 있음
```

### 장점

- 중복 제거 가능
- 데이터 캐싱, 보안에 주로 사용
- 배열의 인덱스로 접근하기 때문에 삽입, 삭제 등의 연산이 빠름

### 단점

- 공간 복잡도가 커짐
- 충돌 발생 가능
- 순서가 있는 배열에는 어울리지 않음

## Hash Table vs Hash Map

- 병렬 처리를 하면서 자원의 동기화를 고려해야 하는 상황이라면 해시테이블을 사용
- 병렬 처리를 하지 않거나 자원의 동기화를 고려하지 않는 상황이라면 해시맵을 사용

```java
// HashMap
Map<Integer, String> map = new HashMap<>();
map.put(1, "one");
map.put(2, "two");

System.out.println(map.get(1)); // one
System.out.println(map.get(2)); // two

// Hashtable
Map<Integer, String> table = new Hashtable<>();
table.put(1, "one");
table.put(2, "two");

System.out.println(table.get(1)); // one
System.out.println(table.get(2)); // two
```

| Hash Map                   | Hash Table                         |
| -------------------------- | ---------------------------------- |
| null O                     | null X                             |
| 동기화 되어있지 않아 빠름  | 동기화되어 느림                    |
| Iterator클래스를 통해 탐색 | Iterator와 Enumeration을 통해 탐색 |
| AbstractMap 클래스 상속    | Dictionary클래스 상속              |
