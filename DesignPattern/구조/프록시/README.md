## Proxy Pattern

![프록시](https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/e5aca8af-c9c3-4b67-937e-187515958c55)

- Proxy: 대리, 대리인
- 클라이언트가 사용하는 실제 서비스 객체를 대신하는 객체를 제공하는 구조적 디자인 패턴
- 클라이언트 요청을 수신하고 일부 작업(액세스 제어, 캐싱 등)을 수행한 다음 요청을 서비스 객체에 전달
- 어떤 작업의 실행을 대리인을 통해 실행하도록 하는 패턴
- Proxy는 실제 객체와 클라이언트 사이에 존재
- Object를 사전참조하면서 높은 비용의 작업을 지연시킬 수 있음
- SubjectObject 코드를 수정하지 않고 기능을 추가할 수 있음

### 적용 사례

- Access Control / Validation
- Caching / Logging
- Debit / Check Card
- 원격 서비스의 로컬 실행
- 리소스가 무거운 객체의 지연초기화
- @Transaction
- Youtube 썸네일

### 구성요소

- Client
- Subject (like interface)
- Proxy
- Real Subject

```typescript
//Subject 인터페이스
interface Payment {
  request(amount: number): void;
}

//Real Subject 실제 객체
class Cash implements Payment {
  request(amount: number) {
    //로직써있다치고
    console.log(`결제 요청 완료.. 금액: ${amount}`);
  }
}

const targetObject = new Cash();

//Proxy
//const proxy = new Proxy(target, handler);
const paymentProxy = new Proxy(targetObject, {
  get: (object, prop) => {
    if (prop === "request") {
      return object[prop];
    }
    throw new Error("operation not implemented");
  },
});

paymentProxy.request(100);
paymentProxy.add(100); // 에러 발생 - 프록시로 전달 받은 오퍼레이션이 실질적인 객체(Cash)에 없기때문
```

### 장점

- 사이즈가 큰 객체가 로딩되기 전에도 프록시를 통해 참조 가능
- 실제 객체의 public, protected 메소드를 숨기고 인터페이스를 통해 노출 시킬 수 있음
- 원래 객체의 접근에 대해 사전처리 가능

### 단점

- 객체 생성 시 한 단계가 추가되어 빈번한 객체 생성 시 성능 저하 발생
- 프록시 내부에 객체 생성을 위해 스레드가 생성, 동기화가 필요한 경우 성능 저하 발생
