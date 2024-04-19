# 제네릭스 알아보기

제네릭스(`Generics`)는 자바 프로그래밍 언어의 중요한 기능 중 하나입니다. 이 기능은 코드의 유연성과 안정성을 향상시켜줍니다.

## 제네릭스란

제네릭스는 컬렉션 프레임워크나 메서드에서 사용되는 클래스와 인터페이스의 타입을 매개변수화할 수 있게 해주는 기능입니다. 이를 통해 클래스나 인터페이스를 작성할 때, 특정한 타입을 지정하지 않고도 다양한 타입에 대해 작동할 수 있습니다.

## 제네릭스 사용 이유

1. **타입 안정성(`Type Safety`):** 제네릭스를 사용하면 컴파일 시점에 타입 불일치로 인한 오류를 사전에 방지할 수 있습니다. 이는 런타임 시 타입 캐스팅 오류를 방지하여 프로그램의 안정성을 높여줍니다.
2. **재사용성(`Reusability`):** 제네릭스를 활용하면 단일한 코드를 여러 타입에 대해 재사용할 수 있습니다.
3. **표현력(`Expressiveness`):** 제네릭스를 사용하면 코드의 가독성을 향상시킬 수 있습니다. 타입 매개변수를 사용하여 메서드나 클래스가 어떤 종류의 객체를 다루는지 명시적으로 나타낼 수 있습니다.

## 예제 코드

```java
public static void main(String[] args) {
    // 제네릭스를 사용하지 않은 경우
    List names = new ArrayList();
    names.add("John");
    names.add("Alice");
    names.add(123); // 컴파일은 되지만 런타임에 ClassCastException 발생 가능

    String firstName = (String) names.get(0); // 타입 캐스팅 필요

    // 제네릭스를 사용한 경우
    List<String> genericNames = new ArrayList<>();
    genericNames.add("John");
    genericNames.add("Alice");
    // genericNames.add(123); // 컴파일 에러 발생

    String firstGenericName = genericNames.get(0); // 타입 캐스팅 불필요
}
```

> 제네릭스를 사용하면 컴파일 시점에 타입 불일치 오류를 확인할 수 있으며, 코드의 가독성이 향상되고 안정성이 높아집니다.
