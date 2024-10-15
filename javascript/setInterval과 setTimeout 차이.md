# setInterval과 setTimeout 차이

`setInterval`과 `setTimeout`은 JavaScript에서 코드의 실행을 예약하는 타이머 함수입니다.
이 두 함수는 비동기적으로 코드를 실행하거나 일정 시간 간격으로 코드를 반복 실행하는 데 사용됩니다.

## 주요 차이점

### 실행 횟수

#### setTimeout

- 지정된 시간 후 콜백 함수를 한 번만 실행합니다12.
- ex. `setTimeout(() => console.log("Hello"), 1000);`는 1초 후 "Hello"를 한 번 출력합니다.

#### setInterval

- 지정된 시간 간격으로 콜백 함수를 반복적으로 실행합니다12.
- ex. `setInterval(() => console.log("Hello"), 1000);`는 1초마다 "Hello"를 계속 출력합니다.

### 실행 방식

#### setTimeout

- 함수 실행이 완료된 후 다음 실행을 예약합니다.
- 이는 각 실행 사이의 간격을 정확히 보장합니다.

#### setInterval

- 함수 실행 시간과 관계없이 일정 간격으로 실행을 시도합니다.
- 함수 실행 시간이 간격보다 길 경우, 실행이 겹칠 수 있습니다.

### 유연성

#### setTimeout

- 재귀적으로 사용하여 setInterval과 유사한 기능을 구현할 수 있습니다.
- 동적으로 간격을 조절하기 쉽습니다.

#### setInterval

- 고정된 간격으로 실행하기 쉽지만, 동적 조절이 상대적으로 어렵습니다.

### 메모리 관리

두 함수 모두 타이머 ID를 반환하며, 이를 사용하여 예약된 실행을 취소할 수 있습니다.

- **setTimeout:** `clearTimeout(timerId)`
- **setInterval:** `clearInterval(timerId)`

불필요한 메모리 사용을 방지하기 위해 더 이상 필요하지 않은 타이머는 취소하는 것이 좋습니다.

### 사용 시나리오

- **setTimeout:** 지연된 일회성 작업에 적합합니다.
- **setInterval:** 주기적인 업데이트나 폴링에 유용합니다.

두 함수의 특성을 이해하고 상황에 맞게 적절히 선택하여 사용하는 것이 중요합니다.
