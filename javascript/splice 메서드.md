# splice 메서드

`splice` 메서드는 배열의 내용을 추가하거나 제거하는 데 사용됩니다.
이 메서드는 배열의 특정 위치에서 요소를 추가하거나 제거하고 배열의 길이를 조절하는 데 유용합니다.

### 기본 문법

`splice()` 메서드의 기본 문법은 다음과 같습니다.

```js
array.splice(start, deleteCount, item1, item2, ...)
```

- `start`: 배열 변경을 시작할 인덱스
- `deleteCount`: 제거할 요소의 수 (선택적)
- `item1, item2, ...`: 배열에 추가할 새 요소들 (선택적)

### 요소 제거

`splice()`를 사용하여 배열에서 요소를 제거할 수 있습니다.

```js
let fruits = ["apple", "banana", "cherry", "date"];
let removed = fruits.splice(1, 2);

console.log(fruits);   // ["apple", "date"]
console.log(removed);  // ["banana", "cherry"]
```

- 인덱스 1부터 시작하여 2개의 요소를 제거했습니다.

### 요소 추가

`splice()`를 사용하여 배열에 새 요소를 추가할 수도 있습니다.

```js
let fruits = ["apple", "banana", "cherry"];
fruits.splice(1, 0, "kiwi", "mango");

console.log(fruits);  // ["apple", "kiwi", "mango", "banana", "cherry"]
```

- 인덱스 1의 위치에 아무 요소도 제거하지 않고 ("kiwi"와 "mango"를 추가했습니다.

### 요소 교체

`splice()`를 사용하여 기존 요소를 새 요소로 교체할 수 있습니다.

```js
let fruits = ["apple", "banana", "cherry"];
fruits.splice(1, 1, "kiwi");

console.log(fruits);  // ["apple", "kiwi", "cherry"]
```

- banana"를 "kiwi"로 교체했습니다.

#### 주의사항

- `splice()` 메서드는 원본 배열을 직접 수정합니다.
- 제거된 요소들로 이루어진 새 배열을 반환합니다.
- 요소를 추가만 하고 제거하지 않을 경우, 빈 배열을 반환합니다.

`splice()` 메서드는 배열 조작에 매우 유용하며, 요소 제거, 추가, 교체 등 다양한 작업을 수행할 수 있습니다.
