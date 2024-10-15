# Array.from 메서드란

`JavaScript`에서 `Array.from` 메서드는 `iterable`한 객체나 유사 배열 객체를 받아 새로운 배열을 생성합니다.

### 기본 기능

`Array.from()`은 다음과 같은 객체들로부터 새로운 배열을 생성합니다.

- 유사 배열 객체 (`array-like objects`)
- 반복 가능한 객체 (`iterable objects`)

이 메서드는 이러한 객체들을 얕게 복사하여 새로운 `Array` 인스턴스를 만듭니다.

#### 구문

```js
Array.from(arrayLike, mapFn, thisArg)
```

- **arrayLike:** 배열로 변환할 객체
- **mapFn (선택적):** 배열의 모든 요소에 적용할 매핑 함수
- **thisArg (선택적):** `mapFn` 실행 시 `this`로 사용할 값

### 주요 사용 사례

#### 1. 문자열을 배열로 변환

```js
Array.from("foo"); // ["f", "o", "o"]
```

#### 2. Set을 배열로 변환

```js
const set = new Set(["foo", "bar", "baz"]);
Array.from(set); // ["foo", "bar", "baz"]
```

#### 3. Map을 배열로 변환

```js
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map); // [[1, 2], [2, 4], [4, 8]]
```

#### 4. 유사 배열 객체를 배열로 변환

```js
Array.from({ length: 5 }, (v, i) => i); // [0, 1, 2, 3, 4]
```

### 매핑 함수 사용

`Array.from()`의 두 번째 인자로 매핑 함수를 제공하면, 새 배열의 각 요소에 이 함수가 적용됩니다.

```js
Array.from([1, 2, 3], x => x * 2); // [2, 4, 6]
```

#### 특징

- `Array.from()`은 희소 배열을 생성하지 않습니다. 누락된 인덱스는 `undefined`로 채워집니다.
- 이 메서드는 `Array`의 하위 클래스에서도 사용 가능하며, 이 경우 하위 클래스의 새 인스턴스를 반환합니다.
- 비동기 순회 가능 객체를 배열로 변환하려면 `Array.fromAsync()`를 사용해야 합니다.

`Array.from()`은 다양한 데이터 구조를 배열로 변환하는 데 유용하며, 특히 유사 배열 객체나 이터러블 객체를 다룰 때 강력한 도구가 됩니다.
