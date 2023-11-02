## Scope

- 전역 스코프
  - 프로그램의 생애 주기와 동일한 스코프
  - HTML을 로딩한 후 페이지를 벗어나 새로고침 할 때까지의 주기
  - 모든 스코프의 최상위 스코프로 모든 지역 범위에서 참조 가능
  - 임의로 생성하거나 삭제 불가능
- 지역 스코프
  - 함수 스코프
    - 함수가 호출 될때 생성
    - 함수 안에서 생성된 모든 변수들은 함수가 실행되는 순간에 생성되며 함수가 종료되면 같이 소멸
    - 블록 내에서 변수를 var로 만들면 함수 스코프에 변수가 만들어짐
  - 블록 스코프
    - 블록 안에서 생성
    - if, while, for 등의 코드 블록으로 생성
    - let, const를 사용하여 변수 생성

### Case1

```javascript
//전역 스코프
var title = "A";

function displayTitle1() {
  //함수 스코프
  var title = "B";

  if (title) {
    //블럭 스코프
    let title = "C";
    console.log(title);
  }
  console.log(title);
}

function displayTitle2() {
  console.log(title);
}

displayTitle1();
displayTitle2();
```

Result

```
C
B
A
```

### Case2

```javascript
var days = ["월", "화", "수"];

for (var i = 0; i < days.length; i++) {
  console.log(days[i]);
}

console.log(i);

for (let j = 0; j < days.length; j++) {
  console.log(days[j]);
}

console.log(j);
```

Result

```
var를 변수로 가진 for문 안/밖의 console.log는 i의 값을 출력
let을 변수로 가진 for문 밖의 console.log는 블록 범위를 벗어나 오류가 발생함
```
