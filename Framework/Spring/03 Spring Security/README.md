## Spring Security란
> Spring 기반의 애플리케이션의 보안(인증, 권한,인가 등)을 담당하는 스프링 하위 프레임워크이다.
> Spring Security는 '인증'과 '권한'에 대한 부분은 Filter 흐름에 따라 처리하고 있다.
> Filter는 Dispatcher Servlet으로 가기 전에 적용되므로 가장 먼저 URL 요청을 받지만, Interceptor는 Dispatcher와 Controller 사이에 위치한다는 점에서 적용 시기의 차이가 있다.
> Spring Security는 보안과 관련해서 체계적으로 많은 옵션을 제공해주기 때문에 개발자 입장에서는 일일이 보안관련 로직을 작성하지 않아도 된다는 장점을 가짐

### 주요 아키텍쳐

#### DelegatingFilterProxy
![alt](https://user-images.githubusercontent.com/66157892/148637802-7a69247f-54ed-4a46-82e2-ec453249289d.PNG)

- Servlet 컨테이너와 스프링 컨테이너(Application Context) 사이의 링크를 제공하는 servletFilter이다. 특정한 이름을 가진 스프링 빈(객체)를 찾아 그 빈에게 요청을 위임한다.
- 이유 : 서플릿 필터(서빌릿 컨테이너)와 시큐리티 필터(스프링 컨테이너)는 서로 다른 컨테이너에서 생성되고 동작한다.
- 요청 순서
> - Servlet Filter가 요청을 DelegatingFilterProxy에 전달한다.
> - DelegatingFilterProxy는 해당 요청을 스프링 컨테이너에 생성된 Filter를 구현한 스프링 빈에 위임한다.
> - SpringSecurityFilterChain 이름으로 생성도니 빈을 ApplicationContext에서 찾아 위임을 요청 (단. 실제 보안 처리를 하지 않음)

#### FilterChainProxy
![alt](https://user-images.githubusercontent.com/66157892/148638129-4511e780-8441-4dc6-8feb-a69744696ffb.PNG)
- SpringSecuriyFilterChain의 이름으로 생성되는 필터 빈이다. DelegatingFilterProxy로부터 요청을 위임 받고 실체로 보안을 처리한다. 스프링 시큐리티 초기화 시 생성되는 필터들을 관리하고 제어한다.

#### 필터 초기화와 다중 설정 클래스
- Spring Security 설정 클래스가 두 개 이상일 경우 FilterChainProxy 내부의 securityFilterChains 리스트에 securityFilterChain을 순서대로 저장한다.
- @Order Annotation을 통해 순서를 정하고 좁은 범위의 설장 클래스 부터 순서를 정한다.
<br>
![alt](https://user-images.githubusercontent.com/66157892/148639385-fdfc37fa-371e-4e7b-843f-bff461da249a.PNG)

### Authentication

- 인증 : Client가 누구인지 증명하는 것
- 사용자의 인증정보를 저장하는 토큰 개념
- 인증 요청 시 Authentication 객체에 id와 Password를 담고 인증 검증을 거친다.
- 인증 후 최종 인증 결과는 (User 객체, 권한정보)를 담아 SecurityContextHolder에 저장되어 전역적으로 참조가 가능해진다.
<br>
  ```   Authentication authentication = SecurityContexHolder.getContext().getAuthentication() ```

#### 구조
- principal : 사용자 아이디 or User 객체를 저장
- credentials : 사용자 비밀번호
- authorities : 인증된 사용자의 권한 목록
- details : 인증 부가 정보
- Authenticated : 인증 여부
- 인증 여부를 제외하면 대부분의 타입은 Object이다.

### SecurityContextHolder, SecurityContext

#### SecurityContext

- Authentication 객체가 저장되는 보관소로 필요 시 언제든지 Authentication 객체를 꺼내어 쓸 수 있도록 제고되는 클래스
- ThreadLocal 에 저장되어 아무 곳에서나 참조가 가능
- 인증이 완료되면 HttpSession에 저장되어 어플리케이션 전반에 걸쳐 전역적인 참조가 가능하다

#### 인증 시 저장되는 객체의 이해
- SecurityContextHolder -> SecurityContext -> Authentication -> User 객체 정보
- 순서대로 앞의 객체가 뒤의 객체를 보관한다

#### SecurityContextHolder

- SecurityContext 를 저장하는 저장소
- Securitycontext 객체 저장 방식
> - MODE_THREADLOCAL : 스레드 당 SecurityContext 객체를 할당, 기본값
> - MODE_INHERITABLETHREADLOCAL : 메인 스레드와 자식 스레드에 관하여 동일한 SecurityContext를 유지
> - MODE_GLOBAL : 응용 프로그램에서 단 하나의 SecurityContext를 저장한다
> ```Authentication authentication = SecurityContextHolder.getContext().getAuthentication()``` 

### SecurityContextPersistenceFilter
> SecurityContextPersistenceFilter 란 객체의 생성, 저장, 조회 등의 LifeCycle을 담당하는 Filter이다.
> SecurityContextRepository를 통하여 매 요청의 HttpSession에 존재하는 SecurityContext의 존재 유무 등을 판별하여 존재하지 않을 경우 비어 있는, 존재하는 경우는 해당 SecurityContext를 전 처리하여 SecurityContextHolder에 저장해줍니다.
![alt](https://user-images.githubusercontent.com/66157892/148670517-6db14b73-618f-4a2f-b7a7-52d717693c10.PNG)

#### SecurityContext 객체의 생성, 저장, 조회
 - 익명사용자
 > 새로운 Securitycontext 객체를 생성하여 SecurityContextHolder에 저장
 - 인증 시
 > 새로운 SecurityContext 객체를 생성하여 SecurityContextHolder에 저장, UsernamePasswordAuthenticationFilter에서 인증 성공 후 SecurityContext에 UsernamePasswordAuthentication 객체를 SecurityContext에 저장, 인증이 최종 완료되면 Session에 SecurityContext를 저장

 - 인증 후
 > Session에서 SecurityContext 꺼내어 SecurityContextHolder에서 저장 SecurityContext 안에 Authentication 객체가 존재하면 계속 인증을 유지한다.

 - 최종 응답 시
 > 항상 최종 응답시 SecurityContextHolder.clearContext() 동작을 진행한다.

 ### Authentication Flow : 인증 흐름 이해
![alt](https://user-images.githubusercontent.com/66157892/148671187-a33953c6-9bd5-47d3-bce0-94d61114b4bf.PNG)

1. UsernamePasswordAuthenticationFilter가 AuthenticationManger에게 Authentication 객체 (Request로 들어온 login id, pass정보)를 전달한다.
2. AuthenticationManger는 인증의 전반적인 관리를 하고, 인증을 처리할 수 있는 AuthenticationProvider를 찾는다. // uri antMatch에 맞는 곳? 
3. AuthenticationProvider가 UserDetailsService를 통해 service 계층에서 Repository 계층을 접근하여 id에 해당하는 회원 객체를 Authentication 객체에 저장하여 권한정보와 저장한다.
4. Authentication 객체를 AuthenticationManager에 전달 후 다 시 UsernamePasswordAuthenticationFilter에 전달 후 SecurityContext에 저장한다.

### AuthenticationManager: 인증관리자
> AuthenticationManager는 인자로 Authentication 객체를 받는다.
> Authentication 객체에 id,pw를 저장 후 AuthenticationManager에 보내 인증 과정을 거친다.
> 구현체는 ProviderManger이다. 해당 인증을 처리해 줄 수 있는 Provider를 찾는다.
> 해당 인증 처리 가능한 Provider가 없으면, 부모 ProviderManager에서 계속 탐색할 수 있다.
> 인증 성공 시 Provider가 Manager에게 인증 성공 Authentication 객체를 전달

### AuthenticationProvider
![alt]([https://](https://user-images.githubusercontent.com/66157892/148720386-8a806a30-100e-41e1-9ac4-ea9f93a59aa9.PNG))
> - AuthenticationProvider에서 실제 인증에 대한 부분을 처리하는데, 인증 전의 Authentication 객체를 받아서 인증이 완료된 객체를 반환하는 역할을 한다. 그림과 같이 AuthenticationProvider 인터페이스를 구현해서 Custom한 AuthenticationProvider를 작성하여 AuthenticationManager에 등록하면된다.
> supports(authentication)이 True인 Provider에게 authenticate()를 실행한다.


### Authorization, FilterSecurityInterceptor

#### Authorization
- Client에게 무엇이 허가 되어있는지 증명하는 것
---
![alt](https://user-images.githubusercontent.com/66157892/148721773-a5616401-d2cb-4320-94e6-1cef8a810ab7.PNG)

#### FilterSecurityInterceptor

- 마지막에 위치한 필터로써 인증된 사용자에 대하여 특정 요청의 승인/거부 여부를 최종적으로 결정
- 인증객체 없이 보호자원에 접근을 시도할 경우 AuthenticationException을 발생
- 인증 후 자원에 접근 가능한 권한이 존재하지 않을 경우 AccessDeniedException을 발생
- 권한 제어 방식 중 HTTP 자원의 보안을 처리하는 필터
- 권한 처리는 AccessDecisionManager에게 맡김

#### 인가 흐름
![alt](https://user-images.githubusercontent.com/66157892/148721924-57199bec-cadd-4b61-a602-566d98a8ae6f.PNG)
> 1. 모든 필터를 통과 후 마지막에 위치한 FilterSecurityInterceptor에게 요청이 온다.
> 2. 인증 객체가 Session에 있는지 없는지 확인한다. 없으면 AuthenticationException 예외를 발생시킨다.
> 3. SecurityMetadataSource를 통해 사용자가 요청한 자원에 필요한 권한 정보를 조회해서 전달한다.
> 4. 권한 정보가 필요 없으면 자원 접근을 허용
> 5. 접근하는 자원에 권한이 필요한 경우 AccessDecisionManager 를 통해 AccessDecisionVoter에게 심의를 요청하고 승인/거부를 결정
> 6. AccessDecisionManager 가 접근 승인을 할 겨우 자원 접근 허용한다. 접근이 거불 될 경우 AccessDeniedException 예외를 터트린다.