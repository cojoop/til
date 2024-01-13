# JavaScript에서 비동기 코드 다루기 (feat. async/await, Promise)

**JavaScript**는 싱글 스레드 언어로, 비동기 코드 처리가 필수적입니다. `async/await`와 `Promise`는 비동기 코드를 다루는 데 사용되는 기술로 코드를 더 읽기 쉽게 만들고 비동기 작업을 쉽게 다룰 수 있게 도와줍니다.
> 비동기 처리시의 유의할 점은 **응답 결과에 대한 처리**입니다.

<br/>

## Promise

`Promise`는 비동기 작업의 완료 또는 실패를 나타내는 객체로, 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용합니다. `Promise`는 세 가지 상태를 가집니다.

1. **Pending (대기 중):** 비동기 작업이 아직 완료되지 않은 상태입니다.
2. **Fulfilled (이행됨):** 비동기 작업이 성공적으로 완료된 상태입니다.
3. **Rejected (거부됨):** 비동기 작업이 실패한 상태입니다.
<br/>

```js
// Promise를 반환하는 비동기 작업을 수행하는 함수
function fetchData() {
  return new Promise((resolve, reject) => {
    // 비동기 작업 시뮬레이션
    setTimeout(() => {
      const isSuccess = true;
      if (isSuccess) {
        resolve("데이터 가져오기 성공!");
      } else {
        reject("데이터 가져오기 실패!");
      }
    }, 2000); // 2초 후에 작업 완료
  });
}
```

<br/>

## async/await

`async`는 함수가 항상 `Promise`를 반환하게 만듭니다. `await`는 `Promise`가 이행될 때까지 기다리고, 결과를 반환합니다. 이를 통해 비동기 코드를 동기적으로 작성할 수 있습니다.

```js
// async/await를 사용하여 비동기 작업 처리하는 함수
async function fetchDataAsync() {
  try {
    console.log("데이터 가져오기 시작...");

    // fetchData 함수에서 반환된 Promise가 이행될 때까지 대기
    const result = await fetchData();
    
    console.log("데이터 가져오기 완료:", result);
  } catch (error) {
    console.error("데이터 가져오기 실패:", error);
  }
}
```

`async/await`는 가독성이 좋고 코드를 작성하기 쉽게 만듭니다. 이는 콜백이나 `Promise` 체인을 사용하는 것보다 코드를 읽고 이해하기 쉽게 만들어주며, 에러 처리도 간편하게 할 수 있습니다.

>`await`는 `async` 함수 내에서만 사용할 수 있습니다. 따라서 `await`를 사용하려면 해당 함수가 `async` 키워드로 정의되어 있어야 합니다.
