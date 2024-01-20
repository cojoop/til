# 화살표 함수와 일반 함수 차이

자바스크립트(ES6)에서 함수를 정의하는 방법은 화살표 함수와 일반 함수로 구분됩니다. 화살표 함수와 일반 함수의 주요 차이점은 함수 표현식의 문법과 `this` 키워드의 동작입니다.

## 문법(Syntax)

#### 화살표 함수

```js
const arrowFunction = (param1, param2) => {
    // 함수 본문
};
```

- 화살표 함수는 인자가 하나뿐이거나, 인자가 없을 경우에는 괄호를 생략할 수 있습니다.

&nbsp;

#### 일반 함수

```js
function regularFunction(param1, param2) {
    // 함수 본문
}
```

- 일반 함수의 선언은 `function` 키워드를 사용하며, 함수의 이름이 필요합니다.

<br>

## this 키워드

#### 화살표 함수

```js
function Example() {
    this.value = 42;

    // 화살표 함수
    this.method = () => {
        console.log(this.value);
    };
}

const obj = new Example();
obj.method(); // 출력: 42
```

- 화살표 함수는 자신의 `this` 바인딩을 생성하지 않습니다.
- 화살표 함수는 선언된 시점에서 외부 스코프의 this 값을 가져옵니다.
- 화살표 함수 내부에서 `this`를 사용하면, 그 함수가 정의된 곳의 `this`를 가리킵니다.

&nbsp;

#### 일반 함수

```js
function Example() {
    this.value = 42;

    // 일반 함수
    this.method = function() {
        console.log(this.value);
    };
}

const obj = new Example();
obj.method(); // 출력: 42
```

- 일반 함수는 자신만의 `this` 바인딩을 생성합니다.
- 함수가 호출되는 방식에 따라 `this`가 동적으로 바뀔 수 있습니다.

<br>

> 일반적으로, 화살표 함수는 간결하고 명료한 코드를 작성하는 데 도움이 됩니다. 하지만 `this`의 동작이나 프로토타입 체인과 관련된 경우에는 주의가 필요합니다. 이러한 차이를 이해하고 상황에 맞게 선택하는 것이 중요합니다.
