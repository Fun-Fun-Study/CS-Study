## 제네릭(Generic) 이란?

<aside>
💡 자바에서 제네릭(Generics)은클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미한다. 객체별로 다른 타입의 자료가 저장될 수 있도록 한다.

</aside>

```java
ArrayList<String> list = new ArrayList<>();
```

저 `<>` 가 바로 제네릭이다. 괄호 안에는 타입명을 기재한다. 이후 ArrayList는 문자열 데이터만 리스트에 적재할 수 있게 된다.

다음과 같이 배열과 리스트의 선언문의 형태를 비교하면 이해가 더 쉽다. 선언하는 키워드와 문법 순서가 다를 뿐, 결국 자료형 명을 선언하고 자료형의 타입을 지정한다는 점은 같다고 볼 수 있다.

![img1 daumcdn](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/8e03c016-13e1-4c11-90bd-bcd67fbe8305)

이 처럼 제너릭은 배열의 타입을 지정하듯이 리스트 자료형 같은 컬렉션 클래스나 메소드에서 사용할 내부 데이터 타입을 파라미터로 주듯이 외부에서 지정하는 `타입을 변수화 한 기능`이라고 이해할 수 있다.

<aside>
💡 우리가 변수를 선언할때 변수의 타입을 지정해주듯이, 제네릭은 객체(Object)에 타입을 지정해주는 것이라고 보면 된다.

</aside>

## 제네릭 타입 매개변수

위에서 보다시피, 제네릭은 `<>` 꺾쇠 괄호 키워드를 사용하는데 이를 다이아몬드 연산자라고 한다. 그리고 이 꺾쇠 괄호 안에식별자 기호를 지정함으로써 파라미터화 할 수 있다. 이것을 마치 메소드가 매개변수를 받아 사용하는 것과 비슷하여 제네릭의 `타입 매개변수(parameter) / 타입 변수` 라고 부른다.

![img1 daumcdn (1)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/9a941b3e-3f22-4d46-90c3-a9037a7b4eca)

**타입 파라미터 정의**

> 이 타입 매개변수는 제네릭을 이용한 클래스나 메소드를 설계할 때 사용된다.
> 

예를들어 다음 코드는 제네릭을 감미한 클래스를 정의한 코드이다. 클래스명 옆에 `<T>` 기호로 제네릭을 붙여준 걸 볼 수 있다. 그리고 클래스 내부에서 식별자 기호 T를 클래스 필드와, 메소드의 매개변수의 타입으로 지정되어 있다.

```java
class FruitBox<T> {
    List<T> fruits = new ArrayList<>();

    public void add(T fruit) {
        fruits.add(fruit);
    }
}
```

제네릭 클래스를 만들었으면 이를 인스턴스화 해보자. 마치 파라미터를 지정해서 보내는 것처럼 생성 코드에서 꺾쇠 괄호 안에 지정해주고 싶은 타입명을 할당해주면, 제네릭 클래스 선언문 부분으로 가서 타입 파라미터 T가 지정된 타입으로 모두 변환되어 클래스의 타입이 지정되게 되는 것

```java
// 제네릭 타입 매개변수에 정수 타입을 할당
FruitBox<Integer> intBox = new FruitBox<>(); 

// 제네릭 타입 매개변수에 실수 타입을 할당
FruitBox<Double> intBox = new FruitBox<>(); 

// 제네릭 타입 매개변수에 문자열 타입을 할당
FruitBox<String> intBox = new FruitBox<>(); 

// 클래스도 넣어줄 수 있다. (Apple 클래스가 있다고 가정)
FruitBox<Apple> intBox = new FruitBox<Apple>();
```

<T> 부분에서 실행부에서 타입을 받아와 내부에서 T 타입으로 지정한 멤버들에게 전파하여 타입이 구체적으로 설정되는 것. 이를 `구체화(Specialization)`이라고 한다.

![img1 daumcdn (2)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/db366c44-0b20-4492-9e86-c50d4043a6ef)

⚠️ **타입 파라미터 할당 가능 타입**
제네릭에서 할당 받을 수 있는 타입은 **Reference 타입** 뿐이다. 즉, int형 이나 double형 같은 자바 원시 타입(Primitive Type)을 제네릭 타입 파라미터로 넘길 수 없다는 말이다.

![img1 daumcdn (3)](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/ef015cbd-2916-409d-8aea-ea7c8e5feee3)

```java
class Fruit { }
class Apple extends Fruit { }
class Banana extends Fruit { }

class FruitBox<T> {
    List<T> fruits = new ArrayList<>();

    public void add(T fruit) {
        fruits.add(fruit);
    }
}

public class Main {
    public static void main(String[] args) {
        FruitBox<Fruit> box = new FruitBox<>();
        
        // 제네릭 타입은 다형성 원리가 그대로 적용된다.
        box.add(new Fruit());
        box.add(new Apple());
        box.add(new Banana());
    }
}
```

또한 제네릭 타입 파라미터에 클래스가 타입으로 온다는 것은, 클래스끼리 상속을 통해 관계를 맺는 객체 지향 프로그래밍의 `다형성 원리`가 그대로 적용이 된다는 소리이다.아래 예제 코드를 보면 타입 파라미터로`<Fruit>` 로 지정했지만업캐스팅을 통해 그 자식 객체도 할당이 됨을 볼 수 있다.

💡 **복수 타입 파라미터**

제네릭은 반드시 한개만 사용하라는 법은 없다. 만일 타입 지정이 여러개가 필요할 경우 2개, 3개 얼마든지 만들 수 있다.

💡 **중첩 타입 파라미터**
제네릭 객체를 제네릭 타입 파라미터로 받는 형식도 표현할 수 있다.ArrayList 자체도 하나의 타입으로써 제네릭 타입 파라미터가 될수 있기 때문에 이렇게 중첩 형식으로 사용할 수 있는 것이다.

**제네릭 사용 이유와 이점**

1. 컴파일 타임에 타입 검사를 통해 예외 방지
2. 불필요한 캐스팅을 없애 성능 향상

**제네릭 사용 주의사항**

1. 제네릭 타입의 객체는 생성이 불가
    
    ```java
    class Sample<T> {
        public void someMethod() {
            // Type parameter 'T' cannot be instantiated directly
            T t = new T();
        }
    }
    ```
    
2. static 멤버에 제네릭 타입이 올 수 없음
    
    ```java
    class Student<T> {
        private String name;
        private int age = 0;
    
        // static 메서드의 반환 타입으로 사용 불가
        public static T addAge(int n) {
    
        }
    }
    
    class Student<T> {
        private String name;
        private int age = 0;
    
        // static 메서드의 매개변수 타입으로 사용 불가
        public static void addAge(T n) {
    
        }
    }
    ```
    
3. 제네릭으로 배열 선언 주의점
    
    ```java
    class Sample<T> { 
    }
    
    public class Main {
        public static void main(String[] args) {
            Sample<Integer>[] arr1 = new Sample<>[10];
        }
    }
    ```
    
    new Sample`<>`[10];으로 인해 에러 발생
    

출처

---

[https://inpa.tistory.com/entry/JAVA-☕-제네릭Generics-개념-문법-정복하기](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%A0%9C%EB%84%A4%EB%A6%ADGenerics-%EA%B0%9C%EB%85%90-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%B3%B5%ED%95%98%EA%B8%B0)