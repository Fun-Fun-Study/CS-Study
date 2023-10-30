# JavaScript

> 자바스크립트는 싱글 스레드 기반이며 논 블로킹 방식의 비동기적인 동시성 언어이며 콜 스택, 이벤트 루프와 콜백 큐 그리고 여러가지 다른 API들을 가지고 있다
>
> [What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

## JavaScript 엔진과 런타임

### V8 엔진

- 오픈 소스 JavaScript 엔진 중 하나
- JavaScript와 WebAssembly 엔진이다.
- 크롬 웹 브라우저와 Node.js에서 사용하고 있다.
- V8은 JavaScript를 바이트코드로 컴파일하고 실행하는 방식을 사용한다.
- 구성
  - 하나의 힙과 하나의 콜 스택만 존재
  - setTimeout, DOM, AJAX 등의 **비동기 메소스 없음**

### JavaScript 런타임

- 런타임이란 프로그래밍 언어가 구동되는 환경을 말한다.
- JavaScript 런타임에는 웹브라우저와 Node.js가 있다.
- 웹 브라우저의 구성
  - setTimeout, DOM, AJAX 등의 **비동기 메소드**
  - **이벤트 루프와 콜백 큐**

## 자바스크립트는 싱글 스레드?

> **자바스크립트(엔진)**은 싱글 스레드이지만 **자바스크립트를 실행하는 런타임**은 완변한 싱글 스레드가 아니라고 할 수 있다.

- 자바스크립트 언어는 기본적으로 싱글 스레드로 작동
- 하지만 자바스크립트를 실행하는 런타임(웹 브라우저, Node.js)는 멀티 스레드로 작동할 수 있다.

### 싱글 스레드

- JavaScript는 전통적인 단일 스레드이다
- 멀티 코어여도 메인 스레드라는 단일 스레드에서만 작업
- 하나의 힙 영역과 하나의 콜 스택
- 동기적으로 처리

### 동기/비동기

- 작업 A, B, C를 진행할 때
- 동기
  - A 완료 후 B 시작, B 완료 후 C 시작
- 비동기
  - A 작업 시작 후 B, C 시작. 완료하는 데로 결과 반환
- 동기로 작업시 블로킹 발생 -> 요청의 처리가 느려짐

### JavaScript의 비동기

- 웹 브라우저의 Web APIs는 비동기 처리
  - setTimeout, DOM, AJAX
  - 이벤트 루프, 콜백 큐
- JavaScript 자체는 비동기 처리가 불가능 <- 런타임에서 지원하는 API를 통해 비동기 요청을 처리
- 비동기 콜백을 통해 싱글 스레드 프로그래밍 언어에서 블로킹을 해결함
  - 함수 호출 시 당장 실행하는 것(동기 -> 블로킹)이 아니라, 한곳에 쌓아두고 동시에 처리(비동기 -> 논블로킹)

## 이벤트 루프(Event Loop)

> 콜 스택과 콜백 큐를 주시하며 이벤트를 처리해주는 역할

JavaScript 런타임에서 비동기 처리를 하는 방법
![image](https://github.com/Fun-Fun-Study/CS-Study/assets/37894963/99080d4c-7bc2-4fc4-811c-3de5422d057b)

### Heap, Stack

- 우리가 잘 아는 그것
- 함수 실행시 Stack에 인수와 지역 변수가 포함된 프레임이 쌓임(콜 스택)
- Object 들은 Heap에 생성됨

### 콜백 큐

- 비동기 요청의 콜백은 Web API들을 통해 실행되고 그 결과가 콜백 큐에 들어감

### 이벤트 루프

- 이벤트 루프는 콜 스택과 콜백 큐를 주시하면서 콜 스택이 비면 콜백 큐에서 콜백을 가져와 콜 스택에 넣음
- 콜 스택에 들어간 함수들은 메인 스레드에서 실행된다.

![image](https://github.com/Fun-Fun-Study/CS-Study/assets/37894963/39527e11-8e85-4888-b49f-b2dbabdaf8f7)

### setTimeout

- setTimeout은 두개의 인자(콜백 함수와 시간)를 받는다
- 이때 시간은 **최소** 지연 시간으로 정확히 해당 시간이 지난 후에 실행되는 것을 보장하진 않는다
  ```javascript
  setTimeout(funtion(){
  console.log("timeout")
  }, 0) // 반드시 바로 실행 되지 않는다 <- 콜백 큐에 콜백 함수가 들어감
  ```
