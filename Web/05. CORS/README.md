# CORS

## CORS란?

#### CORS(Cross-Origin Resource Sharing)는 교차 출처 리소스 공유 정책, 여기서 교차 출처라는 것은 다른 출처를 의미

### 출처(Origin)란?

> URL에서 **Protocol + Host + Port = Origin** <br> <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/1913553c-f630-47c2-bfbe-1c94ad63ca98" style="width: 500">

<br>

### 동일 출처 정책 (Same-Origin Policy)

> 💡 말 그대로 동일한 출처(Origin)에 대한 정책

- 동일한 출처에서만 리소스를 공유할 수 있다는 법률을 가짐
- 즉, 동일 출처 서버에 있는 리소스는 자유로이 가져올 수 있지만, 다른 출처의 서버에 있는 이미지나 영상같은 리소스는 상호작용이 불가능

  #### 동일 출처 정책이 왜 필요?

  > 💡 출처가 다른 두 어플리케이션이 자유로이 소통할 수 있는 환경은 굉장히 위험

  - 다른 사이트에서 특정 사이트를 흉내내어 동일하게 동작하도록 해 사용자가 로그인하게 만들고 세션을 탈취
  - CSRF, XSS 등의 방법으로 악의적인 목적을 가지고 개인정보를 쉽게 가로챌 수 있음

  #### 동일 출처 정책의 작동

  - 출처를 비교하는 로직은 서버에 구현된 스펙이 아니라, **브라우저에 구현**되어 있음 (서버는 정상적으로 응답하고, 브라우저가 정책 위반을 판단하여 응답의 사용 여부를 결정)
  - 웹이라는 환경에서 다른 출처의 리소스를 가져와서 사용하는 일은 굉장히 흔한 일이기 때문에, 몇 가지 예외 조항을 두고 이 조항에 해당하는 리소스 요청은 출처가 다르더라도 허용. 그 중 하나가 `"CORS 정책을 지킨 리소스 요청"`

<br>

### 교차 출처 정책 (Cross-Origin Policy)

> 💡 다른 출처의 리소스 공유에 대한 허용/비허용 정책

#### 브라우저의 CORS 기본 동작

1. 클라이언트에서 HTTP 요청의 헤더에 Origin을 담아서 전달
   - 브라우저는 요청 헤더에 Origin이라는 필드에 출처를 함께 담아 보냄
     <br>
     <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/bac554fc-92e9-4e81-afc2-64989ffc6326" style="width: 400">
2. 서버는 응답 헤더에 Access-Control-Allow-Origin을 담아서 클라이언트에 전달
   - 이 리소스를 접근하는 것이 허용된 출처 url을 내려보냄
     <br>
     <img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/d9f091e6-34fc-4c4a-969e-0d84d0f00aff" style="width: 400">
3. 클라이언트에서 Origin과 서버가 보내준 Access-Control-Allow-Origin을 비교
   - 비교 후 유효하지 않다면 그 응답을 사용하지 않고 버림 <span style="color:red">(CORS 에러)
     </span>

<br>

#### CORS 작동 방식

1. 예비 요청 (Preflight Request)
   > 💡 브라우저는 요청을 보낼 때, 먼저 예비 요청을 보내 서버와 통신이 잘 되는지 확인하고 본 요청을 보냄
   - 예비 요청의 동작
     1. OPTIONS 메소드로 예비 요청을 보내며 Origin 헤더에 자신의 출처를 넣음
     2. 서버는 이 예비 요청에 대한 응답으로 어떤 것을 허용하고 어떤 것음 금지하는지에 대한 정보를 보냄. Access-Control-Allow-Origin 헤더에 허용되는 Origin 목록을 설정
     3. 브라우저는 보낸 요청과 서버가 응답한 정책을 비교하여, 해당 요청이 안전한지 확인 후 본 요청을 전송
2. 단순 요청 (Simple Request)
   > 💡 예비 요청을 생략하고 서버에 바로 본 요청을 보냄. 동작은 예비 요청과 동일
   - 단순 요청의 조건
     - 요청의 메소드는 GET, HEAD, POST 중 하나여야 함
     - Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width 헤더일 경우에만 적용
     - Content-Type 헤더가 application/x-www-form-urlencoded, multipart/form-data, text/plain중 하나여야함
3. 인증된 요청 (Credentialed Request)
   > 💡 자격 인증 정보(Credential)를 실어 요청할 때 사용. 세션 ID가 저장되어있는 쿠키 혹은 Authorization 헤더에 설정하는 토큰 등
   - 인증된 요청의 동작
     1. 클라이언트에서 인증 정보를 보내도록 설정
     2. 서버에서 인증된 요청에 대한 응답 헤더 설정
        - 헤더의 Access-Control-Allow-Credentials 항목을 true로 설정
        - Access-Control-Allow-Origin(|Method|Headers) 값에 와일드카드 사용 불가
     3. 브라우저는 보낸 요청과 서버가 응답한 정책을 비교하여, 해당 요청이 안전한지 확인 후 본 요청을 전송
