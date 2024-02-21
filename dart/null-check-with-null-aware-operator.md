# Null Aware Operator로 null 체크하기

`Null Aware Operator`인 `?.`는 코드에서 `null` 값인 객체에 접근할 때 매우 유용합니다. 객체가 `null`이 아닌 경우에만 해당 객체의 속성이나 메서드에 접근하고자 할 때 사용됩니다.

> 일반적으로 객체에 접근할 때 사용하는 점 연산자(`.`)와 비슷하지만, 객체가 `null`인 경우 점 연산자를 사용할 때 발생하는 예외를 방지할 수 있습니다.

#### 사용 예시

```dart
class Person {
  String? name;

  Person(this.name);
}

void main() {
  Person? person = Person('John');

  // 일반적인 점 연산자 사용
  if (person != null) {
    print(person.name); // 출력: John
  }

  // Null Aware Operator 사용
  print(person?.name); // 출력: John

  person = null;

  // 일반적인 점 연산자 사용
  if (person != null) {
    // 오류 발생: Null check operator used on a null value
    print(person.name); 
  }

  // Null Aware Operator 사용
  print(person?.name); // 출력: null
}
```

&nbsp;

## Null Aware Operator의 Chaining

`Null Aware Operator`는 체이닝(`Chaining`)도 지원합니다. 이는 여러 객체의 연속된 접근에서 `null`을 안전하게 처리할 수 있도록 해줍니다.

```dart
class Address {
  String? city;

  Address(this.city);
}

class Person {
  Address? address;

  Person(this.address);
}

void main() {
  Person? person = Person(Address('New York'));

  // 체이닝을 사용하지 않은 경우
  if (person != null && person.address != null) {
    print(person.address!.city); // 출력: New York
  }

  // Null Aware Operator의 체이닝 사용
  print(person?.address?.city); // 출력: New York

  person = null;

  // Null Aware Operator의 체이닝 사용
  print(person?.address?.city); // 출력: null
}
```
