# Enum 알아보기

`Enum(열거형)`은 서로 연관된 상수들의 집합을 나타냅니다. 각각의 `Enum` 상수는 고유한 이름을 가지며, 해당 상수가 표현하는 값은 변경할 수 없습니다. 이는 상수를 정의하고 그룹화함으로써 프로그램의 가독성을 향상시키고 실수를 줄일 수 있도록 도와줍니다.

```java
// 예제 코드
public enum Direction {
    NORTH("북쪽", 0),
    EAST("동쪽", 90),
    SOUTH("남쪽", 180),
    WEST("서쪽", 270);

    private final String name;
    private final int angle;

    Direction(String name, int angle) {
        this.name = name;
        this.angle = angle;
    }

    public String getName() {
        return name;
    }

    public int getAngle() {
        return angle;
    }
}

public class Main {
    public static void main(String[] args) {
        Direction myDirection = Direction.EAST;

        System.out.println("현재 방향은 " + myDirection.getName() + "입니다.");
        System.out.println("각도는 " + myDirection.getAngle() + "도 입니다.");
    }
}
```

- 방향을 나타내는 `Enum`인 `Direction`을 정의합니다.
- 각각의 방향은 이름과 해당 방향을 표현하는 각도를 가지고 있습니다.
- `Enum`의 생성자를 이용하여 각 상수의 속성을 초기화하고, 각 상수마다 이름과 각도를 반환하는 메서드를 추가했습니다.

## Enum 사용 이유

1. **가독성:** `Enum`을 사용하면 프로그램의 가독성이 향상됩니다.
2. **타입 안정성:** `Enum`은 컴파일 타임에 타입 검사를 제공하여 잘못된 값이나 타입을 사용하는 오류를 사전에 방지합니다. 이는 프로그램의 안정성을 높이고 버그를 줄여줍니다.
3. **명시성:** `Enum`을 사용하면 특정 상수의 의미를 명확하게 나타낼 수 있습니다.

#### 언제 Enum을 사용해야 하나요?

`Enum`은 주로 다음과 같은 상황에서 사용됩니다

- 상태(`state`)를 표현할 때 (ex: 요일, 주문 상태 등)
- 고정된 값의 집합을 나타낼 때 (ex: 컬러, 카테고리 등)
- 서로 연관된 상수를 그룹화할 때
