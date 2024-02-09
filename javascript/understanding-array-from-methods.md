# Array.from 메서드 이해하기

`JavaScript`에서 `Array.from` 메서드는 `iterable`한 객체나 유사 배열 객체를 받아 새로운 배열을 생성합니다.
> `iterable`한 객체는 배열처럼 요소를 순회할 수 있는 객체를 의미하며, 대표적으로 배열, 문자열, `Set`, `Map` 등이 해당됩니다.

&nbsp;

### 기본 구문

```js
Array.from(arrayLike[, mapFn[, thisArg]])
```

- `arrayLike`: 배열로 변환하고자 하는 `iterable`한 객체나 유사 배열 객체입니다.
- `mapFn` (선택 사항): 배열의 모든 요소에 대해 호출될 매핑 함수입니다.
- `thisArg` (선택 사항): `mapFn`에서 사용할 `this` 값입니다.

&nbsp;

### 주의할 점

- `mapFn`을 사용할 때, 배열의 각 요소에 대해 변환 작업을 수행할 수 있습니다.
- `thisArg`를 사용하여 `mapFn` 내부에서 참조할 `this` 값을 지정할 수 있습니다.
- `arrayLike`가 배열이 아닌 경우, `Array.from`은 해당 객체를 배열로 변환합니다.

&nbsp;

## 예제

```js
// 배열과 유사 배열 객체로부터 배열 생성
const arrayLike = { 0: 'a', 1: 'b', 2: 'c', length: 3 };
const newArray = Array.from(arrayLike);
console.log(newArray); // ['a', 'b', 'c']

// 문자열로부터 배열 생성
const str = 'hello';
const newArray2 = Array.from(str);
console.log(newArray2); // ['h', 'e', 'l', 'l', 'o']

// 배열의 각 요소에 함수를 적용하여 새로운 배열 생성
const nums = [1, 2, 3, 4, 5];
const squaredNums = Array.from(nums, num => num * num);
console.log(squaredNums); // [1, 4, 9, 16, 25]
```
