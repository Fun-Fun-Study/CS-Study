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
