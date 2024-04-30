# Enum 알아보기

`Enum(열거형)`은 상수의 집합을 나타내는 자료형입니다. 각각의 `Enum` 상수는 고유한 이름을 가지며, 해당 상수가 표현하는 값은 변경할 수 없습니다.
> 이는 상수를 정의하고 그룹화함으로써 프로그램의 가독성을 향상시키고 실수를 줄일 수 있도록 도와줍니다.

## Enum의 정의

`Enum`은 `enum` 키워드를 사용하여 정의됩니다.

```java
// 요일을 나타내는 Enum
public enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}
```

- `Day`는 `Enum`의 이름이며, `SUNDAY, MONDAY, ..., SATURDAY`는 `Enum` 상수입니다.
- `Enum` 상수는 모두 대문자로 작성되며, 각 상수는 해당 상수의 이름으로만 참조될 수 있습니다.

## Enum의 활용

`Enum`을 사용하면 코드의 가독성을 향상시킬 수 있습니다. `Switch` 문에서 `Enum`을 사용하는 것은 특히 유용합니다.

```java
public class EnumExample {
    public enum Day {
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
    }
    
    public static void main(String[] args) {
        Day today = Day.MONDAY;
        
        switch (today) {
            case MONDAY:
                System.out.println("Today is Monday");
                break;
            case TUESDAY:
                System.out.println("Today is Tuesday");
                break;
            // 나머지 요일에 대한 처리...
            default:
                System.out.println("Today is not Monday or Tuesday");
        }
    }
}
```

- `Day` Enum을 사용하여 현재 요일을 표현하고, `Switch` 문을 사용하여 각 요일에 대한 처리를 수행합니다.

## Enum의 추가 기능

`Enum`은 단순히 상수의 집합 이상의 기능을 제공합니다. 각 `Enum` 상수는 메서드와 속성을 가질 수 있습니다.

```java
public enum Day {
    SUNDAY("Sun"), MONDAY("Mon"), TUESDAY("Tue"), WEDNESDAY("Wed"), 
    THURSDAY("Thu"), FRIDAY("Fri"), SATURDAY("Sat");
    
    private String abbreviation;
    
    private Day(String abbreviation) {
        this.abbreviation = abbreviation;
    }
    
    public String getAbbreviation() {
        return abbreviation;
    }
}
```

- `Day` Enum의 각 상수에 대해 약어를 저장하는 속성과 이를 반환하는 메서드를 추가했습니다.

## Enum 사용 이유

1. **가독성:** `Enum`을 사용하면 프로그램의 가독성이 향상됩니다.
2. **타입 안정성:** `Enum`은 컴파일 타임에 타입 검사를 제공하여 잘못된 값이나 타입을 사용하는 오류를 사전에 방지합니다. 이는 프로그램의 안정성을 높이고 버그를 줄여줍니다.
3. **명시성:** `Enum`을 사용하면 특정 상수의 의미를 명확하게 나타낼 수 있습니다.

#### 언제 Enum을 사용해야 하나요?

`Enum`은 주로 다음과 같은 상황에서 사용됩니다

- 상태(`state`)를 표현할 때 (ex: 요일, 주문 상태 등)
- 고정된 값의 집합을 나타낼 때 (ex: 컬러, 카테고리 등)
- 서로 연관된 상수를 그룹화할 때
