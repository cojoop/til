# 자바 메소드 참조

자바 메소드 참조(`Method Reference`)는 람다 표현식을 더 간결하게 표현할 수 있는 방법 중 하나로, 메소드의 참조를 이용하여 코드를 단축시키고 가독성을 높일 수 있습니다. 메소드 참조는 다양한 상황에서 사용될 수 있으며, 주로 함수형 인터페이스를 구현하는 람다 표현식의 대안으로 사용됩니다.

### 메소드 참조의 네 가지 유형

1. 정적 메소드 참조(`Static Method Reference`)
2. 인스턴스 메소드 참조(`Instance Method Reference`)
3. 클래스의 인스턴스 메소드 참조(`Class::instanceMethod`)
4. 생성자 참조(`Constructor Reference`)

## 정적 메소드 참조(Static Method Reference)

정적 메소드 참조는 정적 메소드를 호출하는 간단한 방법을 제공합니다. 함수형 인터페이스의 메소드를 정확히 일치하는 정적 메소드로 매핑하는 데 사용됩니다.

- 람다 표현식에서는 `클래스이름::메소드이름` 형식으로 정적 메소드를 참조할 수 있습니다.

```java
// 예제: 문자열을 정수로 변환하는 정적 메소드
class StringUtil {
    public static int stringToInt(String str) {
        return Integer.parseInt(str);
    }
}

// 정적 메소드 참조를 사용하여 람다 표현식을 간결하게 표현
Function<String, Integer> stringToIntFunction = StringUtil::stringToInt
```

- `StringUtil` 클래스의 `stringToInt` 메소드를 `Function<String, Integer>` 형식의 함수형 인터페이스에 매핑합니다.
- 정적 메소드를 호출할 때는 클래스 이름과 메소드 이름을 사용하여 정확한 메소드를 지정합니다.

## 인스턴스 메소드 참조(Instance Method Reference)

인스턴스 메소드 참조는 객체의 인스턴스 메소드를 호출하는 방법을 제공합니다. 주로 람다 표현식에서 인스턴스 메소드를 호출하는 데 사용됩니다.

- 람다 표현식에서는 `객체참조::메소드이름` 형식으로 인스턴스 메소드를 참조할 수 있습니다.

```java
// 예제: 문자열을 출력하는 인스턴스 메소드
class Printer {
    public void print(String str) {
        System.out.println(str);
    }
}

// 인스턴스 메소드 참조를 사용하여 람다 표현식을 간결하게 표현
Printer printer = new Printer();
Consumer<String> printConsumer = printer::print;
```

- `Printer` 클래스의 `print` 메소드를 `Consumer<String>` 형식의 함수형 인터페이스에 매핑합니다.
- `Printer` 클래스의 인스턴스를 생성한 후에 해당 인스턴스의 메소드를 호출합니다.

## 클래스의 인스턴스 메소드 참조(Class::instanceMethod)

클래스의 인스턴스 메소드 참조는 클래스의 인스턴스 메소드를 호출하는 방법을 제공합니다. 주로 람다 표현식에서 비교나 변환과 같은 작업을 수행하는 데 사용됩니다.

- 람다 표현식에서는 `클래스이름::인스턴스메소드이름` 형식으로 클래스의 인스턴스 메소드를 참조할 수 있습니다.

```java
// 예제: 문자열을 비교하는 인스턴스 메소드
class StringComparator {
    public int compare(String str1, String str2) {
        return str1.compareTo(str2);
    }
}

// 클래스의 인스턴스 메소드 참조를 사용하여 람다 표현식을 간결하게 표현
StringComparator stringComparator = new StringComparator();
Comparator<String> compareFunction = stringComparator::compare;
```

- `StringComparator` 클래스의 `compare` 메소드를 `Comparator<String>` 형식의 함수형 인터페이스에 매핑합니다.
- `StringComparator` 클래스의 인스턴스를 생성한 후에 해당 인스턴스의 메소드를 호출합니다.

## 생성자 참조(Constructor Reference)

생성자 참조는 객체의 생성을 위해 생성자를 참조하는 방법을 제공합니다. 주로 객체를 생성하는 데 사용됩니다.

- 람다 표현식에서는 `클래스이름::new` 형식으로 생성자를 참조할 수 있습니다.

```java
// 예제: Person 객체를 생성하는 생성자
class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

// 생성자 참조를 사용하여 람다 표현식을 간결하게 표현
Supplier<Person> personSupplier = Person::new;
Person person = personSupplier.get();
```

- `Person` 클래스의 생성자를 `Supplier<Person>` 형식의 함수형 인터페이스에 매핑합니다.
- 생성자 참조를 사용하면 객체를 생성하는 코드를 간결하게 표현할 수 있습니다.
