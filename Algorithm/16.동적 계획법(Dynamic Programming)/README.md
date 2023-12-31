# Dynamic Programmingg(동적계획법)

#### 큰 문제를 작은 문제로 나누어 푸는 문제를 일컫는 것

#### 최적화 이론의 한 기술이며, 특정 범위까지의 값을 구하기 위해서 그것과 다른 범위까지의 값을 이용하여 효율적으로 값을 구하는 알고리즘 설계 기법 즉, <span style="color: skyblue">**특정 알고리즘이 아닌 문제 해결 패러다임**</span>

> 📌 Divide and Conquer(분할정복)와 다른 점은 작은 문제가 <span style="color: skyblue">**중복이 일어나는지 안 일어나는지**</span>. 작은 문제들이 반복되는 것을 풀어나가는 것이 동적 프로그래밍

## Dynamic Programming의 조건

- **_Overlapping Subproblems_** (겹치는 부분 문제)
  - 동일한 작은 문제들이 반복하여 나타나는 경우
- **_Optimal Substructure_** (최적 부분 구조)
  - 부분 문제의 최적 결과 값을 사용해 전체 문제의 최적 결과를 낼 수 있는 경우 <br>ex) A에서 X가 최적값이고, X에서 B가 최적값이면, A-X-B 도 최적<br>
    <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/9d582d4d-374e-494d-874d-4dd92b52816a">
- 특정 문제의 정답은 문제의 크기에 상관없이 항상 동일

## Dynamic Programming이 필요한 이유?

- 일반적인 재귀 방식과 유사하지만, 기존 방식은 동일한 문제, 동일한 결과를 여러 번 구하는 비효율적인 방식이 될 수 있음
- 이미 **결과를 구해놓은 계산은 다시 반복하지 않는 방식**으로 효율성을 개선하기 위해

<br>

## Dynamic Programming 저장 기법

### Memoization

> 📌 동일한 계산을 반복해야 하는 경우, 한 번 계산한 결과를 저장해 두었다가 후에 꺼내 쓰는 것

### Tabulation

> 📌 메모이제이션이 결과가 필요해질 때 계산한다면, 타뷸레이션은 필요하지 않은 값도 미리계산 (Eager-Evaluation)

<br>

## Dynamic Programming의 사용

### DP로 풀 수 있는 문제인지 확인

    - DP의 조건들이 충족되는 문제인지 체크
    - 보통 특정 데이터 내 최대화 / 최소화 계산을 하거나 특정 조건 내 데이터를 세야 한다거나 확률 등의 계산의 경우

### 문제의 변수 파악

    - 현재 변수에 따라 그 결과 값을 찾고 그것을 전달하여 재사용하는 과정을 위해, 문제 내 변수의 개수를 파악

### 변수 간 관계 식 만들기 (점화식)

    - 변수들에 의해 결과 값이 달라지지만 동일한 변수값인 경우 결과는 동일. 그 결과를 그대로 이용하기 때문에 관계식을 설정

### 메모하기 (Memoization or Tabulation)

    - 변수 간 관계식까지 정상적으로 생성되었다면 변수의 값에 따른 결과를 저장하고 필요할 때 사용

### 기저 조건 파악하기

    - 가장 작게 나눌 문제를 정의, 가장 작은 문제의 상태를 정의

<br>

## Dynamic Programming 구현 방법

### Bottom-Up

> 💡 아래에서부터 계산을 수행하고 누적시켜 전체 큰 문제를 해결하는 방식

- 반복을 통해 기저부터 하나씩 채우는 과정을 "table-filling" 하며, 이 Table에 저장된 값에 직접 접근하여 재활용하므로 Tabulation이라고 부름

### Top-Down

> 💡 위에서부터 호출을 시작하여 기저조건까지 내려간 다음, 해당 결과 값을 재귀를 통해 전이시켜 재활용하는 방식

- 이미 이전에 계산을 완료한 경우에는 단순히 메모해놨던 결과값을 사용. 그래서 가장 최근의 상태 값을 메모해 두었다고 하여 Memoization 이라고 부름
