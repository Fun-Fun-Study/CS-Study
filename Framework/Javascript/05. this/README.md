# this

> this는 자신이 속한 객체 또는 자신이 생성한 인스턴스가 가리키는 자기 참조 변수이다.
>
> 자바스크립트의 함수에서 this는 호출 대상을 가리킨다.

- 함수의 호출 방식에 따라 바인딩할 객체가 동적으로 정해진다.

## this 바인딩

> 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. this 바인딩은 this와 this가 가리킬 객체를 바인딩하는 것이다.

- 자바나 C++ 같은 **클래스 기반 언어**에서 **this는 언제나 클래스가 생성하는 인스턴스**를 가리킨다.
- **자바스크립트의 this**는 **함수가 호출되는 방식**에 따라 this가 가리킨느 값이 **동적으로 결정**된다.
- 또한 **strict mode 역시 this 바인딩에 영향**을 준다.
- 함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프는 함수 정의가 평가되어 함수 객체가 생성되는 시점에 결정되지만 this 바인딩은 함수 호출 시점에 결정된다.
- 함수의 선언 위치와 상관없이 어디서 어떻게 호출하느냐에 따라 결정된다.

## 함수 호출 방법

- 함수의 호출 방법은 다양하다
  - 일반 함수 호출(기본 바인딩)
  - 메서드 호출(암시적 바인딩)
  - Function.prototype.apply/call/bind 메서드에 의한 간접 호출(명시적 바인딩)
  - 생성자 함수 호출(new 바인딩)
- this가 가리키는 것이 무엇인지 알기 위해서는 함수 선언이 아니라 **호출 지점**을 봐야한다.
  ```javascript
  function sayHi() {
    console.log("hi");
  }
  sayHi(); // 호출부
  ```

### 일반 함수 호출(기본 바인딩)

- 기본적으로 this에는 전역 객체가 바인딩된다.
- 브라우저에서는 window, Node.js에서는 global을 가리킨다.
  ```javascript
  function foo() {
    console.log(this); // window
    function bar() {
      console.log(this); // window
    }
    bar();
  }
  foo();
  ```
- 만약 strict mode인 경우 일반 함수 의 this는 undefined가 된다.

  ```javascript
  function foo() {
    "use strict";
    console.log(this); // undefined
  }
  foo();
  ```

  #### 콜백 함수 호출 시 그 함수 내부에서의 this

  - 콜백 함수 내부의 this는 콜백 함수의 제어권을 가지는 함수가 결정한다.

    ```javascript
    setTimeout(function () {
      console.log(this); // window;
      // 콜백 함수가 일반 함수로 호출되었으므로 전역 객체가 바인딩된다.
    }, 300);

    [1, 2, 3, 4, 5].forEach(num => {
      console.log(this, num); // window, num;
    });

    document.body.querySelector("#id").addEventListener("click", function(e)) {
      console.log(this, e); // "#id" 엘리멘트와 클릭 이벤트에 대한 객체
    };
    ```

### 메서드 호출(암시적 바인딩)

- 메서드 내부의 this에는 호출한 주체에 대한 정보가 담긴다.
- 메서드로 호출한 경우 호출 주체는 함수명 앞의 객체이다.
- `obj.method()`의 경우 method의 this는 obj를 가리킨다.
- 함수를 호출하는 구문 앞에 점(.) 혹은 대괄호([]) 표기가 있다면 메서드 호출이다.
  ```javascript
  const obj = {
    outer: function () {
      console.log(this);
      const inner = function () {
        console.log(this); // 일반 함수 실행 -> 전역객체 window
      };
      inner();
    },
  };
  obj.outer(); // 메서드 호출 -> obj
  ```

### Function.prototype.apply/call/bind 메서드에 의한 간접 호출(명시적 바인딩)

- 암시적 바인딩의 경우 콜백 함수 등의 이유로 this의 바인딩을 예측하기 어렵다.
- this를 명시적으로 고정하는 방법

  #### call 메서드

  ```javascript
  func.call(thisArg[, arg1[, arg2[, ...]]])
  ```

  - call 메서드는 호출 주체인 함수를 즉시 실행하는 명령
  - 첫번째 인자를 this로 바인딩하고 이후 인자를 매개변수로 사용
  - call을 이용하여 구체적인 객체를 this로 지정할 수 있다.
    ```javascript
    function foo() {
      console.log(this.a);
    }
    const obj = { a: 2 };
    // 명시적으로 obj를 바인딩
    foo.call(obj); // 2
    foo(obj); // undefined
    ```

  #### apply 메서드

  ```javascript
  func.apply(thisArg, [argsArray]);
  ```

  - call()과 기능적으로 유사
  - 입력으로 인수들의 **배열**을 받는다.

    ```javascript
    function foo(a, b, c) {
      console.log(this, a, b, c);
    }
    const obj = { a: 2 };

    foo.call(obj, 4, 5, 6); // {a: 2} 4 5 6
    // apply는 두번째 인자로 함수 인수들의 배열을 받는다.
    foo.apply(obj, [4, 5, 6]); // {a: 2} 4 5 6
    ```

  - 유사배열객체에 배열 메서드를 사용하고 싶을 때 이용

    ```javascript
    const obj = {
      0: "hi",
      1: "hello",
      length: 2,
    };

    Array.prototype.push.call(obj, "hey");
    // [].push.call(obj, 'hey') 이렇게 써도 동일하다.
    console.log(obj); // { '0': 'hi', '1': 'hello', '2': 'hey', length: 3 }
    ```

  #### bind 메서드

  ```javascript
  func.bind(thisArg[, arg1[, arg2[, ...]]])
  ```

  - apply, call과 달리 함수를 호출하지 않음 -> this와 입력된 인자를 지정하여 새로운 함수를 생성

    ```javascript
    function foo() {
      console.log(this);
    }
    const obj = { a: 2 };

    foo.call(obj); // { a: 2 }
    foo.apply(obj); // { a: 2 }
    // 똑같이 bind로 바꾸면 함수를 호출하지 않는 걸 알 수 있다.
    foo.bind(obj); // ƒ bound foo()
    // 명시적으로 실행을 추가해주어야 한다.
    foo.bind(obj)(); // { a: 2 }
    ```

  - bind는 메서드 내부의 중첩 함수 또는 콜백 함수의 this가 일치하지 않는 문제를 해결할 수 있다.
    ```javascript
    const person = {
      name: "edie",
      foo(callback) {
        setTimeout(callback.bind(person), 100);
      },
    };
    person.foo(function () {
      console.log(`hi, i'm ${this.name}`); // "hi, i'm edie"
    });
    ```

### 생성자 함수 호출(new 바인딩)

- 함수를 new와 함께 호출하면 생성자로 동작한다.
- 생성자 함수로 호출된 경우 this는 새로 만들어진 인스턴스 자신이 된다.

  ```javascript
  function Toy(make, model, year) {
    // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
    console.log(this); // Toy { __proto__: { constructor: ƒ Toy() } }

    // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
    this.make = make;
    this.model = model;
    this.year = year;
    this.getAge = function () {
      return new Date().getFullYear() - this.year + 1;
    };
    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
  }

  // 4. 인스턴스 생성. Toy 생성자 함수는 암묵적으로 this를 반환한다.
  const woody = new Toy("PIXAR", "cowboy", 1995);
  console.log(woody);
  // Toy {
  //   make: 'PIXAR',
  //   model: 'cowboy',
  //   year: 1995,
  //   getAge: ƒ (),
  //   __proto__: { constructor: ƒ Toy() }
  // }
  console.log(woody.year); // 'PIXAR'
  console.log(woody.getAge()); // 27
  ```

- 생성자 함수 내부에서 this가 아닌 값을 반환하는 경우 생성자 함수의 동작에 이상이 생길 수 있다.

## this 바인딩 예외

### 화살표 함수

- 화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다.
- ES6의 화살표 함수는 일반적인 바인딩 규칙을 무시하고 렉시컬 스코프로 this를 바인딩한다.
- **화살표 함수 내부의 this는 상위 스코프의 this(=== "lexical this")**
- 화살표 함수가 중첩된 경우 this는 가장 바깥이 화살표 함수가 아닌 함수의 this가 된다.
- 따라서 메서드를 정의하거나 프로토타입 객체의 프로퍼티에 함수를 할당하는 경우에 화살표 함수를 사용하는 경우 문제가 생길 수 있다.

### 별도의 인자로 this를 받는 경우(thisArg)

- 콜백 함수를 인자로 받는 메서드 중 일부는 this를 지정할 객체(thisArg)를 지정할 수 있는 경우가 있다.
- 이 경우 콜백함수 내부에서 this값을 원하는 대로 지정할 수 있다.
- 배열 메서드(forEach, map, filter, some, every, find, findIndex, flatMap ...)
- Set과 Map의 일부 메서드(forEach)

  ```javascript
  const report = {
    sum: 0,
    count: 0,
    add: function () {
      const args = Array.prototype.slice.call(arguments);
      args.forEach(function (entry) {
        this.sum += entry;
        ++this.count;
        // this를 thisArg로 넣어주었다.
      }, this);
    },
  };

  report.add(2, 4, 6);
  console.log(report.sum, report.count); // 12 3
  ```

### call, apply, bind에 첫번째 인자로 null|undefined를 넘기는 경우

- this 바인딩이 무시되고 기본 바인딩 규칙이 적용된다.

## 바인딩 우선 순위

1. new
2. call, apply, bind
3. 콘텍스트 객체로 호출된 경우
4. 기본 바인딩
