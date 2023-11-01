### 🔎 **캐스팅(Casting)이란?**

캐스팅이란 **타입을 변환하는 것**을 말하며 형변환이라고도 한다. 자바의 상속 관계에 있는 부모와 자식 클래스 간에는 서로 간의 형변환이 가능하다.

![casting1](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/bd409d9f-07ce-4b2d-b843-68342e30f023)

⬆️ **업캐스팅(Upcasting)**

업캐스팅이란 **자식 클래스의 객체(Sub-Class)가 부모 클래스(Super-Class) 타입으로 형변환 되는 것**을 말한다.

- 자동으로 타입이 변환되는 `promotion` 방식으로 처리된다.
- 업캐스팅된 서브 클래스 객체는 슈퍼클래스의 메소드만 호출이 가능하다.

아래 코드에서 부모 클래스는 `Person`, 자식 클래스는 `Student`이다.

아래 코드에서 **`Person p = s;`** 부분이 업캐스팅한 부분이다. p가 Student 객체를 가리키지만, p는 Person 타입이기 때문에 Person 클래스의 멤버에만 접근이 가능하다. 그렇기 때문에 p.check에서 컴파일 타임 에러가 발생한다.

```java
class Person{
	String name;
	Person(String name){
		this.name = name;
	}
}

class Student extends Person{
	String check;
	Student(String name){
		super(name);
	}
}

public class Main{
	public static void main(String[] args){
		Student s = new Student("홍길동");
		Person p = s;// 업캐스팅
		p.name = "이름이다.";

		p.check = "컴파일 에러 발생";// 컴파일 에러 발생
	}
}
```

🔽 **다운캐스팅(Downcasting)**

업캐스팅과 반대로 캐스팅 하는 것을 다운캐스팅이라고 한다. 업캐스팅된 것을 다시 원상태로 돌리는 것을 말한다. 하위 클래스로의 다운캐스팅을 할때는 타입을 명시적으로 지정해줘야한다는 특징이 있다.

- 업캐스팅 문제를 해결하기 위한 또 다른 방법이다.

아래 코드를 보면 **`Student s = (Student)p;`** 라고 나오는데 이 부분이 바로 다운캐스팅이다.

```java
class Person{
	String name;
	Person(String name){
		this.name = name;
	}
}

class Student extends Person{
	String check;
	Student(String name){
		super(name);
	}
}

public class Main{
	public static void main(String[] args){
		Person p = new Student("홍길동");

		Student s = (Student)p;// 다운캐스팅
		s.name = "김유신";
		s.check = "check!";
	}
}
```

### 🔎 주의할 점

같은 부모 클래스를 상속받고 있더라도 **형제 클래스 끼리는 아예 타입이 다르기 때문에 참조 형변환 불가능**하다.

![casting2](https://github.com/Fun-Fun-Study/CS-Study/assets/101235186/7d17bc1f-2667-4e4d-ac8a-2f46263ba744)

Cat과 Dog는 서로 참조 캐스팅이 불가능하다.

<details>
<summary>다양한 예제 및 출처</summary>
<div markdown="1">

[https://velog.io/@duck-ach/14.-업-캐스팅Up-Casting과-다운-캐스팅Down-Casting-JAVA](https://velog.io/@duck-ach/14.-%EC%97%85-%EC%BA%90%EC%8A%A4%ED%8C%85Up-Casting%EA%B3%BC-%EB%8B%A4%EC%9A%B4-%EC%BA%90%EC%8A%A4%ED%8C%85Down-Casting-JAVA)

[https://inpa.tistory.com/entry/JAVA-☕-업캐스팅-다운캐스팅-한방-이해하기](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%97%85%EC%BA%90%EC%8A%A4%ED%8C%85-%EB%8B%A4%EC%9A%B4%EC%BA%90%EC%8A%A4%ED%8C%85-%ED%95%9C%EB%B0%A9-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)

</div>
</details>
