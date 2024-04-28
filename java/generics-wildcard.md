# 제네릭스의 와일드카드

제네릭스에서 와일드카드는 제네릭 타입을 좀 더 유연하게 다루기 위한 기능입니다. 와일드카드를 사용하면 타입 매개변수를 정확히 알 수 없는 상황에서도 제네릭 타입을 사용할 수 있습니다.

와일드카드는 주로 세 가지 형태로 사용됩니다.

- **미지정 와일드카드 (`<?>`):** 어떤 타입 매개변수가 될지 정확히 알 수 없는 경우 사용됩니다.
  - ex) `List<?>`는 "모든 종류의 List"를 의미합니다.

- **상한 와일드카드 (`<? extends T>`):** 특정 타입의 하위 타입일 수 있는 타입들을 나타냅니다. 이를 통해 제네릭 클래스나 메서드를 더 일반화할 수 있습니다.
  - ex) `List<? extends Number>`는 Number 또는 Number의 하위 타입을 저장할 수 있는 리스트를 나타냅니다.

- **하한 와일드카드 (`<? super T>`):** 특정 타입의 상위 타입일 수 있는 타입들을 나타냅니다. 이를 사용하면 특정 타입의 상위 클래스를 사용하는 경우 유용합니다.
  - ex) `List<? super Integer>`는 Integer의 상위 클래스를 저장할 수 있는 리스트를 나타냅니다.

## 와일드카드(?)와 extends

와일드카드(`?`)와 `extends` 키워드를 함께 사용하면, 특정 클래스 또는 그 하위 클래스의 객체들을 다룰 수 있습니다.

```java
import java.util.*;

public class WildcardDemo {
    public static double sum(List<? extends Number> list) {
        double sum = 0.0;
        for (Number num : list) {
            sum += num.doubleValue();
        }
        return sum;
    }

    public static void main(String[] args) {
        List<Integer> integers = Arrays.asList(1, 2, 3);
        System.out.println("Sum of integers: " + sum(integers));

        List<Double> doubles = Arrays.asList(1.5, 2.5, 3.5);
        System.out.println("Sum of doubles: " + sum(doubles));
    }
}
```

- `sum` 메서드는 `List<? extends Number>`를 매개변수로 받아들이고 있습니다.
- 이렇게 함으로써 Integer 또는 Double과 같은 Number 클래스의 하위 클래스의 리스트를 인수로 전달할 수 있습니다.

## 와일드카드(?)와 super

와일드카드(`?`)와 ``super`` 키워드를 함께 사용하면, 특정 클래스 또는 그 상위 클래스의 객체들을 다룰 수 있습니다.

```java
import java.util.*;

public class WildcardDemo {
    public static void addNumbers(List<Integer> list) {
        for (int i = 1; i <= 5; i++) {
            list.add(i);
        }
    }

    public static void main(String[] args) {
        List <? super Integer> integerList = new ArrayList<>();
        addNumbers(integerList);
        System.out.println("List of integers: " + integerList);
    }
}
```

- `addNumbers` 메서드는 `List<? super Integer>`를 매개변수로 받아들이고 있습니다.
- 이렇게 함으로써 `Integer` 클래스 또는 `Integer`의 상위 클래스의 리스트를 인수로 전달할 수 있습니다.
- 이 경우 `addNumbers` 메서드는 1부터 5까지의 정수를 해당 리스트에 추가합니다.

### 와일드카드의 활용

와일드카드와 함께 사용되는 `extends`와 `super` 키워드는 제네릭 메서드와 컬렉션 클래스의 유연성을 높여줍니다. 이를 통해 코드의 재사용성과 가독성을 향상시킬 수 있습니다. 특히 제네릭 타입이 복잡한 상속 구조를 가지고 있는 경우에는 이러한 와일드카드 문법이 매우 유용하게 활용될 수 있습니다.
