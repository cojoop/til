# 참조 변수 super와 생성자 super()

자바에서 `super`는 부모 클래스와 관련된 동작을 수행할 때 사용되는 키워드입니다.

1. **super 참조 변수:** 부모 클래스의 멤버(필드나 메서드)에 접근할 때 사용됩니다.
2. **super( ) 생성자 호출:** 부모 클래스의 생성자를 명시적으로 호출할 때 사용됩니다.

## 1. super 참조 변수

`super` 참조 변수는 부모 클래스의 멤버에 접근할 때 사용됩니다. 이는 자식 클래스에서 부모 클래스와 같은 이름의 필드나 메서드가 있을 때, 부모 클래스의 것을 명시적으로 호출하는 데 유용합니다.

#### 예제 코드

```java
class Animal {
    String name = "Animal";

    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    String name = "Dog";  // 부모 클래스와 같은 이름의 필드

    @Override
    public void sound() {
        super.sound();  // 부모 클래스의 sound() 호출
        System.out.println("Dog barks");
    }

    public void displayNames() {
        System.out.println("Child class name: " + name);        // 자식 클래스 필드
        System.out.println("Parent class name: " + super.name);  // 부모 클래스 필드
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sound();        // 부모의 sound() + 자식의 sound() 호출
        dog.displayNames();  // 자식과 부모의 필드 출력
    }
}

// 실행결과
Animal makes a sound
Dog barks
Child class name: Dog
Parent class name: Animal
```

- `super.sound()`는 자식 클래스의 `sound()` 메서드 내에서 부모 클래스의 `sound()` 메서드를 호출합니다.
- `super.name`은 자식 클래스와 동일한 이름의 필드가 있을 때, 부모 클래스의 필드에 접근하는 방법을 보여줍니다.

## 2. super() 생성자 호출

`super()`는 부모 클래스의 생성자를 호출하는 역할을 합니다. 자식 클래스의 생성자가 호출될 때는 먼저 부모 클래스의 생성자가 호출되어야 합니다.

이때 부모 클래스의 기본 생성자가 자동으로 호출되지만, 부모 클래스에 인자가 있는 생성자를 호출하려면 명시적으로 `super()`를 사용해야 합니다.

### 기본 생성자 호출

만약 부모 클래스에 명시된 생성자가 없거나 기본 생성자가 정의되어 있다면, 자식 클래스의 생성자가 부모 클래스의 기본 생성자를 자동으로 호출합니다.

#### 예제 코드

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        super();  // 부모 클래스의 기본 생성자 호출 (생략 가능)
        System.out.println("Dog constructor");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();  // 객체 생성
    }
}

// 실행결과
Animal constructor
Dog constructor
```

### 인자 있는 생성자 호출

부모 클래스에 인자가 있는 생성자가 있을 경우, 자식 클래스의 생성자에서 명시적으로 `super(인자)`를 사용하여 호출할 수 있습니다.

#### 예제 코드

```java
class Animal {
    String name;

    Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor: " + name);
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);  // 부모 클래스의 인자 있는 생성자 호출
        System.out.println("Dog constructor: " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Buddy");  // 객체 생성
    }
}

// 실행결과
Animal constructor: Buddy
Dog constructor: Buddy
```

- `super(name)`는 부모 클래스 Animal의 생성자 `Animal(String name)`을 호출합니다.
- 부모 클래스의 생성자가 먼저 실행된 후, 자식 클래스의 생성자가 실행됩니다.

> **`super()` 관련 주의 사항**
>
> 1. **`super()`는 항상 첫 번째로 호출되어야 함:** 자식 클래스 생성자 내에서 `super()`는 첫 번째 줄에 있어야 하며, 그렇지 않으면 컴파일 오류가 발생합니다.
> 2. **명시적 호출이 없을 때:** 자식 클래스 생성자에서 `super()`를 명시하지 않으면, 자바는 부모 클래스의 기본 생성자를 자동으로 호출합니다. 만약 부모 클래스에 기본 생성자가 정의되어 있지 않으면, 명시적으로 `super(인자)`를 호출해야 합니다.
