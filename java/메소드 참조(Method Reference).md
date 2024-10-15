# 메소드 참조(Method Reference)

자바 메소드 참조(`Method Reference`)는 람다 표현식을 더 간결하게 표현할 수 있는 방법 중 하나로, 메소드 참조를 사용하면 이미 정의된 메소드를 재사용하여 코드를 더 간단하게 만들 수 있습니다.

## 메소드 참조의 유형

### 정적 메소드 참조

정적 메소드를 참조할 때 사용합니다.

#### 문법

```java
클래스명::정적메소드명
```

#### 예제 코드

```java
List<Integer> numbers = Arrays.asList(1, -5, 2, -7, -3);
numbers.stream().map(Math::abs).forEach(System.out::println);
```

- `Math::abs`는 `Math.abs()` 정적 메소드를 참조합니다.

### 인스턴스 메소드 참조

특정 객체의 인스턴스 메소드를 참조할 때 사용합니다.

#### 문법

```java
객체참조::인스턴스메소드명
```

#### 예제 코드

```java
List<Person> people = Arrays.asList(new Person("Alice"), new Person("Bob"));
people.forEach(Person::printName);
```

- `Person::printName`은 `Person` 객체의 `printName()` 메소드를 참조합니다.

### 생성자 참조

생성자를 참조할 때 사용합니다.

#### 문법

```java
클래스명::new
```

#### 예제 코드

```java
Supplier<Person> personSupplier = Person::new;
Person person = personSupplier.get();
```

- `Person::new`는 `Person` 클래스의 생성자를 참조합니다.

### 메소드 참조의 장점

**1. 간결성:** 람다 표현식보다 더 짧고 읽기 쉬운 코드를 작성할 수 있습니다.
**2. 재사용성:** 이미 정의된 메소드를 재사용할 수 있어 코드 중복을 줄일 수 있습니다.
**3. 가독성:** 메소드 이름을 직접 사용하므로 코드의 의도를 더 명확하게 표현할 수 있습니다.
