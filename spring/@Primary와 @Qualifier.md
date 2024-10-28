# @Primary와 @Qualifier

`@Primary`와 `@Qualifier`는 둘 다 Spring Framework에서 의존성 주입 시 빈(`Bean`)을 선택하는 데 사용되는 애노테이션입니다.

## @Primary

- 동일한 타입의 빈이 여러 개 있을 때 우선적으로 주입될 빈을 지정합니다.
- 기본값(`default`)처럼 동작하여 별도의 지정 없이 주입됩니다.

#### 빈 등록 시

```java
@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy {}
```

## @Qualifier

- 주입 대상 빈을 더 구체적으로 지정할 때 사용합니다.
- 이름을 지정하여 빈을 주입하므로, 특정 빈을 선택적으로 주입할 수 있습니다.
- `@Primary`와 달리 여러 빈에 대해 선택적으로 사용할 수 있습니다.
- 빈 등록과 주입 시점 모두에서 사용해야 합니다.

#### 등록 시

```java
@Component
@Qualifier("mainDiscountPolicy")
public class RateDiscountPolicy implements DiscountPolicy {}
```

#### 주입 시

```java
@Autowired
public OrderServiceImpl(@Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
    this.discountPolicy = discountPolicy;
}
```

### 주요 차이점

1. 사용 방식: `@Primary`는 빈 등록 시에만 사용하지만, `@Qualifier`는 등록과 주입 시 모두 사용해야 합니다.
2. 우선순위: `@Qualifier`가 `@Primary`보다 우선순위가 높습니다. 둘 다 존재할 경우 `@Qualifier`가 우선 적용됩니다.
3. 유연성: `@Primary`는 기본값을 지정하는 데 유용하고, @Qualifier는 특정 상황에서 다른 빈을 주입하고 싶을 때 유용합니다.
