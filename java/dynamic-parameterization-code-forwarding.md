# 동적 파라미터화 코드 전달하기

동작 파라미터화(behavior parameterization)는 메소드의 동작을 파라미터로 전달하여 유연하게 제어하는 기법입니다. 이를 통해 동일한 메소드가 다양한 동작을 수행할 수 있게 만듭니다.
자주 사용되는 방식으로는 전략 패턴을 활용한 인터페이스 선언, 익명 클래스, 람다 표현식 등이 있습니다.

## Predicate 인터페이스 선언을 통한 전략 패턴 구현

`Predicate<T>`는 자바 8부터 제공된 함수형 인터페이스로, T 타입의 객체를 인자로 받아 boolean 값을 반환하는 메소드를 정의합니다. 주로 필터링이나 조건 검사를 할 때 사용됩니다.

예시: 전략 인터페이스 선언

```java
// 예제 코드: 전략 인터페이스 선언
import java.util.function.Predicate;

public class TransactionFilter {
    // Predicate 인터페이스를 사용하여 조건에 따라 트랜잭션 필터링
    public static boolean filterTransaction(Transaction transaction, Predicate<Transaction> predicate) {
        return predicate.test(transaction);
    }
}

class Transaction {
    private String type;
    private double amount;

    public Transaction(String type, double amount) {
        this.type = type;
        this.amount = amount;
    }

    public String getType() {
        return type;
    }

    public double getAmount() {
        return amount;
    }
}
```

- `filterTransaction` 메소드는 `Predicate<Transaction>`을 사용하여 트랜잭션 객체의 조건을 동적으로 테스트할 수 있습니다.

## 클래스를 통한 동작 파라미터화

전략 패턴을 구현하기 위해 Predicate 인터페이스를 구현한 클래스를 만들어 동작을 파라미터화할 수 있습니다.

```java
// 예제 코드: 클래스 구현을 통한 동작 파라미터화
class HighValueTransactionPredicate implements Predicate<Transaction> {
    @Override
    public boolean test(Transaction transaction) {
        return transaction.getAmount() > 1000;
    }
}

public class Main {
    public static void main(String[] args) {
        Transaction transaction = new Transaction("credit", 1500);
        Predicate<Transaction> highValuePredicate = new HighValueTransactionPredicate();
        
        boolean result = TransactionFilter.filterTransaction(transaction, highValuePredicate);
        System.out.println("High value transaction: " + result);
    }
}
```

- HighValueTransactionPredicate라는 클래스를 만들어 `Predicate<Transaction>` 인터페이스를 구현하고, 이를 통해 트랜잭션이 1000 이상의 금액을 가진지 여부를 확인하는 동작을 파라미터화했습니다.

## 익명 클래스를 통한 동작 파라미터화

익명 클래스를 사용하면 별도의 클래스를 정의하지 않고 즉시 동작을 정의할 수 있습니다. 이는 단순한 경우에 코드 간결성을 유지하는 데 유용합니다.

```java
// 예제 코드: 익명 클래스를 사용한 동작 파라미터화
public class Main {
    public static void main(String[] args) {
        Transaction transaction = new Transaction("credit", 1500);
        
        // 익명 클래스를 통해 동작 파라미터화
        boolean result = TransactionFilter.filterTransaction(transaction, new Predicate<Transaction>() {
            @Override
            public boolean test(Transaction t) {
                return t.getAmount() > 1000;
            }
        });
        
        System.out.println("High value transaction: " + result);
    }
}
```

- 익명 클래스를 사용하면 별도의 HighValueTransactionPredicate 클래스를 만들지 않고, 메소드 호출 시 바로 조건을 정의할 수 있습니다.

## 람다 표현식을 통한 동작 파라미터화

자바 8 이후로 람다 표현식을 사용하여 훨씬 간결하게 동작 파라미터화를 할 수 있습니다. 람다는 함수형 인터페이스의 인스턴스를 간단한 표현식으로 정의하는 방법입니다.

```java
//  예제 코드: 람다를 사용한 동작 파라미터화
public class Main {
    public static void main(String[] args) {
        Transaction transaction = new Transaction("credit", 1500);

        // 람다 표현식을 통해 동작 파라미터화
        boolean result = TransactionFilter.filterTransaction(transaction, t -> t.getAmount() > 1000);
        
        System.out.println("High value transaction: " + result);
    }
}
```

- 람다를 사용하면 불필요한 클래스 정의나 익명 클래스보다 코드가 더 깔끔하고 직관적입니다.

## 자바 API에서의 동작 파라미터화

자바의 다양한 API에서도 동작 파라미터화가 광범위하게 사용됩니다.
> 대표적인 예로 Comparator 인터페이스를 사용한 정렬, Thread 클래스의 실행 동작을 지정하기 위한 Runnable 인터페이스 등이 있습니다.

```java
// 예제 코드: 정렬
import java.util.Arrays;
import java.util.Comparator;

public class SortExample {
    public static void main(String[] args) {
        String[] names = { "Steve", "Mary", "John", "Patricia" };
        
        // Comparator를 람다로 동작 파라미터화하여 정렬
        Arrays.sort(names, (s1, s2) -> s1.compareToIgnoreCase(s2));
        
        System.out.println(Arrays.toString(names));
    }
}
```

```java
// 예제 코드: 스레드
public class ThreadExample {
    public static void main(String[] args) {
        // Runnable을 람다로 동작 파라미터화
        Thread thread = new Thread(() -> {
            System.out.println("Thread is running");
        });
        thread.start();
    }
}
```
