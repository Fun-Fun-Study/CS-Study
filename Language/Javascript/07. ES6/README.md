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

        var obj = { name: '짱구', species: 'human'};
        obj = { ...obj, age: 5};
        console.log(obj)
        // {name: "짱구", species: "human", age: 5}
        obj = { ...obj, name: '짱아', age: 11};
        console.log(obj);
        // {name: "짱아", species: "human", age: 11}

        ```

12. For/Of
13. Map Objects
14. Set Objects
15. Symbol
16. Array.from()
17. Array keys()
18. Array find()
19. Array findIndex()
20. New Math Methods
21. New Number Properties
22. New Number Methods
23. New Global Methods
24. Object entries

[Javascript ES6 참고](https://www.w3schools.com/js/js_es6.asp)
