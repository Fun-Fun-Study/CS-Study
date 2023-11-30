## CSR || SSR

> CSR : Client Side Rendering <br>
> SSR : Server Side Rendering <br>

##### SPA(Single Page Applictaion)

> 최초 한 번 페이지 전체를 로딩한 뒤, 데이터만 변경하여 사용할 수 있는 애플리케이션

SPA는 기본적으로 페이지 로드가 없고, 모든 페이지가 단순히 Html5 History에 의해 렌더링된다.

<br>

기존의 전통적 방법인 SSR 방식에는 성능 문제가 있었다.

요즘 웹에서 제공되는 정보가 워낙 많다. 요청할 때마다 새로고침이 일어나면서 페이지를 로딩할 때마다 서버로부터 리소스를 전달받아 해석하고, 화면에 렌더링하는 방식인 SSR은 데이터가 많을 수록 성능문제가 발생했다.

```
현재 주소에서 동일한 주소를 가리키는 버튼을 눌렀을 때,
설정페이지에서 필요한 데이터를 다시 가져올 수 없다.
```

이는, 인터랙션이 많은 환경에서 비효율적이다. 렌더링을 서버쪽에서 진행하면 그만큼 서버 자원이 많이 사용되기 때문에 불필요한 트래픽이 낭비된다.

<br>

CSR 방식은 사용자의 행동에 따라 필요한 부분만 다시 읽어온다. 따라서 서버 측에서 렌더링하여 전체 페이지를 다시 읽어들이는 것보다 빠른 인터렉션을 기대할 수 있다. 서버는 단지 JSON파일만 보내주고, HTML을 그리는 역할은 자바스크립트를 통해 클라이언트 측에서 수행하는 방식이다.

<br>

뷰 렌더링을 유저의 브라우저가 담당하고, 먼저 웹앱을 브라우저에게 로드한 다음 필요한 데이터만 전달받아 보여주는 CSR은 트래픽을 감소시키고, 사용자에게 더 나은 경험을 제공할 수 있도록 도와준다.

<br>

<br>

#### CSR 장단점

- ##### 장점

  - 트래픽 감소

    > 필요한 데이터만 받는다

  - 사용자 경험

    > 새로고침이 발생하지 않음. 사용자가 네이티브 앱과 같은 경험을 할 수 있음

- ##### 단점

  - 검색 엔진

    > 크롬에서 리액트로 만든 웹앱 소스를 확인하면 내용이 비어있음. 이처럼 검색엔진 크롤러가 데이터 수집에 어려움이 있을 가능성 존재
    >
    > 구글 검색엔진은 자바스크립트 엔진이 내장되어있지만, 네이버나 다음 등 검색엔진은 크롤링에 어려움이 있어 SSR을 따로 구현해야하는 번거로움 존재

<br>

#### SSR 장단점

- ##### 장점

  - 검색엔진 최적화

  - 초기로딩 성능개선

    > 첫 렌더링된 HTML을 클라이언트에서 전달해주기 때문에 초기로딩속도를 많이 줄여줌

- ##### 단점

  - 프로젝트 복잡도

    > 라우터 사용하다보면 복잡도가 높아질 수 있음

  - 성능 악화 가능성

<br>

<br>

## SPA || MPA

<br>

<br>

### SPA vs MPA

> - SPA(Single Page Application)는 한 개(Single)의 Page로 구성된 Application이다.
> MPA(Multiple Page Application)는 여러 개(Single)의 Page로 구성된 Application이다.
> MPA는 새로운 페이지를 요청할 때마다 정적 리소스가 다운로드된다. 매번 전체 페이지가 다시 렌더링 된다.
반면 SPA는 웹 에플리케이션에 필요한 모든 정적 리소스를 최초 한 번에 다운로드한다.
그 이후 새로운 페이지 요청이 있을 때, 페이지 갱신에 필요한 데이터만 전달 받아서 페이지를 갱신한다.
> 

<br>

<br>

### SPA (Single Page Application)
> 한개의 Page로 구성된 Application이다.<br>
> SPA는 CSR방식으로 렌더링한다.<br>
> 단 한 번만 리소스를 로딩한다. 이후 데이터를 받아올 때만 서버와 통신한다.<br>
> 이를 클라이언트 관점에서 말하자면 최초 페이지를 로딩한 시점부터는 페이지 리로딩 없이 필요한 부분만 서버로 부터 받아서 화면을 갱신하는 것이다. <br>
> 필요한 부분만 갱신하기 때문에 네이티브 앱에 가까운 자연스러운 페이지 이동과 사용자 경험(UX)을 제공할 수 있다.

![alt](https://i0.wp.com/hanamon.kr/wp-content/uploads/2021/03/SPA.png?resize=768%2C415&ssl=1)

#### 장점
1. 자연스로운 사용자 경험(UX) : 페이지의 깜박거림이 없다.
2. 필요한 리소스만 부분적으로 로딩
3. 서버의 템플릿 연산을 클라이언트로 분산
4. 컴포넌트별 개발 용이(개발 생산성 증가)
5. 모바일 앱과 동일한 API를 사용하도록 설계가 가능하다.

#### 단점
1. JavaScript 파일을 번들링해서 한 번에 받기 때문에 초기 구동 속도가 느리다.
2. 검색엔진최적화가 어렵다. 
3. CSR을 통해 클라이언트측의 쿠키말고는 사용자에 대한 정보를 저장할 공간이 없다.


<br>

<br>

### MPA (Mulitple Page Application)
> 여러 개의 Page로 구성된 Application이다. <br>
> MPA는 SSR 방식으로 렌더링한다. <br>
> 새로운 페이지를 요청할 때마다 서버에서 렌더링된 정적 리소스(HTML,CSS,JavaScript)가 다운로드된다.<br>
> 페이지 이동하거나 새로고침하면 전체 페이지를 다시 렌더링한다.
![alt](https://i0.wp.com/hanamon.kr/wp-content/uploads/2021/03/MPA.png?resize=768%2C415&ssl=1)

#### 장점
1. SEO(Search Engine Optimization, 검색 엔진 최적화)관점에서 유리하다
  > MPA는 완성된 형태의 HTML 파일을 서버로부터 전달받아 검색엔진이 페이지를 크롤링하기에 적합하다.

2. 첫 로딩이 매우 짧다.
  > 서버에서 이미 렌더링해 가져온다. 하지만 클라이언트는 JS파일을 모두 다운로드하고 적용하기 전까지의 각각의 기능은 동작하지 않는다.


#### 단점
1. 새로운 페이지를 이동하면 '깜빡'인다 (UX의 불편함 제공)
2. 페이지 이동시 불필요한 템플릿도 중복해서 로딩한다.
3. 서버 렌더링에 따른 부하가 증가한다.
4. 모바일 앱 개발시 추가적인 백엔드 작업이 필요해져 생산성이 복잡해진다.