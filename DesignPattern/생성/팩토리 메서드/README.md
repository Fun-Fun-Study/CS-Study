### 🔎 Factory Method Pattern 이란?

팩토리 메소드 패턴은 객체 생성을 공장(Factory) 클래스로 캡슐화 처리하여 대신 생성하게 하는 생성 디자인 패턴이다.

즉, 클라이언트에서 직접 `new` 연산자를 통해 제품 객체를 생성하는 것이 아닌, 제품 객체들을 도맡아 생성하는 공장 클래스를 만들고, 이를 상속하는 서브 공장 클래스의 메서드에서 여러가지 제품 객체 생성을 각각 책임 지는 것이다.

또한 객체 생성에 필요한 과정을 템플릿 처럼 미리 구성해놓고, 객체 생성에 관한 전처리나 후처리를 통해 생성 과정을 다양하게 처리하여 객체를 유연하게 정할 수 있는 특징도 있다.

![메서드1](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/2e2190bc-f57c-4857-b551-dd11c57b1127)

1. **Creator:** 최상위 공장 클래스로서, 팩토리 메서드를 추상화하여 서브 클래스로 하여금 구현하도록 함
    1. **객체 생성 처리 메서드(someOperartion) :** 객체 생성에 관한 전처리, 후처리를 템플릿화한 메소드
    2. **팩토리 메서드(createProduct)** **:** 서브 공장 클래스에서 재정의할 객체 생성 추상 메서드
2. **ConcreteCreator:** 각 서브 공장 클래스들은 이에 맞는 제품 객체를 반환하도록 생성 추상 메소드를 재정의한다. 즉, 제품 객체 하나당 그에 걸맞는 생산 공장 객체가 위치된다.
3. **Product:** 제품 구현체를 추상화
4. **ConcreteProduct:** 제품 구현체

<aside>
🧐 정리하자면, 팩토리 메소드 패턴은 객체를 만들어내는 공장(Factory 객체)을 만드는 패턴이라고 보면 된다. 그리고 어떤 클래스의 인스턴스를 만들지는 미리 정의한 공장 서브 클래스에서 결정한다.
객체는 사람/사물과 같은 유형의 형태가 될수도 있고, 전략/상태와 같은 무형의 형태가 될수도 있고, 공장과 같은 중간 생성자 역할도 한다고 보면 된다.

</aside>

### 🔎 Factory Method Pattern 흐름

**클래스 구성**

![메서드2](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/cef0ea4f-8b2c-4362-8619-dd3df1f5fde4)

**제품(Product) 클래스**

```java
// 제품 객체 추상화 (인터페이스)
interface IProduct {
    void setting();
}

// 제품 구현체
class ConcreteProductA implements IProduct {
    public void setting() {
    }
}

class ConcreteProductB implements IProduct {
    public void setting() {
    }
}
```

**공장(Factory) 클래스**

```java
// 공장 객체 추상화 (추상 클래스)
abstract class AbstractFactory {

    // 객체 생성 전처리 후처리 메소드 (final로 오버라이딩 방지, 템플릿화)
    final IProduct createOperation() {
        IProduct product = createProduct(); // 서브 클래스에서 구체화한 팩토리 메서드 실행
        product.setting(); // .. 이밖의 객체 생성에 가미할 로직 실행
        return product; // 제품 객체를 생성하고 추가 설정하고 완성된 제품을 반환
    }

    // 팩토리 메소드 : 구체적인 객체 생성 종류는 각 서브 클래스에 위임
    // protected 이기 때문에 외부에 노출이 안됨
    abstract protected IProduct createProduct();
}

// 공장 객체 A (ProductA를 생성하여 반환)
class ConcreteFactoryA extends AbstractFactory {
    @Override
    public IProduct createProduct() {
        return new ConcreteProductA();
    }
}

// 공장 객체 B (ProductB를 생성하여 반환)
class ConcreteFactoryB extends AbstractFactory {
    @Override
    public IProduct createProduct() {
        return new ConcreteProductB();
    }
}
```

**클래스 흐름**

![메서드3](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/61772b0a-6766-4564-9444-44eeb9e48feb)

```java
class Client {
    public static void main(String[] args) {
        // 1. 공장 객체 생성 (리스트)
        AbstractFactory[] factory = {
                new ConcreteFactoryA(),
                new ConcreteFactoryB()
        };

        // 2. 제품A 생성 (안에서 createProduct() 와 생성 후처리 실행)
        IProduct productA = factory[0].createOperation();

        // 3. 제품B 생성 (안에서 createProduct() 와 생성 후처리 실행)
        IProduct productB = factory[1].createOperation();
    }
}
```

![메서드4](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/1b32a60f-4aea-4b3c-9d17-c64aec97b5a8)

### 🔎 Factory Method Pattern 특징

**패턴 사용 시기**

1. 클래스 생성과 사용의 처리 로직을 분리하여 결합도를 낮추고자 할 때
2. 코드가 동작해야 하는 객체의 유형과 종속성을 캡슐화를 통해 정보 은닉 처리 할 경우
3. 라이브러리 혹은 프레임워크 사용자에게 구성 요소를 확장하는 방법을 제공하려는 경우
4. 기존 객체를 재구성하는 대신 기존 객체를 재사용하여 리소스를 절약하고자 하는 경우
    1. 상황에 따라 적절한 객체를 생성하는 코드는 자주 중복될 수 있다. 그리고 객체 생성 방식의 변화는 해당되는 모든 코드 부분을 변경해야 하는 문제가 발생한다.
    2. 따라서 객체의 생성 코드를 별도의 클래스 / 메서드로 분리 함으로써 객체 생성의 변화에 대해 대비를 하기 위해 팩토리 메서드 패턴을 이용한다고 보면 된다.
    3. 특정 기능의 구현은 별개의 클래스로 제공되는 것이 바람직한 설계이기 때문이다.

**패턴 장점**

1. 생성자(Creator)와 구현 객체(concrete product)의 강한 결합을 피할 수 있다.
2. 팩토리 메서드를 통해 객체의 생성 후 공통으로 할 일을 수행하도록 지정해줄 수 있다.
3. 캡슐화, 추상화를 통해 생성되는 객체의 구체적인 타입을 감출 수 있다.
4. 단일 책임 원칙 준수 : 객체 생성 코드를 한 곳 (패키지, 클래스 등)으로 이동하여 코드를 유지보수하기 쉽게 할수 있으므로 원칙을 만족
5. 개방/폐쇄 원칙 준수 : 기존 코드를 수정하지 않고 새로운 유형의 제품 인스턴스를 프로그램에 도입할 수 있어 원칙을 만족 (확장성 있는 전체 프로젝트 구성이 가능)
6. 생성에 대한 인터페이스 부분과 생성에 대한 구현 부분을 따로 나뉘었기 때문에 패키지 분리하여 개별로 여러 개발자가 협업을 통해 개발

![메서드5](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/21cae871-9779-49fc-8d9c-f57195e87de3)

**패턴 단점**

1. 각 제품 구현체마다 팩토리 객체들을 모두 구현해주어야 하기 때문에, 구현체가 늘어날때 마다 팩토리 클래스가 증가하여 서브 클래스 수가 폭발한다.
2. 코드의 복잡성이 증가한다.


<details>
<summary>자바 코드로 살펴보기</summary>
<div markdown="1">

**`Car`**

```java
@AllArgsConstructor
@ToString
public class Car {
    private final String type;
    private final int doors;
    private final int seats;
    private final boolean hasTruckBed; // 트럭 짐칸 여부
}
```

**`CarFactory`**

```java
public class CarFactory {
    public static Car buildCar(String type) {
        // validate
        if (type == null) {
            throw new IllegalArgumentException("타입에 null 이 들어올 수 없습니다.");
        }

        if(!type.equals("sedan") && !type.equals("truck")) {
            throw new IllegalArgumentException("현재 만들 수 없는 종류의 차입니다.");
        }

        // notifyPreparing
        notifyPreparing(type);

        // produceCar
        Car car = null;

        if(type.equals("sedan")) {
            car = new Car(type, 4, 4, false);
        }

        if(type.equals("truck")) {
            car = new Car(type, 2, 2, true);
        }

        // notifyCompleted
        System.out.println(type + "을 완성했습니다.");

        return car;
    }

    private static void notifyPreparing(String type) {
        System.out.println(type + "을 만들 준비중 입니다.");
    }
}
```

**`Client`**

```java
public class Client {
    public static void main(String[] args) {
        Car sedan = CarFactory.buildCar("sedan");
        System.out.println("생산 결과: " + sedan.toString());
        Car truck = CarFactory.buildCar("truck");
        System.out.println("생산 결과: " + truck.toString());
    }
}
```

- 다양한 종류의 차를 만드는 공장이 필요하다면?
    - 자동차 종류가 추가되어도 쉽게 대응하여야 한다

---

**공통 부분을 추상화하고 인터페이스로 묶기**

- 아무리 타입이 바뀌어도 바뀌지 않는 공통 로직은?
    - 검증 부분(**`validate`**)
    - 준비 알림 부분(**`notifyPreparing`**)
    - 완료 알림 부분(`**notifiyCompleted**`)
- 타입이 바뀔 때마다 변화해야 하는 부분은?
    - 타입에 따라 커스터마이징 하는 부분(**`produceCar`**)

**인터페이스 생성하기**

```java
public interface CarFactory {

}
```

**validate 부분 수정**

- 타입이 한정되어 있을 때는 enum을 활용하자!
- carType이라는 `**enum**` 클래스를 새로 만들자

```java
public enum CarType {
    SEDAN("sedan"), TRUCK("truck");

    public final String name;

    CarType(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return name;
    }
}
```

- **`CarType`**을 만들어 클라이언트는 더 이상 문자열 실수를 하지 않고, 지원하지 않는 타입을 선택할 수도 없다
- **`CarFactory`**에서 사용할 공통 `**validate()**` 메서드를 생성하자

```java
public interface CarFactory {
    private void validateType(CarType type) {
        if (type == null) {
            throw new IllegalArgumentException("타입에 null 이 들어올 수 없습니다.");
        }
    }
		private void notifyPreparing(CarType type) {
        System.out.println(type + "을 만들 준비중 입니다.");
    }

    private void notifyComplete(CarType type) {
        System.out.println(type + "을 완성했습니다.");
    }
		Car produceCar(CarType type);
}
```

<aside>
🧐 JAVA 11부터는 인터페이스에 일반 함수를 정의할 수 있다

</aside>


- null 만 체크하면 된다
- 공통으로 사용될 로직은 전부 의미있는 메서드 이름으로 빠져서 가독성이 좋아졌음
- 자동차 종류마다 달라지는 produceCar()의 구현은 클라이언트에게 넘김
    - 💡 **팩토리 메서드 패턴의 특징은 객체 생성부 로직 구현을 다른 클래스에게 넘기는 것**
- 클라이언트는 공통 로직을 제외한 커스터마이징 로직(`**produceCar()**`)만 구현하면 되는 것이다

출처

https://jake-seo-dev.tistory.com/366
</div>
</details>