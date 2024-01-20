# setInterval과 setTimeout 차이

`setInterval`과 `setTimeout`은 `JavaScript`에서 사용되는 두 가지 타이머 함수입니다. 이 두 함수는 비동기적으로 코드를 실행하거나 일정 시간 간격으로 코드를 반복 실행하는 데 사용됩니다.

&nbsp;

## setTimeout

`setTimeout` 함수는 일정 시간이 지난 후에 특정한 코드를 실행하도록 예약합니다.

```js
setTimeout(function() {
  console.log("이 코드는 1초 후에 실행됩니다.");
}, 1000);
```

- `setTimeout`을 사용하여 1초 후에 특정 함수를 실행하도록 예약할 수 있습니다.

&nbsp;

## setInterval

`setInterval` 함수는 일정한 간격으로 특정한 코드를 반복 실행하도록 예약합니다.

```js
setInterval(function() {
  console.log("이 코드는 1초마다 실행됩니다.");
}, 1000);
```

- `setInterval`을 사용하여 1초마다 특정 함수를 실행하도록 예약할 수 있습니다.

> `setInterval`은 계속해서 실행되며, 명시적으로 해제되지 않는 이상 계속 반복됩니다. 해제하려면 `clearInterval` 함수를 사용해야 합니다.

&nbsp;

### 차이점

- `setTimeout`은 한 번만 실행되고 종료됩니다.
- `setInterval`은 지정된 간격으로 계속해서 반복 실행됩니다.
