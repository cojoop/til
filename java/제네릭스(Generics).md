# 제네릭스(Generics)란

제네릭스(`Generics`)는 코드의 유연성과 안정성을 향상시켜 주는 자바의 중요한 기능입니다.

### 정의와 목적

제네릭스는 다양한 타입의 객체를 다루는 메서드나 컬렉션 클래스에 컴파일 시점의 타입 체크를 제공하는 기능입니다.

#### 주요 목적

- 타입 안정성 향상
- 불필요한 형변환 제거

### 사용 방법

제네릭스는 클래스와 메서드에 선언할 수 있습니다.

#### 제네릭 클래스 선언

```java
class Box<T> {
  T item;
  void setItem(T item) { this.item = item; }
  T getItem() { return item; }
}
```

- T는 타입 변수(`type variable`)로, 실제 사용 시 구체적인 타입으로 대체됩니다.

#### 제네릭 클래스 사용

```java
Box<String> stringBox = new Box<>();
stringBox.setItem("ABC");
String item = stringBox.getItem(); // 형변환 불필요
```

#### 주요 특징

**1. 타입 안정성:** 컴파일 시점에 타입 체크를 수행하여 런타임 에러를 방지합니다.
**2. 코드 재사용:** 다양한 타입에 대해 동일한 코드를 사용할 수 있습니다.
**3. 제한된 타입 매개변수:** extends 키워드를 사용하여 타입을 제한할 수 있습니다.

```java
class FruitBox<T extends Fruit> { ... }
```

**4. static 멤버 제한:** 제네릭 클래스의 `static` 멤버에는 타입 매개변수를 사용할 수 없습니다.
**5. 타입 소거:** 컴파일 후에는 제네릭 타입 정보가 제거되어 원시 타입(`raw type`)으로 변환됩니다.
