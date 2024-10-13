# @Valid 어노테이션이란

`@Valid` 어노테이션은 Java의 Bean Validation API에서 제공되는 강력한 도구로, 객체의 유효성을 검사하는 데 사용됩니다. 이 어노테이션은 주로 Spring Framework와 함께 사용되어 애플리케이션의 데이터 무결성을 보장하는 데 중요한 역할을 합니다.

## @Valid 어노테이션의 주요 특징

- **객체 검증:** @Valid를 사용하면 객체의 필드에 정의된 제약 조건을 자동으로 검사할 수 있습니다.
- **컨트롤러 레벨 검증:** 주로 컨트롤러 메서드의 파라미터에 적용되어, 클라이언트로부터 받은 데이터의 유효성을 검증합니다.
- **예외 발생:** 유효성 검증에 실패하면 `MethodArgumentNotValidException` 예외가 발생합니다.

## 사용 시기와 이유

### @Valid 어노테이션이 사용되는 경우

- **클라이언트 입력 검증:** 사용자로부터 받은 데이터가 애플리케이션의 요구사항을 충족하는지 확인할 때 사용합니다1.
- **데이터 일관성 유지:** 데이터베이스에 저장되기 전에 데이터의 형식과 내용이 올바른지 확인합니다.
- **비즈니스 로직 보호:** 잘못된 데이터가 애플리케이션의 핵심 로직에 영향을 미치는 것을 방지합니다.

### 사용 시 장점

- **코드 간소화:** 복잡한 if-else 문을 사용하지 않고도 간단하게 유효성 검사를 수행할 수 있습니다1.
- **중앙화된 검증 로직:** 검증 로직을 한 곳에 모아 관리할 수 있어 유지보수가 용이합니다.
- **선언적 프로그래밍:** 어노테이션을 통해 의도를 명확히 표현할 수 있습니다.

### 사용하지 않을 때의 단점

- **수동 검증의 번거로움:** 각 메서드에서 수동으로 유효성 검사를 수행해야 하므로 코드가 복잡해집니다.
- **일관성 부족:** 개발자마다 다른 방식으로 유효성 검사를 구현할 수 있어 일관성이 떨어질 수 있습니다.
- **누락 가능성:** 수동으로 검사할 경우 일부 필드의 검증을 누락할 가능성이 있습니다.

#### 예제 코드

```java
// 컨트롤러에서 @Valid 사용
@Controller
public class UserController {
    @PostMapping("/user")
    public ResponseEntity<String> createUser(@Valid @RequestBody UserDto userDto) {
        // 유효성 검사를 통과한 경우에만 이 코드가 실행됩니다.
        return ResponseEntity.ok("User created successfully");
    }
}
```

```java
public class UserDto {
    @NotNull(message = "Name cannot be null")
    private String name;

    @Email(message = "Email should be valid")
    private String email;

    @Valid
    private Address address;
}

public class Address {
    @NotNull(message = "Street cannot be null")
    private String street;

    @NotNull(message = "City cannot be null")
    private String city;
}
```

```java
// BindingResult를 사용한 상세 오류 처리
@PostMapping("/user")
public ResponseEntity<String> createUser(@Valid @RequestBody UserDto userDto, BindingResult result) {
    if (result.hasErrors()) {
        String errors = result.getAllErrors()
                              .stream()
                              .map(DefaultMessageSourceResolvable::getDefaultMessage)
                              .collect(Collectors.joining(", "));
        return ResponseEntity.badRequest().body("Validation failed: " + errors);
    }
    return ResponseEntity.ok("User created successfully");
}
```

### @Valid vs @Column(nullable = false)

`@Valid`와 데이터베이스 레벨의 제약 조건(`ex. @Column(nullable = false)`)은 서로 다른 레벨에서 작동하지만, 함께 사용될 때 가장 효과적입니다.

- **@Valid:** 애플리케이션 레벨에서 데이터 유효성을 검사합니다.
- **@Column(nullable = false):** 데이터베이스 레벨에서 제약 조건을 설정합니다.

두 가지를 함께 사용함으로써 애플리케이션의 여러 계층에서 데이터 무결성을 보장할 수 있습니다2.
