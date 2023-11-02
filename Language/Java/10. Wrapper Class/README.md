# 💫 Wrapper Class

    기본 타입(Primitive Type)을 객체로 다루기 위해서 사용하는 클래스들을 래퍼 클래스라고 합니다.

- 자바는 모든 기본 타입 값을 갖는 객체를 생성할 수 있습니다.
- 래퍼 클래스로 감싸고 있는 기본 타입 값은 외부에서 변경할 수 없습니다.
  - 값을 변경하려면 새로운 Wrapper Class를 만들어야 합니다.

<br>

| 기본타입 | 래퍼클래스 |
| :------: | :--------: |
|   btye   |    Byte    |
|   char   |  Charater  |
|   int    |  Integer   |
|  float   |   Float    |
|  double  |   Double   |
| boolean  |  Boolean   |
|   long   |    Long    |
|  short   |   Short    |

<br>

## Wrapper Class 구조도

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/cfbdd1ef-7cb5-4923-af27-bfba71fb1281">

모든 래퍼 클래스의 부모는 Object이고 내부적으로 숫자를 나루는 래퍼클래스의 부모 클래스는 Number클래스 입니다.

<br>

## Boxing과 UnBoxing

- **Boxing**: 기본 타입의 값을 포장 객체로 만드는 과정
- **UnBoxing**: 포장 객체에서 기본 타입의 값을 얻어내는 과정

<br>

```java
public class Trans_Wrapper {
    public static void main(String[] args){
        String str1 = "10";
        String str2 = "10.5";
        String str3 = "true";

        byte b = Byte.parseByte(str1);
        int i = Integer.parseInt(str1);
        short s = Short.parseShore(str1);
        long l = Long.parseLong(str1);
        float f = Float.parseFloat(str2);
        double d = Double.parseDouble(str2);
        boolean bool = Boolean.parseBoolean(str3);
    }
}

```

<br>

```java
public class Compare {
    public static void main(String[] args)  {
        Integer num1 = new Integer(10); //래퍼 클래스1
        Integer num2 = new Integer(10); //래퍼 클래스2
        int i = 10; //기본타입

        System.out.println((num1 == i)); //true
        System.out.println(num1.equals(i)); //true
        System.out.println((num1 == num2)); //false
        System.out.println(num1.equals(num2)); //true
    }
}

```
