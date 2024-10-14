# DTO, VO, Entity의 사용 방식

DTO, VO, Entity는 각각 다른 목적과 계층에서 사용되는 객체입니다.
각 객체는 데이터 흐름과 관련된 특정 역할을 수행하며, 이들의 차이점을 명확히 이해하면 애플리케이션의 계층 구조를 잘 설계할 수 있습니다.

## DTO (Data Transfer Object)

DTO는 계층 간 데이터 전송을 위해 사용되는 객체입니다12.

### 주요 특징

- 주로 Controller와 Service 계층 간 데이터 교환에 사용
- `getter/setter` 메서드만 가짐
- 비즈니스 로직을 포함하지 않음
- 주로 `Request/Response` 객체로 활용

#### 사용 예시

```java
public class UserDTO {
    private String name;
    private int age;

    // getter와 setter 메서드
}
```

## VO (Value Object)

VO는 값 그 자체를 표현하는 객체입니다12.

### 주요 특징

- 불변성(`immutability`)을 가짐
- 모든 속성 값이 같으면 동일한 객체로 간주
- `equals()`와 `hashCode()` 메서드를 오버라이드하여 동등성 비교
- 주로 도메인 모델에서 사용

#### 사용 예시

```java
public class Money {
    private final BigDecimal amount;
    private final Currency currency;

    // 생성자, getter 메서드
    // equals(), hashCode() 오버라이드
}
```

## Entity

Entity는 데이터베이스 테이블과 매핑되는 객체입니다2.

### 주요 특징

- JPA를 사용할 때 `@Entity` 어노테이션으로 정의
- 데이터베이스의 테이블과 1:1로 매핑
- 식별자(`ID`)를 가짐
- 비즈니스 로직을 포함할 수 있음

#### 사용 예시

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private int age;

    // 생성자, getter/setter, 비즈니스 메서드
}
```

### 사용 방식 조합

#### Controller 계층

- DTO를 주로 사용하여 클라이언트와 데이터를 주고받습니다.
- Entity나 VO를 직접 노출하지 않아 보안성을 높입니다.

#### Service 계층

- DTO를 받아 Entity로 변환하거나, Entity를 DTO로 변환하는 로직을 구현합니다.
- 비즈니스 로직을 처리하며, 필요에 따라 VO를 사용합니다.

#### Repository 계층

- Entity를 사용하여 데이터베이스와 직접 상호작용합니다.

#### 도메인 모델

- Entity와 VO를 조합하여 도메인 모델을 구성합니다.
