## **TDD란?**

<aside>
💡 TDD란 Test Driven Development의 약자로 ‘테스트 주도 개발’이라고 한다.

</aside>

반복 테스트를 이용한 소프트웨어 방법론으로 작은 단위의 테스트 케이스를 작성하고 이를 통과하는 코드를 추가하는 단계를 반복하여 구현한다.

짧은 개발 주기의 반복에 의존하는 개발 프로세스이며, 애자일 방법론 중 하나인 `eXtream Programming(XP)`의 ‘Test-First’ 개념에 기반을 둔 단순한 설계를 중요시한다.

- **eXtream Programming(XP)란?**
    
    미래에 대한 예측을 최대한 하지 않고 지속적으로 프로토타입을 완성하는 애자일 기방법론 중 하나이다.
    
    이 방법론은 추가 요구사항이 생기더라도 실시간으로 반영할 수 있다.
    

### **단위 테스트(unit Test)란?**

말 그대로 한 단위(일반적으로 class)만을 테스트하는 것이다.

![image (94)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/d0c2d738-8c0f-497b-b1cb-3db2a7a75b75)

## **TDD 개발주기**

위 그림은 TDD의 개발주기를 표현한 것이다.

**{ Red } 단계에서는 실패하는 테스트 코드를 먼저 작성한다.**

**{ Green } 단계에서는 테스트 코드를 성공시키기 위한 실제 코드를 작성한다.**

**{ Blue } 단계에서는 중복 코드 제거, 일반화 등의 리팩토링을 수행한다.**

중요한 것은 `실패하는 테스트 코드를 작성할 때까지 실제 코드를 작성하지 않는 것`과, 실패하는 테스트를 통과할 정도의 `최소 실제 코드`를 작성해야 하는 것이다. 이를 통해 실제 코드에 대해 기대되는 바를 보다 명확하게 정의 함으로써 불필요한 설계를 피할 수 있고, 정확한 요구 사항에 집중할 수 있다.

## **일반 개발 방식과 TDD 개발 방식의 비교**

**일반 개발 방식**

보통 개발 방식은 ‘요구사항 분석 → 설계 → 개발 → 테스트 → 배포’의 형태의 개발 주기를 갖는다.

![image (96)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/3f8b667d-6bd5-4c9b-9dcf-939332d8faa9)

이러한 방식은 소프트웨어 개발을 느리게 하는 잠재적 위험이 존재한다.

그 이유는 아래와 같다.

**소비자의 요구사항이 처음부터 명확하지 않을 수 있다.<br>
따라서 처음부터 완벽한 설계는 어렵다.<br>
자체 버그 검출 능력 저하 또는 소스코드의 품질이 저하될 수 있다.<br>
자체 테스트 비용이 증가할 수 있다.**

이러한 문제점이 발생되는 이유는 어느 프로젝트든 초기 설계가 완벽하다고 말할 수 없기 때문이다.

고객의 요구사항 또는 디자인의 오류 등 많은 외부 또는 내부 조건에 의해 재설계하여 점진적으로 완벽한 설계로 나아간다.

재설계로 인해 개발자는 코드를 삽입, 수정, 삭제하는 과정에서 불필요한 코드가 남거나 중복처 될 가능성이 크다.

> 결론적으로 이러한 코드들은 재사용이 어렵고 관리가 어려워서 유지보수를 어렵게 만든다.
> 

작은 부분의 기능 수정에도 모든 부분을 테스트해야 하므로 전체적인 버그를 검출하기 어려워진다. 따라서 자체 버그 검출 능력이 저하된다. 그 결과 어디서 버그가 발생할지 모르기 때문에 잘못된 코드도 고치지 않으려 하는 현상이 나타나게 된다.

이 현상은 소스코드의 품질 저하와 직결된다. 작은 수정에도 모든 기능을 다시 테스트해야하는 문제가 발생하여 자체 테스트 비용이 증가된다.

**TDD 개발 방식**

TDD와 일반적인 개발 방식의 가장 큰 차이점은 테스트 코드를 작성한 뒤에 실제 코드를 작성한다는 것이다.

디자인(설계) 단계에서 프로그래밍 목적을 반드시 미리 정의해야만 하고, 무엇보다 테스트해야 할지 미리 정의(테스트 케이스 작성)해야만 한다.

테스트 코드를 작성하는 도중 발생하는 예외 사항(버그 및 수정사항)은 테스트 케이스에 추가하고 설계를 개선한다.

이후 테스트가 통과된 코드만을 코드 개발 단계에서 실제 코드로 작성한다.

![image (95)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/6b455cd1-9186-4672-b9f4-0e14cf9cc0eb)
> 이러한 반복적인 단계가 진행되면서 자연스럽게 코드의 버그가 줄어들고 소스코드는 간결해진다.
> 

또한 테스트 케이스 작성으로 인해 자연스럽게 설계가 개선됨으로 재설계 시간이 절감된다.

### **JUnit란?**

JUnit는 현재 전 세계적으로 가장 널리 사용되는 ‘Java 단위 테스트 프레임워크’이다.

에릭 감마와 켄트 벡이 탄생시켰다. JUnit을 시작으로 CUnit(C언어), CPPUnit(C++), PyUnit(Python) 등 xUnit 프레임워크가 탄생하게 되었다.

### **xUnit란?**

자바의 단위 테스팅 프레임워크인 JUnit만 있는 것이 아니다.

다른 언어도 단위 테스트를 위한 프레임워크가 존재하며 보통 이름을 xUnit이라 지칭한다.

## **TDD 개발 방식의 장점**

1. **보다 튼튼한 객체 지향적인 코드 생산**
    
    TDD는 코드의 재사용 보장을 명시하므로 TDD를 통한 소프트웨어 개발 시 기능 별 철저한 모듈화가 이뤄진다.
    
    이는 종속성과 의존성이 낮은 모듈로 조합된 소프트웨어 개발을 가능하게 하며 필요에 따라 모듈을 추가하거나 제거해도 소프트웨어 전체 구조에 영향을 미치치 않게 된다.
    
2. **재설계 시간의 단축**
    
    테스트 코드를 먼저 작성하기 때문에 개발자가 지금 무엇을 해야하는지 분명히 정의하고 개발을 시작하게된다. 또한 테스트 시나리오를 작성하면서 다양한 예외사항에 대해 생각해 볼 수 있다. 이는 개발 진행 중 소프트웨어의 전반적인 설계가 변경되는 일을 방지할 수 있다.
    
3. **디버깅 시간의 단축**
    
    이는 유닛 테스팅을 하는 이점이기도하다. 예를 들면 사용자의 데이터가 잘못 나온다면 DB의 문제인지, 비즈니스 레이어의 문제인지 UI의 문제인지 실제 모든 레이어들을 전부 디버깅 해야하지만, TDD의 경우 자동화 된 유닛 테스팅을 전제하므로 특정 버그를 손 쉰게 찾아낼 수 있다.
    
4. **테스트 문서의 대체 가능**
    
    주로 SI 프로젝트 진행 과정에서 어떤 요소들이 테스트 되었는지 테스트 정의서를 만든다. 이것은 단순 통합 테스트문서에 지나지 않는다. 하지만 TDD를 하게 될 경우 테스팅을 자동화 시킴과 동시에 보다 정확한 테스트 근거를 산출 할 수 있다.
    
5. **추가 구현의 용의함**
    
    개발이 완료된 소프트웨어에 어떤 기능을 추가할 때 가장 우려되는 점은 해당 기능이 기존 코드에 어떤 영향을 미칠지 알지 못한다는 것이다. 하지만 TDD의 경우 자동화된 유닛 테스팅을 전제하므로 테스트 기간을 획기적으로 단축시킬 수 있다.
    

> 이러한 TDD의 장점에도 불구하고 모두가 이 개발 프로세스를 따르는 것은 아니다. 그 이유는 무엇일까?
> 

## **TDD 개발 방식의 단점**

**가장 큰 단점은 바로 `생산성 저하`이다.**

개발 속도가 느려진다고 생각하는 사람이 많기 때문에 TDD에 대해 반신반의 한다.

왜냐하면 처음부터 2개의 코드를 짜야하고 중간중간 테스트를 하면서 고쳐나가야하기 때문이다.

TDD 방식의 개발 시간은 일반적인 개발 방식에 비해 대략 10~30% 정도로 늘어난다.
