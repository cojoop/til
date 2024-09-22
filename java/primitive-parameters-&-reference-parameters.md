# 기본형 매개변수와 참조형 매개변수

## 1. 기본형 매개변수 (Primitive Parameters)

기본형 매개변수는 자바에서 기본 데이터 타입(`Primitive types`)을 사용합니다.

#### 기본 데이터 타입

- int, long, short, byte (정수형)
- float, double (실수형)
- char (문자형)
- boolean (논리형)

### 특징

- **값을 복사하여 전달:** 기본형 매개변수는 함수나 메서드에 전달될 때, 그 값 자체가 복사되어 전달됩니다. 즉, 함수 내부에서 매개변수를 변경하더라도 원본 값에는 아무런 영향이 없습니다.
- **메모리 할당:** 기본형 데이터는 스택 메모리에 저장됩니다. 매개변수로 전달되면 새로운 스택 공간에 복사본이 만들어집니다.
- **불변성:** 메서드 내부에서 매개변수의 값을 변경해도 외부에는 영향을 미치지 않습니다. 이는 기본형 매개변수가 값에 의한 호출(`Call by Value`) 방식을 따르기 때문입니다.

#### 예제 코드

```java
public class Test {
    public static void main(String[] args) {
        int a = 10;
        modifyValue(a);
        System.out.println(a);  // 결과: 10
    }

    public static void modifyValue(int x) {
        x = 20;  // 여기서 변경된 x 값은 메인 메서드의 변수 a에 영향을 주지 않음
    }
}
```

## 2. 참조형 매개변수 (Reference Parameters)

참조형 매개변수는 객체나 배열과 같은 참조 타입(`Reference types`)을 사용합니다.

#### 참조형 타입

- String
- 사용자 정의 클래스 (class)
- 배열 (Array)
- List, Set, Map 등 컬렉션

### 특징

- **참조를 전달:** 참조형 매개변수는 객체나 배열의 참조값(메모리 주소)을 전달합니다. 즉, 함수 내부에서 참조형 매개변수를 변경하면 원본 객체에 영향을 줄 수 있습니다.
- **메모리 할당:** 참조형 데이터는 힙 메모리에 저장됩니다. 함수에 전달되는 것은 힙에 있는 객체의 메모리 주소입니다. 따라서 함수 내부에서 이 주소를 통해 객체에 접근하거나 변경할 수 있습니다.
- **가변성:** 참조형 매개변수는 `주소에 의한 호출(Call by Reference)`처럼 작동하므로 함수 내부에서 객체의 상태를 변경하면 원본 객체에도 영향을 미칩니다.

#### 예제 코드

```java
public class Test {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        modifyArray(arr);
        System.out.println(arr[0]);  // 결과: 10
    }

    public static void modifyArray(int[] x) {
        x[0] = 10;  // 참조된 배열의 첫 번째 값을 변경
    }
}
```

## 3. 기본형과 참조형의 반환 타입 차이점

#### 기본형

- 기본형을 반환할 때는 복사된 값이 반환됩니다.
- 메서드 내부에서 수정한 값이 반환되더라도, 외부에서 이를 사용하지 않으면 원본 데이터는 영향을 받지 않습니다

```java
public static int increment(int value) {
    value += 1;
    return value;  // 수정된 값이 반환됨
}
```

#### 참조형

- 참조형을 반환하면 객체의 참조값(주소)을 반환합니다.
- 따라서 반환된 객체는 외부에서도 변경할 수 있으며, 기존 객체와 동일한 메모리 위치를 가리킵니다.

```java
public static int[] modifyAndReturnArray(int[] arr) {
    arr[0] = 100;
    return arr;  // 수정된 배열의 참조값이 반환됨
}
```
