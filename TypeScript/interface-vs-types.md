# interface와 type 비교

`TypeScript`에서 `interface`와 `type`은 둘 다 타입을 정의하는데 사용되는 구조입니다.

&nbsp;

## 유사점

- `interface`와 `type` 모두 새로운 타입을 정의하는 데 사용됩니다.
- 객체, 함수, 클래스 등 다양한 타입을 정의할 수 있습니다.
- `TypeScript` 버전에 따라 지원하는 기능이 약간 다를 수 있지만, 대부분의 경우 유사하게 사용할 수 있습니다.

@nbsp;

## 차이점

#### 확장 가능성

`interface`는 선언을 병합할 수 있습니다. 여러 곳에서 동일한 `interface`를 선언하면 그 인터페이스는 병합됩니다.

```ts
interface Car {
  brand: string;
}

interface Car {
  model: string;
}

const myCar: Car = {
  brand: "Audi",
  model: "A8",
};
```

&nbsp;

`type`는 병합할 수 없습니다. 여러 곳에서 동일한 이름의 타입을 선언하면 오류가 발생합니다.

```ts
type Car = {
  brand: string;
};

// Error: Duplicate identifier 'Car'.
type Car = {
  model: string;
};
```

&nbsp;

## 상속

`interface`는 `extends` 키워드를 사용하여 다른 인터페이스를 상속할 수 있습니다.

```ts
interface Shape {
  color: string;
}

interface Square extends Shape {
  sideLength: number;
}
```

&nbsp;

`type`은 `&` 연산자를 사용하여 다른 타입을 조합할 수 있습니다.

```ts
type Shape = {
  color: string;
};

type Square = Shape & {
  sideLength: number;
};
```

&nbsp;

## 추상화 수준

`interface`는 주로 객체나 클래스의 구조를 정의하는 데 사용됩니다.

```ts
interface Point {
  x: number;
  y: number;
}
```

&nbsp;

`type`은 좀 더 일반적인 타입을 정의하며, 객체 뿐만 아니라 유니온, 인터섹션, 타입 별칭 등 다양한 타입을 정의하는 데 사용됩니다.

```ts
type Point = {
  x: number;
  y: number;
};

type Coordinates = [number, number];

type Person = { name: string; age: number };
```

&nbsp;

> 대부분의 경우, `interface`와 `type`은 상호 교환 가능하게 사용될 수 있습니다. 객체나 클래스의 구조를 정의해야 할 때는 `interface`를 사용하는 것이 일반적입니다.
좀 더 일반적인 타입을 정의하거나 유니온, 인터섹션, 타입 별칭 등을 사용해야 할 때는 `type`을 사용합니다.
