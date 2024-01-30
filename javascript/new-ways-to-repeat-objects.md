# 객체를 반복하는 새로운 방법

`entries()`는 **ES8(ECMAScript 2017)**에서 소개된 객체를 반복할 때 매우 유용한 메서드입니다. 이 메서드는 객체의 `키-값` 쌍을 포함하는 배열을 반환하여 객체를 반복하는 데 도움이 됩니다.

## entries 메서드란

`entries()` 메서드는 객체의 속성을 `[키, 값]` 쌍의 배열로 반환합니다. 이 메서드는 객체를 반복할 때 특히 유용하며, `이터레이터(iterator)`를 반환하여 객체의 각 속성을 순회할 수 있습니다. 이를 통해 객체의 내용을 보다 쉽게 처리할 수 있습니다.

```js
const obj = { a: 1, b: 2, c: 3 };

const entries = Object.entries(obj);

console.log(entries);
// 출력: [ ["a", 1], ["b", 2], ["c", 3] ]
```

- `obj`라는 객체를 생성하고, `Object.entries()` 메서드를 사용하여 이 객체의 속성을 배열로 변환했습니다.
- 그 결과, 배열 entries에는 `obj` 객체의 `키-값` 쌍이 포함되어 있습니다.

## entries 메서드의 활용

`entries()` 메서드는 객체를 반복하고 특정 작업을 수행할 때 매우 유용합니다. 예를 들어, 객체의 속성을 로그로 출력하거나 반복적인 작업을 수행할 때 사용할 수 있습니다. 또한 `for...of` 루프와 함께 사용하여 객체를 순회할 수도 있습니다.

```js
const obj = { a: 1, b: 2, c: 3 };

for (const [key, value] of Object.entries(obj)) {
  console.log(`Key: ${key}, Value: ${value}`);
}
// 출력:
// Key: a, Value: 1
// Key: b, Value: 2
// Key: c, Value: 3
```

- `for...of` 루프를 사용하여 `entries()` 메서드가 반환한 배열을 순회하고, 각 키-값 쌍을 출력하고 있습니다.

&nbsp;

```js
const obj = { a: 1, b: 2, c: 3 };
const transformedEntries = Object.entries(obj).map(([key, value]) => [key.toUpperCase(), value * 2]);

console.log(transformedEntries);
// 출력: [ ["A", 2], ["B", 4], ["C", 6] ]
```

- `map()`을 사용하여 객체의 각 속성을 변형하고 있습니다.
