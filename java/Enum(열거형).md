# Enum(열거형)

`Enum(열거형)`은 상수의 집합을 나타내는 자료형입니다.
각각의 `Enum` 상수는 고유한 이름을 가지며, 해당 상수가 표현하는 값은 변경할 수 없습니다.

### Enum 기본 사용법

#### 선언

Enum은 다음과 같이 선언합니다.

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```

#### 사용

선언된 Enum은 다음과 같이 사용할 수 있습니다.

```java
Day today = Day.MONDAY;
System.out.println(today); // 출력: MONDAY
```

### Enum의 주요 메소드

#### values( )

Enum의 모든 상수를 배열로 반환합니다.

```java
Day[] days = Day.values();
for (Day day : days) {
    System.out.println(day);
}
```

#### valueOf(String name)

문자열과 일치하는 Enum 상수를 반환합니다.

```java
Day day = Day.valueOf("MONDAY");
```

#### ordinal()

Enum 상수의 순서(0부터 시작)를 반환합니다.

```java
int order = Day.WEDNESDAY.ordinal(); // 2
```

#### Enum의 확장 사용

Enum은 단순한 상수 집합 이상의 기능을 제공할 수 있습니다.

```java
public enum Day {
    MONDAY("월"),
    TUESDAY("화"),
    WEDNESDAY("수"),
    THURSDAY("목"),
    FRIDAY("금"),
    SATURDAY("토"),
    SUNDAY("일");

    private final String koreanName;

    Day(String koreanName) {
        this.koreanName = koreanName;
    }

    public String getKoreanName() {
        return koreanName;
    }
}
```

이렇게 정의된 Enum은 다음과 같이 사용할 수 있습니다.

```java
System.out.println(Day.MONDAY.getKoreanName()); // 출력: 월
```

### Enum의 장점

1. 코드의 가독성이 향상됩니다.
2. 타입 안전성을 보장합니다.
3. 컴파일 시점에 모든 상수를 알 수 있어 런타임 오류를 방지합니다.
4. `switch` 문에서 효과적으로 사용할 수 있습니다.
