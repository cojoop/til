# equals( ) 메서드 오버라이딩

`Java`에서 객체의 동등성 비교를 위해 `equals()`메서드를 오버라이딩하는 것은 매우 중요합니다. 이는 주로 컬렉션 프레임워크의 `Set`과 같은 자료구조에서 객체를 추가하거나 조회할 때 관여합니다.

특히, `Set`은 중복된 요소를 허용하지 않으므로 `equals()`메서드를 올바르게 구현하지 않으면 예상치 못한 동작을 유발할 수 있습니다.

## equals( ) 메서드 오버라이딩

```java
// Building 클래스의 equals() 메서드를 구현한 예시입니다. 
@Override
public boolean equals(Object obj) {
    if (!(obj instanceof Building))
        return false;

    Building building = (Building) obj;
    return Objects.equals(name, building.name) && Objects.equals(addr, building.addr); 
}
```

- 두 `Building` 객체의 이름과 주소가 동일한지를 비교하여 동등성을 판단합니다.

## 필드값이 null인 경우

위 코드에는 필드값이 `null`인 경우의 처리가 빠져있습니다. 객체를 생성할 때 필드값이 n`ull`인 경우, `equals()` 메서드에서 `NullPointerException`이 발생할 수 있습니다.

처리하는 방법 중 하나는 객체를 생성할 때 필드값이 `null`인지를 검사하고, `null`인 경우 객체를 생성하지 않도록 처리하는 것입니다. 이를 위해 생성자를 수정하거나, 객체 생성을 담당하는 팩토리 메서드를 사용할 수 있습니다.

```java
public Building(String name, String addr) {
    if (name == null || addr == null) {
        throw new IllegalArgumentException("Name and address cannot be null");
    }
    this.name = name;
    this.addr = addr;
}
```

- 생성자를 수정하여 필드값이 `null`인 경우 객체를 생성하지 못하도록 처리할 수 있습니다.
- 이렇게 함으로써 `equals()` 메서드에서 `NullPointerException`이 발생하는 상황을 방지할 수 있습니다.
