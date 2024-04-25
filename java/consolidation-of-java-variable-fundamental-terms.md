# 자바 변수 기초 용어 정리

### 인스턴스 변수 (객체 변수, non-static 필드)

인스턴스 변수는 클래스의 각 인스턴스(객체)마다 개별적으로 유지되는 변수입니다. 클래스 내부에 선언되며, 클래스의 객체가 생성될 때마다 새로운 메모리 공간이 할당됩니다.

```java
public class Car {
    String color; // 인스턴스 변수

    public void setColor(String newColor) {
        color = newColor;
    }
}
```

- 인스턴스 변수는 객체의 상태를 나타내는데 사용됩니다.

### 클래스 변수 (static 필드)

클래스 변수는 해당 클래스의 모든 인스턴스가 공유하는 변수입니다. 클래스 내부에 `static` 키워드로 선언되며, 프로그램이 시작될 때 메모리에 할당되고 프로그램이 종료될 때까지 유지됩니다.

```java
public class Circle {
    static final double PI = 3.14159; // 클래스 변수

    public static double calculateArea(double radius) {
        return PI * radius * radius;
    }
}
```

- 클래스 변수는 객체 간에 데이터를 공유할 때 사용됩니다.

### 인스턴스 메소드 (일반 메소드)

인스턴스 메소드는 객체의 인스턴스 변수를 조작하고 클래스의 동작을 수행하는 메소드입니다.

```java
public class Person {
    private String name; // 인스턴스 변수

    public void setName(String newName) { // 인스턴스 메소드
        name = newName;
    }

    public String getName() { // 인스턴스 메소드
        return name;
    }
}
```

- 인스턴스 메소드는 특정 객체에 대해 작업을 수행하는 데 사용됩니다.

### 로컬 변수 (지역 변수)

로컬 변수는 메소드, 생성자 또는 블록 내에서 선언되는 변수입니다. 해당 블록 내에서만 유효하며 메소드가 실행될 때 스택 메모리에 할당되고 메소드 실행이 종료되면 제거됩니다.

```java
public class Calculator {
    public int add(int a, int b) { // 메소드
        int sum = a + b; // 로컬 변수
        return sum;
    }
}
```

- 로컬 변수는 특정 블록 내에서 임시 데이터를 저장할 때 사용됩니다.

### static 메소드 (정적 메소드)

정적 메소드는 클래스의 인스턴스 없이 호출할 수 있는 메소드입니다. 클래스 레벨에서 독립적으로 작동하며, 일반적으로 유틸리티 기능을 구현하는 데 사용됩니다.

```java
public class MathUtil {
    public static int add(int a, int b) { // 정적 메소드
        return a + b;
    }
}
```

- 정적 메소드는 특정 객체에 종속되지 않는 독립적인 작업을 수행할 때 사용됩니다.
