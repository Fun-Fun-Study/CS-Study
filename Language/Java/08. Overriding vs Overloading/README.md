# 💦 Overriding

    부모 클래스로부터 상속받은 메소드를 자식 클래스에서 재정의

```java
public class OverridingTest {
	public static void main(String[] args) {
		Person person = new Person();
		Child child = new Child();

		person.cry();
		child.cry();
	}
}

class Person {
	void cry() {
		System.out.println("오버라이딩1");
	}
}

class Child extends Person {
	@Override
	protected void cry() {
		System.out.println("오버라이딩2");
	}
}

```

### 조건

- 자식 클래스에서는 오버라이딩하고자 하는 메소드의 이름, 매개변수, 리턴 값이 모두 같아야 한다.
- 선언부는 부모의 것과 완벽히 동일해야 한다.
- 자식 클래스에서 오버리이딩하는 메소드의 접근 제엊자는 부모 클래스보다 좁게 설정할 수 없다.
- 예외는 부모 클래스의 메소드보다 많이 선언할 수 없다.
- static 메소드를 인스턴스의 메소드 또는 그 반대로 바꿀 수 없다.

<br>

# 💦 Overloading

    자바의 한 클래스 내에 이미 사용하려는 이름과 같은 이름을 가진 메소드가 있더라도
    매개변수의 개수 또는 타입이 다르면,
    같은 이름을 사용해서 메소드 정의가 가능하다.

```java
public static void main(String[] args){
    method m = new method();

    m.print();
    m.print(3);
    m.print("Hello");
    m.print(1, 2);
}

public void print() {
    System.out.println("오버로딩1");
}

String print(int a){
    System.out.println("오버로딩2");
    return a.toString();
}

void print(String a){
    System.out.println("오버로딩3");
}

String print(int a, int b){
    System.out.println("오버로딩4");
    return a.toString() + b.toString();
}

```

### 조건

- 메소드의 이름이 같고, 매개변수의 개수나 타입이 달라여 한다.
- **리턴 값만** 다른 것은 오버로딩을 할 수 없다.
- 접근 제어자 자유롭게 지정 가능.
  public, default, protected, private 등으로 다르게 지정해도 상관없다.
  **접근 제어자만** 다른 것도 오버로딩 불가능
- **매개변수의 차이로만 구현할 수 있다.**

### 사용 이유

- 같은 기능을 하는 메소드를 하나의 이름으로 사용할 수 있다.
- 메소드의 이름을 절약할 수 있다.

<br><br>

# 비교

|   구분    |            OverRiding            |               OverLoading               |
| :-------: | :------------------------------: | :-------------------------------------: |
|   정의    | 상속받은 메소드를 재정의 하는 것 | 기존에 없던 새로운 메소드를 추가하는 것 |
|  리턴형   |               동일               |              달라도 된다.               |
| 메소드명  |               동일               |                  동일                   |
| 매개변수  |               동일               |             달라야만 한다.              |
| 적용 범위 |             상속관계             |             같은 클래스 내              |
