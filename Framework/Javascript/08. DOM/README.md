## 문서 객체 모델(DOM, Document Object Model)

XML이나 HTML 문서에 접근하기 위한 일종의 인터페이스<br>
뷰 포트에 무엇을 렌더링 할지 결정하기 위해 사용<br>
웹페이지에서 자바스크립트로 요소들을 제어하는데 사용되는 Document Object Model<br>
문서 내의 모든 요소를 정의하고, 각각의 요소에 접근하는 방법을 제공<br>

텍스트 파일로 만들어져 있는 웹 문서를 브라우저에 렌더링하려면 웹 문서를 브라우저가 이해할 수 있는 구조로 메모리에 올려야 한다. 브라우저의 렌더링 엔진은 웹 문서를 로드한 후, 파싱하여 웹 문서를 브라우저가 이해할 수 있는 구조로 구성하여 메모리에 적재하는데 이를 DOM이라 한다. 즉 모든 요소와 요소의 어트리뷰트, 텍스트를 각각의 객체로 만들고 이들 객체를 부자 관계를 표현할 수 있는 트리 구조로 구성한 것이 DOM이다. 이 DOM은 자바스크립트를 통해 동적으로 변경할 수 있으며 변경된 DOM은 렌더링에 반영된다.

### DOM의 종류

1. Core DOM
   - 모든 문서 타입을 위한 DOM 모델
2. HTML DOM
   - HTML 문서를 위한 DOM 모델
   - HTML 문서를 조작하고 접근하는 표준화된 방법을 정의
   - 모든 HTML 요소는 HTML DOM를 통해 접근 가능
3. XML DOM
   - XML 문서를 위한 DOM 모델

### Critical Rendering Path [📎참고](https://bitsofco.de/understanding-the-critical-rendering-path/)

- 브라우저가 하나의 화면을 그려내는 과정
  <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/c67bc189-18d7-4a1e-bd9b-d37f7a92b3ef">
  1. HTML 데이터 파싱
     - url을 통해 서버로부터 HTML 문서를 받아와 파싱
  2. **DOM 트리 생성**
     - 완전하게 파싱된 HTML 페이지의 Object 표현
  3. CSSOM 트리 생성
     - DOM과 관련된 스타일의 Object 표현
  4. Javascript 실행
     - parser blocking resource
     - HTML 문서 자체의 파싱이 JavaScript에 의해 차단된다
  5. Render 트리 생성
     - DOM 과 CSSOM 이 합쳐진 것으로 페이지에서 최종적으로 렌더링할 내용을 나타내는 트리
  6. 레이아웃 생성
     - 뷰포트의 크기를 결정하며, 뷰포트의 크기는 뷰포트의 크기와 관련있는 CSS 스타일에 대한 컨텍스트를 제공
  7. 페인팅
     - 페이지의 내용을 픽셀로 변환하여 화면에 표시

### DOM의 구조

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/9c060964-c8ec-46c8-899a-9f092fbf9ac0">

- HTML 문서를 브라우저가 파싱하면 트리형식으로 구조가 반영
- Node : document, html, body, li와 같은 요소

### 상속 구조

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/f43c34f7-8bff-436e-ab96-0a5b09d7b49e">

- Documnet Node: HTML 문서 전체를 나타내는 노드
- Element Node : 모든 HTML 요소는 Element Node이며, 속성 노드를 가질 수 있는 유일한 노드

## 가상 DOM(Virtual DOM) [📎참고](https://velog.io/@woohm402/virtual-dom-and-react)

- Vue.js는 가상 DOM(Virtual DOM) 기반의 렌더링 시스템으로 빠른 렌더링 속도를 자랑한다.

- 가상 DOM은 실제 DOM의 복사본을 메모리 내에 저장하여 사용

- 수정이 될 때 마다 전체가 다시 렌더링 되어 속도의 단점이 있는 진짜 DOM과 달리, 가상 DOM은 변경될 때마다 진짜 DOM과 비교해서 차이를 찾아 그 부분만 수정하는 효율적인 동작을 하여 속도가 빠르다.

## 윈도우 객체 구조

<img src = "https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/f1114760-03cb-42d4-9b03-c13138811adc">

## 브라우저 객체 모델(BOM, Browser Object Model)

- Javascript가 브라우저와 소통하기 위해 만들어진 모델
- 모든 개별 객체들은 최상위 객체인 window 아래 존재

  - window
    - 최상위 객체
    - 프레임 별로 하나씩 존재
  - document
    - 현재 문서에 대한 정보 제공
  - location
    - url 주소 정보 제공
  - navigator
    - 브라우저의 정보 제공
  - screen
    - 외부 환경 정보 제공
  - history
    - 방문 기록 정보 제공

- Window 속성에 속하며, document문서가 아닌 window를 제어

> 참고<br>[브라우저는 어떻게 동작하는가?](https://d2.naver.com/helloworld/59361)<br>[문서 객체 모델(Document Object Model)](https://poiemaweb.com/js-dom)
