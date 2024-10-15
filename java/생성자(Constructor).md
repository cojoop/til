# 생성자(Constructor)란

생성자(`Constructor`)는 자바에서 객체를 초기화하는 특별한 메서드입니다.
객체가 생성될 때 자동으로 호출되어 중요한 역할을 수행합니다.

### 생성자의 정의와 특징

생성자는 다음과 같은 특징을 가집니다.

- 클래스 이름과 동일한 이름을 가집니다.
- 리턴 타입이 없으며, void도 사용하지 않습니다.
- 객체 생성 시 new 키워드와 함께 자동으로 호출됩니다.
- 인스턴스 변수를 초기화하고 객체 사용 준비를 합니다.

#### 생성자의 종류

**1. 기본 생성자:** 매개변수가 없는 생성자로, 클래스에 생성자가 명시되지 않으면 컴파일러가 자동으로 제공합니다.
**2. 매개변수가 있는 생성자:** 객체 생성 시 특정 값으로 초기화할 때 사용합니다.
**3. 복사 생성자:** 다른 객체의 상태를 복사하여 새 객체를 초기화할 때 사용합니다.

#### 생성자 사용 예시

```java
public class Book {
    private String title;
    private String author;

    // 기본 생성자
    public Book() {
        this.title = "Unknown";
        this.author = "Unknown";
    }

    // 매개변수가 있는 생성자
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
}

// 사용 예
Book book1 = new Book();  // 기본 생성자 호출
Book book2 = new Book("Java Programming", "John Doe");  // 매개변수가 있는 생성자 호출
```

### 생성자 오버로딩

클래스는 여러 개의 생성자를 가질 수 있으며, 이를 생성자 오버로딩이라고 합니다.
매개변수의 개수나 타입을 다르게 하여 다양한 방식으로 객체를 초기화할 수 있습니다.

### this 키워드 사용

생성자 내에서 `this` 키워드를 사용하여 인스턴스 변수에 접근하거나 다른 생성자를 호출할 수 있습니다.

```java
public class Example {
    int value1;
    int value2;

    Example(int value1, int value2) {
        this.value1 = value1;
        this.value2 = value2;
    }
}
```
