## ECMAScript6 (ES6)

ECMA International라는 국제기구에서 만든 표준 문서인 ECMAScript의 6번째 개정판 문서에 있는 표준 스펙

- 코드가 간결해지고 생산성이 향상됨
- IE9 부터 지원

> ECMA : European Computer Manufacturers Association

### 주요기능

1.  키워드 let, const

    - 블록 스코프
    - let : 가변 변수, 재정의 가능, 재선언 불가능
    - const : 불변 변수, 재정의/재선언 불가능
    - var의 문제점
      - 변수 선언이 유연해 예기치 못한 값을 반환할 수 있음
      - 코드가 길어지면 어디서 사용되는지 파악하기 어려움
      - 변수 선언문 이전에 변수를 참조하면 undefined 반환(Hoisting)

2.  Template Literals

    - `(백틱)을 사용하는 새로운 문자열 표기법
    - 줄바꿈, ${}를 통한 표현식 사용 가능

    ```javascript
    let name = "heelee";
    let str = `Hello ${name}`;
    let str = `asdhasfhfsahsfhfshasfhsfahsfahsfahasfh
    mxmxmxmxmxmxmxmmxmxmxmxmxmmxmxmxmxmxm`;
    ```

3.  Arrow Functions

    - 함수 표현식을 단순하고 간결하게 작성하는 문법

    ```javascript
    //ES5
    let sum = function (a, b) {
      return a + b;
    };

     //ES6 Arrow Function
    let sum = (a+b) => {return a+b;}
    let sum = (a, b) => a + b;
    ```

4.  Class

    - class 키워드를 사용해서 선언
    - 객체를 생성하기 위한 템플릿
    - 블록 스코프에 선언
    - let, const와 같은 Hoisting 동작 방식
    - `#`키워드를 작성하면 Private Property가 되며, 외부 접근이 불가능
    - super을 사용하여 상속과 오버라이딩 수행

    ```javascript
    class Person {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }
      nextYearAge() {
        // 메서드 생성
        return Number(this.age) + 1;
      }
    }

    // 클래스 상속
    class introducePerson extends Person {
      constructor(name, age, city, futureHope) {
        // super 키워드를 이용해서 자식 class에서 부모 메서드를 호출
        super(name, age, city);
        this.futureHope = futureHope;
      }
      introduce() {
        return `저는 ${this.city}에 사는 ${this.name} 입니다.
         내년엔 ${super.nextYearAge()}살이며,
         장래희망은 ${this.futureHope} 입니다.`;
      }
    }

    let kim = new introducePerson("kim", "23", "seoul", "개발자");
    console.log(kim.introduce());
    ```

5.  Promise

    - 비동기 처리에 사용되는 객체
    - [참고\_Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

6.  JavaScript Modules(import/export)

    - 세부사항은 캡슐화 시키고, API 부분만 외부에 노출시킨 코드
    - ES5 까지는 require을 통해 모듈화
    - ES6 부터는 import/export로 모듈을 관리

    ```javascript
    import moduleName from 'filePath';
    import {moduleName1,moduleName2, ...} from 'filePath';
    import * as newName from 'filePath';
     // newName.methods();


    export default moduleName;
    export const i = 10;
    export funtion multi(x){}
    export default class exam{}
    ```

7.  String Method (includes, startsWith, endsWith)

    - Boolean 타입 return
    - 문자열이 포함되어있는지, 시작하는지, 끝나는지

    ```javascript
    const str = "Hello World Hanamon";
    str.includes("Hana"); // true
    str.startsWith("Hello"); // true
    str.endsWith("mon"); // true
    ```

8.  Default Parameters

    - 함수 선언 시 매개변수에 Default값 지정

    ```javascript
    const myFn = (a = 100, b = 200) => a + b;
    ```

9.  Destructing(구조 분해 할당)

    - 객체와 배열의 값을 쉽게 변수로 저장
    - 객체

      - 중괄호를 사용해 같은 key이름을 사용
      - key와 다른 이름으로 꺼낼 때는 변수이름: 키 값을 사용

      ```javascript
      const introduce = { name: "unknown", age: 23 };
      // key와 같은 이름으로 변수 선언
      const { name, age } = introduce;
      // 다른 이름으로 변수 선언 -> 변수이름: 키값
      const { myName: name, myAge: age } = introduce;

      console.log(myName); // unknown
      console.log(myAge); // 23
      ```

    - 배열

      - 대괄호를 사용하여 순차적으로 꺼냄

      ```javascript
      const fruits = ["apple", "mango", "grape"];
      // 앞에서부터 순차적으로 변수 선언 가능
      const [zero, one, two] = fruits;

      console.log(zero); // apple
      ```

10. Rest Parameter(나머지 매개변수)

    - 나머지 후속 매개변수들을 묶어 하나의 배열에 저장해서 사용
    - 묶어줄 매개변수 앞에 ...을 붙여 작성
    - 배열과 함수의 인자 중 나머지를 가리키며, 객체의 나머지 필드를 가리킴
    - 함수 정의에는 하나의 ...만 존재
    - 반드시 마지막 매개변수여야 함

    ```javascript
    // args에 1,2,3,4,5가 한꺼번에 배열로 담겨 인자로 넘겨진다.
    function func1(...args) {
      console.log(`args: [${args}]`);
      // args: [1,2,3,4,5]
    }
    func1(1, 2, 3, 4, 5);

    // arg1에는 1, arg2에는 2, arg3에는 나머지 3,4,5가 배열로 담겨 인자로 넘겨진다.
    function func2(arg1, arg2, ...arg3) {
      console.log(`arg1: ${arg1}, arg2: ${arg2}, arg3: [${arg3}]`);
      // arg1: 1, arg2: 2, arg3: [3,4,5]
    }
    func2(1, 2, 3, 4, 5);
    ```

11. Spread Operator(전개 구문)

    - 묶인 배열 혹은 객체를 개별적 요소로 분리
    - 매개변수 앞에 ...을 붙여서 작성
    - 순서에 따라 값이 변경될 수 있어 작성 순서에 주의

    ```javascript
    let arr = [1, 2, 3, 4, 5];
    console.log(...arr);
    // 1 2 3 4 5

    var str = "javascript";
    console.log(...str);
    // "j" "a" "v" "a" "s" "c" "r" "i" "p" "t"

    var obj = { name: "짱구", species: "human" };
    obj = { ...obj, age: 5 };
    console.log(obj);
    // {name: "짱구", species: "human", age: 5}
    obj = { ...obj, name: "짱아", age: 11 };
    console.log(obj);
    // {name: "짱아", species: "human", age: 11}
    ```

12. For/Of
    - 반복 가능한 객체의 값을 반복한다.
    - 배열, 문자열, 맵, NodeList 등
    - For/In 과의 차이점
      - For/In: 열거 가능한 속성을 반복
      - For/Of: 이터러블 객체(Symbol.iterator 속성을 가지는 객체)
    ```javascript
    const languages = ["Java", "C", "Python"];
    for (let lang of languages) {
      console.log(lang);
    }
    // Java
    // C
    // Python
    ```
13. Map Objects
    - Java의 Collections의 Map과 같은 역할
    ```javascript
    const myMap = new Map([
      ["a", 1],
      ["b", 2],
    ]);
    myMap.set("c", 3);
    console.log(myMap.get("a")); // 1
    myMap.set("a", 100);
    console.log(myMap.get("a")); // 100
    ```
14. Set Objects

    - Java의 Collections의 Set과 같은 역할

    ```javascript
    const mySet = new Set();
    mySet.add(1);
    mySet.add(2);
    mySet.add(3);
    mySet.size; // 3
    mySet.add(3);
    mySet.size; // 3

    mySet.has(1); // true
    mySet.has(100); // false

    mySet.delete(3);
    mySet.has(3); // false
    ```

15. Symbol

    - 원시 타입(primative)
    - 다른 코드가 접근할 수 없는 숨겨진 식별자를 의미
    - 고유한 식별자를 생성

    ```javascript
    const sym1 = Symbol();
    const sym2 = Symbol("id");
    const sym3 = Symbol("id");

    sym2 === sym3; // false
    ```

16. Array.from()
    - 순회 가능 또는 유사 배열 객체에서 얕은 복사로 새로운 Array를 생성하는 함수
    - `Array.from(arrayLike [, mapFn])`
    - 배열 등 이나 문자열을 넣을 수 있음
    - mapFn으로 각 배열에 map 함수를 적용한 결과물을 얻을 수도 있음
    ```javascript
    Array.from("ABCD"); // ["A", "B", "C", "D"]
    Array.from([1, 2, 3], (x) => x + 1); // [2, 3, 4]
    ```
17. Array keys()
    - 배열의 각 인덱스를 키 값으로 가지는 새로운 `Array Interator` 객체를 반환하는 함수
    ```javascript
    const arr = ["a", "b", "c"];
    const iter = arr.keys();
    for (const key of iter) {
      console.log(key);
    }
    // 0
    // 1
    // 2
    ```
18. Array find()
    - 배열 안에서 테스트 함수를 만족하는 첫번째 요소를 반환하는 함수
    - 만약 테스트를 만족하는 값이 없다면 undefined를 반환
    ```javascript
    const arr = [5, 12, 8, 130, 44];
    arr.find((x) => x > 10); // 12
    ```
19. Array findIndex()
    - find와 같지만 값이 아니라 인덱스를 반환하는 함수
    - 테스트를 만족하는 요소가 없다면 -1을 반환
    ```javascript
    const arr = [5, 12, 8, 130, 44];
    arr.findIndex((x) => x > 10); // 1
    ```
20. New Math Methods

    - Math.trunc()
      - 실수의 정수 부분만 반환
    - Math.sign()
      - 양수인지 음수인지 반환
    - Math.cbrt()
      - 세제곱근을 반환
    - Math.log2()
      - 밑이 2인 로그 값을 반환
    - Math.log10()
      - 밑이 10인 로그 값을 반환

    ```javascript
    Math.trunc(3.14) // 3

    Math.sign(-10) // -1
    Math.sign(0) // 0
    Math.sign(4) // 1

    Math.cbrt(8) // 2

    Math.log2(4) = 2

    Math.log10(1000) = 3
    ```

21. New Number Properties
    - Number.EPSILON
      - 2.220446049250313e-16
    - Number.MIN_SAFE_INTEGER
      - -9007199254740991 <- $-(2^{53}-1)$
    - Number.MAX_SAFE_INTEGER
      - 9007199254740991 <- $2^{53}-1$
22. New Number Methods

    - Number.isInteger()
      - 정수 여부를 판단
    - Number.isSafeInteger()
      - safe한 정수인지 판단
      - $-(2^{53}-1) \leq x \leq 2^{53}-1$

    ```javascript
    Number.isInteger(10); // true
    Number.isInteger(10.5); // false

    Number.isSafeInteger(10); // true
    Number.isSafeInteger(12345678901234567890); // false
    ```

23. New Global Methods

    - isFinite()
      - 유한 값인지 판단
      - 정확히는 `Infinity`나 `NaN`이 아닌 경우 true 반환
    - isNaN()
      - `NaN`인지 판단

    ```javascript
    isFinite(10 / 0); // false
    isFinite(10 / 1); // true

    isNaN("hi"); // true
    ```

24. Object entries

    - key, value 쌍으로 이루어진 Array Iterator를 반환
    - 순서를 보장하지 않으므로 필요한 경우 정렬해서 사용해야함
      - `Obejct.entries(obj).sort((a, b) => b[0].localCompare(a[0]))`

    ```javascript
    const obj = { a: "string", b: 52 };
    for (const [key, value] of Object.entries(obj)) {
      console.log(`${key}: ${value}`);
    }
    // a: string
    // b: 52
    ```

[Javascript ES6 참고](https://www.w3schools.com/js/js_es6.asp)
