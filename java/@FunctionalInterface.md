# @FunctionalInterface이란

`@FunctionalInterface`는 Java 8에서 도입된 어노테이션으로, 함수형 인터페이스를 명시적으로 선언하는 데 사용됩니다.

### 함수형 인터페이스 정의

`@FunctionalInterface`가 붙은 인터페이스는 오직 하나의 추상 메소드만 가질 수 있습니다.
이는 함수형 인터페이스의 핵심 조건입니다.

### 컴파일 시점 검증

이 어노테이션을 사용하면 컴파일러가 해당 인터페이스가 함수형 인터페이스의 조건을 만족하는지 검사합니다.
만약 조건을 위반하면 컴파일 오류가 발생합니다.

### 추가 메소드 허용

함수형 인터페이스는 하나의 추상 메소드 외에도 다음을 포함할 수 있습니다

- **default 메소드:** 구현이 제공된 메소드
- **static 메소드:** 인터페이스에 정의된 정적 메소드
- **Object 클래스의 public 메소드:** `equals()`, `toString()` 등

#### 사용 예시

```java
@FunctionalInterface
interface CustomInterface<T> {
    T myCall();

    default void printDefault() {
        System.out.println("Hello Default");
    }

    static void printStatic() {
        System.out.println("Hello Static");
    }
}
```

- `myCall()`이 유일한 추상 메소드이며, `default`와 `static` 메소드는 함수형 인터페이스 조건에 영향을 주지 않습니다.

### 람다 표현식과의 관계

`@FunctionalInterface`로 선언된 인터페이스는 람다 표현식으로 구현될 수 있습니다.
이는 Java에서 함수형 프로그래밍을 가능하게 하는 핵심 요소입니다2.

#### 주요 함수형 인터페이스

Java 표준 라이브러리는 여러 함수형 인터페이스를 제공합니다.

- `Predicate<T>: T -> boolean`
- `Consumer<T>: T -> void`
- `Function<T, R>: T -> R`
- `Supplier<T>: () -> T`
- `Comparator<T>: (T, T) -> int`
- `Runnable: () -> void`
- `Callable<V>: () -> V12`

이러한 표준 함수형 인터페이스들은 다양한 상황에서 유용하게 사용될 수 있습니다.
