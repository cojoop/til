# Functional Interface 알아보기

`Java`의 `Functional Interface`는 단 하나의 추상 메서드만을 가지고 있는 인터페이스를 말합니다. 기존의 Java 인터페이스에서는 여러 개의 추상 메서드를 가질 수 있었지만, `Functional Interface`는 오직 하나의 추상 메서드만을 허용합니다.
> 그렇기 때문에 이를 구현하는 클래스나 람다 표현식에서는 반드시 해당 추상 메서드를 구현해야 합니다.

## 주요 Functional Interface

### Consumer

`Consumer`는 입력 값을 받아서 처리하는 역할을 합니다.

- 입력 값을 받아서 어떤 동작을 수행하는 것이 주요 목적입니다.

##### 구조

```java
@FunctionalInterface
interface Consumer<T> {
    void accept(T t);
}
```

##### 예제 코드

```java
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        Consumer<String> printer = (s) -> System.out.println(s);
        printer.accept("Hello, Consumer!");
    }
}
```

### Supplier

`Supplier`는 값을 제공하는 역할을 합니다.

- 입력을 받지 않고 값을 반환합니다.

##### 구조

```java
@FunctionalInterface
interface Supplier<T> {
    T get();
}
```

##### 예제 코드

```java
import java.util.function.Supplier;

public class SupplierExample {
    public static void main(String[] args) {
        Supplier<String> supplier = () -> "Hello, Supplier!";
        System.out.println(supplier.get());
    }
}
```

### Function

`Function`은 입력 값을 받아서 다른 값으로 변환하는 역할을 합니다.

##### 구조

```java
@FunctionalInterface
interface Function<T, R> {
    R apply(T t);
}
```

##### 예제 코드

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        Function<String, Integer> lengthCalculator = (s) -> s.length();
        System.out.println(lengthCalculator.apply("Hello, Function!")); // 출력: 17
    }
}
```

### BiFunction

`BiFunction`은 두 개의 인수를 받아서 결과를 반환하는 역할을 수행합니다.

##### 구조

```java
@FunctionalInterface
interface BiFunction<T, U, R> {
    R apply(T t, U u);
}
```

##### 예제 코드

```java
import java.util.function.BiFunction;

public class BiFunctionExample {
    public static void main(String[] args) {
        // 두 정수를 더하여 결과를 반환하는 BiFunction 구현체
        BiFunction<Integer, Integer, Integer> adder = (a, b) -> a + b;
        
        // 5와 3을 더한 결과를 반환
        System.out.println(adder.apply(5, 3)); // 출력: 8
    }
}
```

### Operator

`Operator`는 주어진 입력을 받아서 동일한 유형의 출력을 생성하는 연산을 수행합니다.
> `Java`에서는 다양한 종류의 `Operator`를 제공하고 있습니다.

#### UnaryOperator

`UnaryOperator`는 하나의 입력을 받아서 동일한 유형의 출력을 생성하는 연산을 수행합니다.

```java
// 구조
@FunctionalInterface
interface UnaryOperator<T> extends Function<T, T> {
    // 상속된 메서드인 apply를 통해 하나의 입력을 받아서 동일한 유형의 출력을 생성
}

// 예제 코드
import java.util.function.UnaryOperator;

public class UnaryOperatorExample {
    public static void main(String[] args) {
        // 문자열의 끝에 "!"를 추가하는 UnaryOperator 구현체
        UnaryOperator<String> addExclamation = (s) -> s + "!";
        
        // 입력으로 "Hello"를 주면 "Hello!"를 반환
        System.out.println(addExclamation.apply("Hello")); // 출력: Hello!
    }
}
```

#### BinaryOperator

`BinaryOperator`는 두 개의 입력을 받아서 동일한 유형의 출력을 생성하는 연산을 수행합니다.

```java
// 구조
@FunctionalInterface
interface BinaryOperator<T> extends BiFunction<T,T,T> {
    // 상속된 메서드인 apply를 통해 두 개의 입력을 받아서 동일한 유형의 출력을 생성
}

// 예제 코드
import java.util.function.BinaryOperator;

public class BinaryOperatorExample {
    public static void main(String[] args) {
        // 두 정수를 더하는 BinaryOperator 구현체
        BinaryOperator<Integer> adder = (a, b) -> a + b;
        
        // 5와 3을 더한 결과를 반환
        System.out.println(adder.apply(5, 3)); // 출력: 8
    }
}
```

### Predicate

`Predicate`는 조건을 검사하여 `true` 또는 `false`를 반환하는 역할을 합니다.

##### 구조

```java
@FunctionalInterface
interface Predicate<T> {
    boolean test(T t);
}
```

##### 예제 코드

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = (n) -> n % 2 == 0;
        System.out.println(isEven.test(5)); // 출력: false
    }
}
```

## Functional Interface 사용 이유

`Functional Interface`는 람다 표현식을 이용하여 간결하게 메서드를 정의하고 전달할 수 있도록 해줍니다. 이는 코드의 가독성과 유지보수성을 높여줍니다. 또한, `Java`에서 함수형 프로그래밍을 지원하는 다양한 함수형 인터페이스들이 `Functional Interface`의 형태로 제공되어, 이를 활용하여 다양한 함수형 프로그래밍 패턴을 구현할 수 있습니다.
