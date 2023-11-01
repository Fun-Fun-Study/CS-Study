함수가 인수를 전달할 때 사용되는 방식이며, 값고 참조를 호출하는 차이가 있습니다.

<br>

# 📞 Call by Value

- 함수가 인수로 전달받은 값을 복사하여 처리하는 방식
- 변수가 가진 값을 복사하여 전달하므로 함수 내에서 값을 변경해도 **원본 값은 변경되지 않음**
- 값의 불변성을 유지하는 데에 용이
- Just 값만 전달

```java
public static void main(String[] args) {
  int a = 1, b = 2;
  System.out.println(a+" "+b); // 1 2
  method(a, b);
  System.out.println(a+" "+b); // 1 2
}
public void method(int a, int b){
  a = 3; b = 4;
  System.out.println(a+" "+b); // 3 4
}

```

### 장점

복사하여 처리하기 때문에 안전하며 원래 값 보존

<br>

### 단점

복사를 하기 때문에 메모리 사용량이 증가

<br>

# 📞 Call by Reference

- 함수 호출 시 인수로 전달되는 변수의 참조 값을 함수 내부로 전달하는 방식
- 힘수 내에서 인자로 전달된 변수의 값을 변경하면, **호출한 쪽에서도 해당 변수의 값이 변경**
- 인자로 전달되는 값이 변수의 주소이므로, 함수 내에서 변수의 값을 변경하면 해당 주소에 저장된 값이 변경

```c
int main(){
  string str = "abc";
  printf(str); // abc
  method(str);
  printf(str); // abcdef
}
void method(string &str){
  str+="def";
}

```

### 장점

복사하지 않고 직접 참조를 하기에 빠른 속도

<br>

### 단점

직접 참조를 하기 때문에 원래 값에 영향 (리스크)

> ❔단점을 해결하려면 <br>
> 깊은복사이용 <br>
> But, 깊은복사를 사용하게 되면 속도의 장점을 잃어버릴 수 있지만 불변성을 지켜야 한다면 깊은복사로 보완할 것

<br>

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/452c66ab-d707-44f8-bfe9-ce3a22b09bd4">

<br><br>

## JAVA에서는 Call By Value 로만 동작

<br>

JAVA에서 변수 선언 -> Stack 영역에 할당
<br>

- 원시 타입(Primitive Type)은 Stack 영역에 변수와 함께 저장
- 참조 타입(Reference Type) 객체는 Heap 영역에 저장되고 Stack 영역에 있는 변수가 객체의 주소값을 지님

<br>

원시 타입, 참조 타입을 생성할 때마다 동일한 방식으로 메모리에 할당

**반면, C언어에서는 포인터를 이용해 주소값을 넘겨 Call By Reference로 동작 가능**
