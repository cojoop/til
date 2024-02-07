# 객체의 키-값 쌍 순회하기

`JavaScript`에서 객체(`object`)를 다룰 때, 객체의 키(`key`)와 값(`value`) 쌍을 순회하고자 할 때 `entries()` 메소드가 유용하게 사용됩니다. 이 메소드는 객체를 반복 가능한 `키-값` 쌍의 배열로 반환하여, 객체의 속성을 쉽게 접근하고 처리할 수 있도록 도와줍니다.

## entries( ) 메소드의 구문

```js
// obj는 순회하고자 하는 객체
Object.entries(obj)
```

&nbsp;

## entries( ) 메소드의 동작

```js
const obj = { 'name': 'John', 'age': 30, 'city': 'New York' };
const entriesArray = Object.entries(obj);

console.log(entriesArray);
// 출력: [ ['name', 'John'], ['age', 30], ['city', 'New York'] ]
```

- `entries()` 메소드를 사용하면 객체의 속성을 쉽게 순회하고 조작할 수 있습니다.

&nbsp;

```js
const obj = { 'name': 'John', 'age': 30, 'city': 'New York' };

for (const [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}
// 출력:
// name: John
// age: 30
// city: New York
```

- `for...of` 루프를 사용하여 모든 키-값 쌍에 접근할 수 있습니다.
