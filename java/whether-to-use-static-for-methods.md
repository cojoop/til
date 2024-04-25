# 메서드에 static 사용 여부

`Java`에서는 메소드를 정의할 때 `static` 키워드를 사용하여 정적 메소드(`static method`)와 일반 메소드(`instance method`)를 구분합니다.

## 정적 메소드 (Static Method)

정적 메소드는 클래스에 속한 메소드로, 클래스의 인스턴스와 관련이 없이 호출될 수 있습니다. 이 메소드는 클래스의 인스턴스가 생성되지 않아도 호출할 수 있기 때문에 클래스 이름을 통해 직접 접근할 수 있습니다. 주로 공통적인 유틸리티 메소드나 특정한 기능을 수행하는 메소드를 정의할 때 사용됩니다.

```java
public class MyClass {
    static int y;

    static void staticMethod() {
        System.out.println("This is a static method.");
    }

    static void anotherStaticMethod(int x, int y) {
        System.out.println("x: " + x);
        System.out.println("y: " + y);
    }
}

// 정적 메소드 호출
MyClass.staticMethod();
MyClass.anotherStaticMethod(5, 10);
System.out.println(MyClass.y);
```

## 일반 메소드 (Instance Method)

일반 메소드는 클래스의 인스턴스에 속한 메소드로, 해당 클래스의 객체가 생성되어야만 호출될 수 있습니다. 이 메소드는 객체의 상태를 변경하거나 객체에 속한 필드를 사용할 수 있습니다.

```java
public class MyClass {
    int x;

    void instanceMethod() {
        System.out.println("This is an instance method.");
    }

    void anotherInstanceMethod() {
        System.out.println("x: " + x);
    }
}

// 객체 생성
MyClass myObject = new MyClass();

// 일반 메소드 호출
myObject.instanceMethod();
myObject.anotherInstanceMethod();
```

#### 정적 메소드와 일반 메소드를 구분하는 경우

- 정적 메소드는 클래스의 인스턴스를 생성하지 않고도 호출할 수 있으며, 클래스 이름을 통해 호출됩니다.
- 일반 메소드는 해당 클래스의 객체가 생성되어야 호출할 수 있으며, 객체를 통해 호출됩니다.

정적 메소드는 어떤 객체의 상태에 의존하지 않고 독립적으로 작동해야 하며, 이에 따라 주로 유틸리티성을 가집니다. 일반 메소드는 특정 객체의 상태를 변경하거나 해당 객체에 특화된 작업을 수행합니다.
