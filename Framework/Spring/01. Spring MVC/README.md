### ☀️ MVC

![mvc1](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/2acce5b8-a6a2-419f-886c-b2cf270a02c5)

**View란?**

- 사용자 인터페이스 요소를 나타낸다.
- 데이터 및 객체의 입력, 출력을 담당한다.
- 모델이 가지고 있는 정보를 따로 저장해서는 안된다.
  - 즉, 화면에 표시하기만 하는 로직만 가지고 있어야 한다.
- 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 된다.
  - 다른 요소를 참조하거나 어떻게 동작하는지 알아서는 안된다. 즉 뷰는 데이터를 받으면 화면에 표시해주는 역할만 가진다.
- 변경이 일어나면 변경통지에 대한 처리방법을 구현해야만 한다.
  - 데이터가 변경하면 이를 모델에게 전달해서 모델을 변경하는 로직을 구현해야한다.
- 재사용이 가능하게끔 설계를 해야 하며 다른 정보들을 표현할 때 쉽게 설계를 해야 한다.

**Controller란?**

- 모델과 뷰를 잇는 다리 역할이다.
- 사용자가 데이터를 만들거나 수정하는 이벤트를 발생하면 그 이벤트를 처리하는 부분을 뜻한다.
- 모델이나 뷰에 대해서 알고 있어야 한다.
  - 변경 이벤트가 발생하면 컨트롤이 중재하기 위해 모델과 그에 관련된 뷰에 대해서 알고 있어야 한다.
- 모델이나 뷰의 변경을 모니터링 해야 한다.
  - 모델이나 뷰의 변경 통지를 받으면 해당 로직에 맞게 바꿔 각각의 구성 요소들에게 통지를 해야한다.

**Model이란?**

- 애플리케이션의 정보, 데이터 즉 상태를 가지고 있다.
- 모델에서는 정보, 데이터들의 가공을 책임지고 있다.
- 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.
  - 모든 정보들을 가지고 있어야 한다.
- 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 한다.
  - UI를 직접 수정하는 로직이나 뷰를 참조하는 내부 속성값을 가지고 있지 말아야 한다.
- 변경이 일어나면 변경 통지에 대한 처리 방법을 구현해야만 한다.
  - 모델이 가지고 있는 정보는 모델만 가지고 있어야 한다.

**왜 MVC패턴을 사용해야 할까?**

- 사용자가 보는 화면, 데이터 처리, 이를 중재하는 컨트롤을 나눠서 구현을 하면 각각 맡은바에만 집중을 할 수 있다. 즉 공장에서도 하나의 역할만 하면 효율적인 분업 효과를 받을 수 있듯이 이러한 패턴을 사용한다.
- 이러한 패턴을 사용함으로써 애플리케이션을 만들면 유지보수, 확장성, 유연성이 증가하고 개발의 치명적인 문제점인 중복코드도 사라진다.

💡 **MVC는 Model,View,Controller의 앞머리를 딴 글자입니다.**

### ☀️ 라이브러리 vs 프레임워크

- 여러 회사 비영리 단체, 혹은 개인들이 MVC 구조의 기본 설계가 갖춰진 상태인 **MVC 웹 프레임워크**를 제공합니다.
- MVC 웹 프레임워크를 건물에 비유를 하면, **건물의 기초 골격과 수도, 전기, 난방이 설치된 채로 사용자가 원하는 대로 집을 개조하고 꾸밀 수 있게 제공되는 것**입니다.
- 라이브러리는 각 각 **개별적인 기능들**(비유하자면 문짝이나 욕조 등의 부속품)이라고 하면 프레임워크는 이것들이 연결되어 **기초적인 제품 형태를 갖춘 상태**를 뜻합니다.
- 쉽게 말해, **내가 무언가를 가져다가 쓴다는 느낌이 든다면 그것을 라이브러리를 사용하는 것**이고(내가 갑), **내가 무언가의 틀 안에서 작업한다는 느낌이 든다면 프레임워크**입니다.(프레임워크가 갑)

**인기 MVC 프레임워크**

| 프레임워크     | 언어       |
| -------------- | ---------- |
| Spring         | Java       |
| Django         | Python     |
| ASP.NET        | C#         |
| Express        | JavaScript |
| Ruby on Radils | Ruby       |
| Laravel        | PHP        |

**MVC는 크게 두 가지 패턴으로 구분할 수 있습니다. 이 중, 스프링은 MVC2패턴을 채택하였습니다.**

### ☀️ MVC1

- MVC1 패턴의 경우 View와 Controller를 모두 **JSP**가 담당하는 형태를 가집니다.
- 즉 JSP 하나로 유저의 요청을 받고 응답을 처리하므로 구현 난이도는 쉽습니다.
- 단순한 프로젝트에는 괜찮겠지만 내용이 복잡하고 거대해질수록 이 패턴은 힘을 잃습니다.
- JSP 하나에서 MVC 가 모두 이루어지다보니 재사용성도 매우 떨어지고, 읽기도 힘들어집니다. **즉 유지보수에 있어서 문제가 발생합니다.**
  ![mvc2](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/7e1de919-da02-4f5d-b490-1ff918d73ad0)

### ☀️ MVC2

- MVC2 패턴은 널리 표준으로 사용되는 패턴입니다. 요청을 하나의 컨트롤러(Servlet)가 먼저 받습니다.
- **즉 MVC1과는 다르게 Controller, View가 분리되어 있습니다.**
- 따라서 역할이 분리되어 MVC1패턴에서의 단점을 보완할 수 있습니다.
- 그러므로 개발자는 M, V, C 중에서 수정해야 할 부분이 있다면, 그것만 꺼내어 수정하면 됩니다. **따라서 유지보수에 있어서도 큰 이점을 가집니다.**
- MV2는 MVC1 패턴보다 구조가 복잡해질 수 있지만, 개발자가 이러한 세부적인 구성까지 신경쓰지 않을 수 있도록 각종 프레임워크들이 지금까지 잘 발전되어 왔습니다. 그 중에서 대표적인 것이 바로 **스프링 프레임워크**입니다.
  ![mvc3](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/60b5bc04-2a98-4e51-a0a7-7520628a575c)

### ☀️ Spring Framework의 MVC2 패턴

- 스프링에서는 유저의 요청을 받는 **DispathcerServlet**이 핵심입니다. 이것이 Front Controller의 역할을 맡습니다.
- Front Controller(프런트 컨트롤러)란, 우선적으로 유저(클라이언트)의 모든 요청을 받고, 그 요청을 분석하여 세부 컨트롤러들에게 필요한 작업을 나눠주게 됩니다.
- 모든 과정은, 스프링 프로젝트를 실행하여 디버깅할 시 로그에서 모두 확인할 수 있습니다.
  ![mvc4](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/fdc4667e-aab5-44e9-99ac-636215501be2)
  ![mvc5](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/69ce9e31-028e-4562-9d36-21e69a147d7b)

  ✅ DispatcherServlet : 제일 앞단에서 HTTP Request를 처리하는 Controller
  Spring MVC에서는 HTTP Request가 왔을 때, DispatcherServlet이 HTTP Request를 처리할 Controller를 지정한다.

  ✅ Controller(Handler) : HTTP Request를 처리해 Model을 만들고 View를 지정
  DispatcherServlet에 의해 배정된 Controller는 HTTP Request를 처리하고, HTTP Request의 메세지를 처리해 필요한 데이터를 뽑아 Model에 저장한다.

  ✅ ModelAndView : Controller에 의해 반환된 Model과 View가 Wrapping된 객체
  Model은 Map 자료구조로, HTTP Request 속의 데이터를 파싱해 Key-Value 쌍으로 만들어 저장한다.

  ```java
  public ModelAndView(String viewName, @Nullable Map<String, ?> model){
  	this.view = viewName;
  	if(model != null) {
  		getModelMap().addAllAttributes(model);
  	}
  }
  ```

  ✅ View, View Name: View Resolver에서 그릴 View 지정
  ✅ ViewResolver: ModelAndView를 처리하여 View 그리기
  우리가 특정한 url로 들어갔을 때, 우리에게 보여지는 View가 바로 이곳에서 만들어지는 View이다.

### ☀️ Spring MVC의 의의

특히 Spring MVC는 HTTP Request를 처리하는 부분인 Controller, 데이터를 처리해 정제된 데이터를 넣는 Model, 정제된 데이터를 활용해 사용자에게 보여지는 View에 대한 역할 분리를 하였다. Spring MVC를 사용하면 Model, View, Controller 모두를 인터페이스를 사용해 규격화해놓아 유연하고 확장성 있게 웹 어플리케이션을 설계할 수 있다.

    💡 Spring MVC는 웹 어플리케이션을 유연하고 확장 가능하게 만들어준다.

출처

[https://kotlinworld.com/326#Controller-Handler-%--%-A%--HTTP%--Request�%A-�%--�%B-%--�%A-��%--%B-%--Model�%-D%--%--�%A-%-C�%--%A-�%B-%A-%--View�%A-�%--�%A-%--�%A-%--](https://kotlinworld.com/326#Controller-Handler-%25--%25-A%25--HTTP%25--Request%EB%25A-%BC%25--%EC%25B-%25--%EB%25A-%AC%ED%25--%25B-%25--Model%EC%25-D%25--%25--%EB%25A-%25-C%EB%25--%25A-%EA%25B-%25A-%25--View%EB%25A-%BC%25--%EC%25A-%25--%EC%25A-%25--)

https://poododang.tistory.com/entry/MVC-MVCFrameWork
