## React Lifecycle [📎참고](https://dori-coding.tistory.com/entry/React-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4Lifecycle%EC%97%90-%EB%8C%80%ED%95%B4)

컴포넌트의 수명은 페이지에 렌더링 되기전인 준비과정에서 시작하여 페이지에서 사라질 때 끝난다.

- 마운트 → 업데이트(리렌더링) → 언마운트

1. **마운트**<br>

   - DOM이 생성되고 웹브라우저에 나타나는 것<br>
     <img width="245" alt="mount" src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/521a925a-08f6-49dc-8321-a80d09365f64">
     <br>

   * constructor: 컴포넌트를 새로 만들때 호출되는 클래스 생성자 메서드
   * getDerivedStateFromProps: props에 있는 값을 state에 넣을때 사용하는 메서드
   * render: 준비한 UI를 랜더링하는 메서드
   * componentDidMount: 컴포넌트가 웹 브라우저 상에 나타난 후 호출되는 메서드

<br>

2. **업데이트**

   - props가 바뀔 때
   - state가 바뀔 때
   - 부모 컴포넌트가 리랜더링 될 때
   - this.forceUpdate로 강제로 랜더링을 트리거 할 때
     <img width="384" alt="update" src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/1d27d782-59b0-4750-bab3-e90de92d8224">

   * getDerivedStateFromProps: props의 변화에 따라 state값에 변화를 주고 싶을 때 사용
   * shouldComponentUpdate: props나 state를 변경했을 때, 컴포넌트가 리랜더링을 해야할지 말아야할지 결정하는 메서드
   * getSnapshotBeforeUpdate: 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출되는 메서드
   * componentDidUpdate: 컴포넌트의 작업이 끝난 후 호출되는 메서드

<br>

3. **언마운트**
   - 컴포넌트를 DOM에서 제거하는 것<br>
     <img width="216" alt="unmount" src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/095614c0-3f6d-40ee-8151-b3e13c9fe4ef">
   * componentWillUnmount: 컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드

## Vue Lifecycle [📎참고](https://leeproblog.tistory.com/46)

vue의 인스턴스가 생성된 순간부터 종료될 때까지의 순환주기
라이프 사이클 단계마다 메서드를 사용해 개발자가 원하는 커스텀 로직을 수행할 수 있기 때문에 vue는 따로 Controller를 가지고 있지 않다.

<img height=1000 src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/0c04baa2-1257-4f82-aa8c-97d28d04780e">

Vue.js의 생명주기는 크게 4가지 Creation, Mounting, Updating, Destruction으로 나눌 수 있다

#### Creation

---

컴포넌트 초기화 단계로 컴포넌트들이 DOM에 추가되기 전 단계<br>

##### beforeCreate

- 가장 먼저 실행되는 훅
- data와 events가 세팅되지 않은 시점
- 데이터나 이벤트에 접근하려고하면 에러가 발생생

##### Created

- data와 event 활성화
- 템플릿과 Virtual DOM은 마운트 및 렌더링 되지 않은 상태

#### Mounting

---

초기 렌더링 직전에 컴포넌트에 직접 접근할 수 있는 단계<br>
초기 렌더링 직전에 DOM을 변경하고자한다면 이 단계를 활용<br>
컴포넌트 초기에 세팅되어야할 데이터 패치의 경우 Created 단계에서 마치는 것이 좋음

##### beforeMount

- 템플릿과 렌더 함수들이 컴파일 된 후, 첫 랜더링이 일어나기 전에 실행
- 대부분의 경우 사용하지 않는 것이 좋음
- 서버사이드 렌더링 시 호출 되지 않음

##### mounted

- 컴포넌트, 템플릿, 렌더링된 DOM에 접근 가능
- vue 라이브러리 외의 non-vue라이브러리를 통합하기 위해 DOM을 수정해야 할 때 사용
- 부모-자식 관계의 컴포넌트는 자식이 mounted가 완료 후에 부모 mounted가 실행 됨

<img width="676" alt="parent-child" src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/3e500a9a-dcb1-4976-9cca-b84bcfebf40d">

- Created : 부모 > 자식
- Mounted : 자식 > 부모
  - 부모의 mounted가 실행되었다고 모든 자식 컴포넌트가 mounted 상태라는 것을 보장하지 않음
  - this.$nextTick을 사용하여 모든 화면이 렌더링 후 실행하도록 할 수 있음

#### Updating

---

컴포넌트에서 사용되는 반응형 속성들이 변경되거나 재렌더링이 발생되면 실행<br>
디버깅이나 프로파일링을 위해 컴포넌트 재렌더링 시점을 알고 싶을 때 사용<br>
컴포넌트 반응형 속성이 언제 변경되는지 알아야하는 경우엔 Computed나 Watchers를 사용

##### beforeUpdate

- 컴포넌트의 데이터가 변해 업데이트 사이클이 시작될 때 실행
- DOM이 재 렌더링되고 패치되기 직전에 실행
- 재렌더링전의 새 상태의 데이터를 얻고 싶을 때 사용, 이 변경으로 인한 재렌더링은 발생하지 않음

##### updated

- 컴포넌트의 데이터 변경 후 재 렌더링이 일어난 후에 실행
- DOM 업데이트가 완료되 상태로 DOM에 종속적인 연산을 실행 할 수 있음
- 여기서 data를 변경하면 무한루프에 빠질 수 있음
- 모든 자식컴포넌트의 재렌더링 상태를 보장하지 않음

#### Destruction

---

구성요소가 해체되고 DOM에서 제거될 떄 실행<br>
컴포넌트 요소가 해체되었을 때 cleanup이나 분석 내용 전송등을 수행

##### beforeDestroy

- 뷰 인스턴트가 제거되기 직전에 호출
- 컴포넌트는 원래의 모습과 기능을 그대로 가지고 있는 상태
- 이벤트 리스너를 제거하거나 reactive subscription을 제거할 때 주로 사용
- 서버렌더링 시에 호출되지 않음

##### Destroyed

- 뷰 인스턴트가 제거된 후에 호출
- 모든 바인딩이 해제되고 모든 이벤트 리스너가 제거되며 하위 Vue 인스턴스도 제거
- 서버렌더링 시에 호출되지 않음

#### errorCaptured

---

자식 컴포넌트로부터 에러가 캡처되었을 때 호출<br>
오류가 발생한 컴포넌트 및 오류가 캡처된 위치에 대한 정보가 들어있는 정보를 받음

> [Vue 생명 주기 훅\_한글](https://ko.vuejs.org/guide/essentials/lifecycle.html) <br> [Vue 생명 주기 훅\_영문](https://vuejs.org/guide/essentials/lifecycle.html)
