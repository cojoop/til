# equals( ) 메서드 오버라이딩

`Java`에서 객체의 동등성 비교를 위해 `equals()`메서드를 오버라이딩하는 것은 매우 중요합니다.

### equals( ) 메서드 오버라이딩 시 주의사항

#### 동등성 정의

```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Product product = (Product) o;
    return Objects.equals(id, product.id);
}
```

- 객체의 동등성을 어떻게 정의할지 명확히 해야 합니다.
- 보통 객체의 주요 필드 값들을 비교하여 동등성을 판단합니다1.

#### hashCode( ) 메서드 오버라이딩

```java
@Override
public int hashCode() {
    return Objects.hash(id);
}
```

- `equals()`를 오버라이딩할 때는 반드시 `hashCode()` 메서드도 함께 오버라이딩해야 합니다.
- 그렇지 않으면 `HashSet`, `HashMap` 등의 해시 기반 컬렉션에서 객체가 제대로 동작하지 않을 수 있습니다.

#### 일관성 유지

- `equals()` 메서드는 일관성을 유지해야 합니다.
- 즉, 객체의 상태가 변경되지 않는 한 항상 같은 결과를 반환해야 합니다2.

#### null 처리

- `equals()` 메서드는 `null`을 처리할 수 있어야 합니다.
- `null`과의 비교는 항상 `false`를 반환해야 합니다2.

#### 대칭성 유지

- `a.equals(b)`가 `true`라면 `b.equals(a)`도 `true`여야 합니다3.

#### 성능 고려사항

```java
@Override
public boolean equals(Object obj) {
    if (this.hashCode() != obj.hashCode()) {
        return false;
    }
    // 추가적인 비교 로직
}
```

- `hashCode()` 메서드를 잘 구현하면 `equals()` 메서드의 성능을 향상시킬 수 있습니다.
- 두 객체의 해시코드가 다르면 `equals()` 메서드를 호출하지 않고 바로 `false`를 반환할 수 있기 때문입니다2.
