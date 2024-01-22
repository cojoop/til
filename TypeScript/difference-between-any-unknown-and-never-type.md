# any, unknown, never 타입의 차이점

`TypeScript`에는 다양한 타입들이 존재하는데, `any`, `unknown`, 그리고 `never`는 동적 타입을 다룰 때 주목해야 할 중요한 세 가지 타입입니다.

&nbsp;

## any: 모든 것이 가능한 자유로운 타입

`any`는 `TypeScript`에서 모든 타입의 값을 허용하는 동적 타입입니다. 어떤 타입의 값이든 할당할 수 있기 때문에 자유로운 사용이 가능하지만, 그만큼 타입 안정성이 떨어집니다.

```ts
let dynamicValue: any = 10;
dynamicValue = 'Hello';
dynamicValue = [1, 2, 3];
// 모든 타입이 허용되어 컴파일러가 타입 검사를 수행하지 않음
```

> `any`를 남발하면 타입 시스템의 이점을 잃게 되므로, 코드 내에서 최대한 사용을 피하는 것이 좋습니다.

&nbsp;

## unknown: 타입 불확실성을 안전하게 다루기

`unknown`은 `any`와 달리 타입 안정성을 제공합니다. 어떤 타입인지 확실하지 않은 값을 나타내며, 사용 전에 명시적인 타입 체크나 형변환이 필요합니다.

```ts
let uncertainValue: unknown = 10;

// 컴파일 오류: number 타입이라고 명시하지 않으면 사용할 수 없음
// const result = uncertainValue + 5;

if (typeof uncertainValue === 'number') {
  const result = uncertainValue + 5; // 안전하게 사용 가능
}
```

> `unknown`은 타입 불확실성을 안전하게 처리하면서, 타입 안정성을 유지할 수 있도록 도와줍니다.

&nbsp;

## never: 코드 흐름의 종료를 표현하는 타입

`never`는 함수의 반환 타입으로 주로 사용되며, 함수가 어떤 값도 반환하지 않음을 나타냅니다. 이는 주로 예외를 던지거나 무한 루프에 빠지는 등의 상황에서 쓰입니다.

```ts
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    // 무한 루프
  }
}
```

> `never`는 코드 흐름이 종료되지 않는 상황에서 사용되며, 예상치 못한 에러 처리나 특정 조건에서의 무한 루프 등에 활용됩니다.
