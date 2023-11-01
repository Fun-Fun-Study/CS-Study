# Promise

> 자바스크립트에서 비동기 처리에 사용하는 객체
>
> 특정 코드의 실행이 완료되어 결과를 줄 것이라고 약속하는 객체

## 프로미스의 3가지 상태(state)

- 프로미스의 처리 과정
- `new Promise()`로 프로미스를 생성하고 종료될 때까지 3가지 상태를 가짐
  - Pending(대기): 비동기 처리 로직이 아직 완료되지 않은 상태
  - Fulfilled(이행): 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
  - Rejected(실패): 비동기 처리가 실패하거나 오류가 발생한 상태

### Pending(대기)

- 새로운 프로미스를 생성했을 때의 초기 상태
- `new Promise` 메서드에 resolve와 reject를 인자로 받는 콜백 함수를 선언할 수 있다.
  ```javascript
  new Promise(function (resolve, reject) {
    // ...
  });
  ```

### Fulfilled(이행)

- 콜백 함수의 인자 resolve를 실행하면 이행 상태가 된다.
  ```javascript
  new Promise(function (resolve, reject) {
    resolve();
  });
  ```
- 이행 상태가 되면 then()을 이용해 처리 결과를 받을 수 있다.
  ```javascript
  function getDate() {
    return new Promise(function (resolve, reject) {
      var date = 100;
      resolve(data);
    });
  }
  // resolve()의 결과 값 data를 resolvedData로 받음
  getData().then(function (resolvedData) {
    console.log(resolvedData);
  });
  ```
- 이행 = 완료 라고 볼 수 있음

### Rejected(실패)

- 콜백 함수의 reject를 호출하면 실패(Rejected) 상태가 된다.
  ```javascript
  new Promise(function (resolve, reject) {
    reject();
  });
  ```
- 실패 상태가 되면 실패한 이유를 catch()로 받을 수 있다.
  ```javascript
  function getDate() {
    return new Promise(function (resolve, reject) {
      reject(new Error("Request is failed"));
    });
  }
  // reject()의 결과 값 Error을 err에 받음
  getData()
    .then()
    .catch(function (err) {
      console.log(err);
    });
  ```

![image](./image.svg)

### 예제

```javascript
function getData() {
  return new Promise(function (resolve, reject) {
    $.get("url 주소/products/1", function (response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData()
  .then(function (data) {
    console.log(data); // response 값 출력
  })
  .catch(function (err) {
    console.error(err); // Error 출력
  });
```

## 프로미스 체이닝

> 여러 개의 프로미스를 연결하여 사용하는 것을 프로미스 체이닝이라고 한다.

- 프로미스 객체의 메서드 함수 then과 catch의 반환 값은 다시 프로미스 객체임
- 따라서 메서드 함수 then과 catch를 연결해서 사용할 수 있다.
- then, catch에서 사용할 수 있는 결과값은 함수안의 콜백에 인자로 받아야한다.

```javascript
function getData() {
  return new Promise({
    // ...
  });
}
// then() 으로 여러 개의 프로미스를 연결한 형식
getData()
  .then(function (data) {
    // ...
  })
  .then(function () {
    // ...
  })
  .then(function () {
    // ...
  });
```

## 프로미스의 에러 처리 방법

- then 메서드의 두번째 인자를 사용하는 방법
  ```javascript
  getData().then(handleSuccess, handleError);
  ```
- catch 메서드를 이용하는 방법
  ```javascript
  getData().then().catch();
  ```

```javascript
function getData() {
  return new Promise(function (resolve, reject) {
    reject("failed");
  });
}
// 1. then()의 두 번째 인자로 에러를 처리하는 코드
getData().then(
  function () {
    // ...
  },
  function (err) {
    console.log(err);
  }
);
// 2. catch()로 에러를 처리하는 코드
getData()
  .then()
  .catch(function (err) {
    console.log(err);
  });
```

- 프로미스 에러 처리는 가급적 catch를 사용해야한다.

  - then으로 처리하는 경우 감지하지 못하는 에러가 있다.
  - then 안에서 발생한 에러를 감지하지 못함

    ```javascript
    // then()의 두 번째 인자로는 감지하지 못하는 오류
    function getData() {
      return new Promise(function (resolve, reject) {
        resolve("hi");
      });
    }

    getData().then(
      function (result) {
        console.log(result);
        throw new Error("Error in then()"); // Uncaught (in promise) Error: Error in then()
      },
      function (err) {
        console.log("then error : ", err);
      }
    );
    ```

- catch 사용 시 정상 처리됨

  ```javascript
  // catch()로 오류를 감지하는 코드
  function getData() {
    return new Promise(function (resolve, reject) {
      resolve("hi");
    });
  }

  getData()
    .then(function (result) {
      console.log(result); // hi
      throw new Error("Error in then()");
    })
    .catch(function (err) {
      console.log("then error : ", err); // then error :  Error: Error in then()
    });
  ```
