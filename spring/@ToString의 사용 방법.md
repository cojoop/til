# 다대다(N:N) 및 일대다(1:N) 관계에서 @ToString의 사용 방법

`@ToString`은 객체의 `toString()` 메서드를 자동으로 생성해줍니다.
다대다(N:N) 또는 일대다(1:N) 관계에서 이를 사용할 때, 주의해야 할 점은 순환 참조(`circular reference`)로 인해 `toString()` 호출 시 스택 오버플로우가 발생할 수 있다는 것입니다.

- JPA와 같은 ORM을 사용할 경우, 엔티티들 간의 참조가 양방향으로 설정되어 있다면 이러한 문제가 자주 발생합니다.

### 문제 상황

- **다대다(N:N):** 두 엔티티가 서로를 양방향으로 참조하고 있을 때, `@ToString`을 양쪽에 걸면 무한 순환 참조가 발생할 수 있습니다.
- **일대다(1:N):** `부모-자식` 관계에서, 부모는 자식 리스트를 가지고 있고 자식은 부모를 참조하는 구조에서 마찬가지로 순환 참조가 발생할 수 있습니다.

#### 해결 방법

`@ToString` 애노테이션을 사용할 때 순환 참조를 피하기 위해 Lombok에서 제공하는 옵션들을 사용할 수 있습니다.

##### 1. exclude 옵션 사용

- 순환 참조가 발생할 수 있는 필드를 `toString()`에서 제외하는 방법입니다.
- 양방향 관계에서 한쪽 필드를 제외하여 순환을 피할 수 있습니다.

```java
@ToString(exclude = "parent")
@Entity
public class Child {
    @ManyToOne
    private Parent parent;
}

@ToString(exclude = "children")
@Entity
public class Parent {
    @OneToMany(mappedBy = "parent")
    private List<Child> children;
}
```

##### 2. @ToString.Include와 @ToString.Exclude 사용

- 특정 필드를 포함하거나 제외할 수 있습니다.

```java
@ToString
@Entity
public class Child {
    @ToString.Exclude
    @ManyToOne
    private Parent parent;
}

@ToString
@Entity
public class Parent {
    @ToString.Exclude
    @OneToMany(mappedBy = "parent")
    private List<Child> children;
}
```

##### 3. @ToString(callSuper = true)

- 상속 관계에서 부모 클래스의 `toString()`을 호출할 수 있는 옵션입니다.
- 주의해서 사용해야 하며, 상속 관계에 한정됩니다.
