# Predicate란

Predicate는 Java의 `java.util.function` 패키지에 포함된 함수형 인터페이스로, 조건을 검사하는 데 사용됩니다.

### 기본 개념

- 하나의 인자를 받아 boolean 값을 반환하는 함수형 인터페이스입니다.
- Predicate는 주로 Stream API와 함께 사용되며, 데이터를 필터링하거나 특정 조건에 맞는지 검사하는 데 쓰입니다.

### Predicate의 기본 구조

Predicate는 다음과 같은 단일 추상 메서드를 가지고 있습니다.

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```

#### 주요 메서드

##### 1. test(T t)

T 타입의 인수를 받아 조건을 평가하여 true나 false를 반환합니다.

##### 2. and(Predicate other)

두 개의 Predicate를 AND 조건으로 결합합니다. 첫 번째 조건과 두 번째 조건이 모두 참이어야 true를 반환합니다.

##### 3. or(Predicate other)

두 개의 Predicate를 OR 조건으로 결합합니다. 하나라도 참이면 true를 반환합니다.

##### 4. negate()

현재 Predicate 조건의 반대 값을 반환합니다. 즉, test()가 true일 때 false, false일 때 true를 반환합니다.

##### 5. isEqual(Object targetRef)

주어진 객체와 같은지 여부를 검사하는 Predicate를 반환합니다.

### 사용 예시

#### 1. 단순한 Predicate 사용

다음 예제는 Predicate를 사용해 숫자가 짝수인지 검사합니다.

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = number -> number % 2 == 0;
        
        System.out.println(isEven.test(4)); // true
        System.out.println(isEven.test(5)); // false
    }
}
```

#### 2. Predicate와 Stream API 함께 사용하기

Predicate는 Stream API의 filter() 메서드와 함께 자주 사용됩니다. 아래 예제는 Predicate를 사용해 리스트에서 짝수만 필터링합니다.

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;
import java.util.stream.Collectors;

public class StreamPredicateExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
        Predicate<Integer> isEven = number -> number % 2 == 0;

        List<Integer> evenNumbers = numbers.stream()
                                           .filter(isEven)
                                           .collect(Collectors.toList());
        
        System.out.println(evenNumbers); // [2, 4, 6]
    }
}
```

#### 3. 여러 Predicate 조합

Predicate의 and(), or(), negate() 메서드를 사용하여 복합 조건을 구성할 수도 있습니다.

```java
import java.util.function.Predicate;

public class CombinedPredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isPositive = number -> number > 0;
        Predicate<Integer> isEven = number -> number % 2 == 0;

        // 양수이면서 짝수인 조건
        Predicate<Integer> isPositiveAndEven = isPositive.and(isEven);
        System.out.println(isPositiveAndEven.test(4)); // true
        System.out.println(isPositiveAndEven.test(-2)); // false

        // 양수이거나 짝수인 조건
        Predicate<Integer> isPositiveOrEven = isPositive.or(isEven);
        System.out.println(isPositiveOrEven.test(-2)); // true
        System.out.println(isPositiveOrEven.test(-3)); // false
    }
}
```

#### 활용

- 데이터 처리나 컬렉션의 필터링에 유용합니다.
- Stream API와 함께 사용하여 복잡한 조건 로직을 간결하게 표현할 수 있습니다.
- 람다 표현식과 함께 사용하여 코드를 더 간결하고 읽기 쉽게 만들 수 있습니다.
