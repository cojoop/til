# 스토어(Store)를 구독하는 방법

`SvelteKit`에서는 상태 관리를 위해`Store`를 사용할 수 있습니다. `Store`는 `Svelte` 애플리케이션의 상태를 저장하고 관리하는 객체입니다.

> 이러한 `Store`는 `Svelte`의 반응성(`reactivity`) 기능을 이용하여 상태 변경을 감지하고 관련된 컴포넌트에 변경 사항을 전달합니다.

&nbsp;

## Store 생성하기

`Store`를 생성하려면 `writable()`, `readable()`, `derived()` 등의 함수를 사용합니다. 이러한 함수를 사용하여 쓰기 가능한(`writable`), 읽기 전용(`readable`), 또는 파생된(`derived`) `Store`를 생성할 수 있습니다.

```js
import { writable } from 'svelte/store';

// 쓰기 가능한 Store 생성
export const count = writable(0);
```

&nbsp;

## Store 구독하기

`Store`를 수동으로 구독하려면 `subscribe()` 메소드를 사용합니다. 이 메소드는 `Store`의 값을 변경할 때마다 호출되는 콜백 함수를 등록합니다.

```js
import { writable } from 'svelte/store';

const count = writable(0);

const unsubscribe = count.subscribe(value => {
    console.log('현재 값:', value);
});

// 스토어 값 변경
count.set(1);
count.set(2);

// 수동으로 구독 해제
unsubscribe();
</script>

```

&nbsp;

## $: 구문을 사용하기

 `$:` 구문을 사용하여 `Store`를 자동으로 구독하고 업데이트할 수 있습니다. 이 구문을 사용하면 `Store`의 값이 변경될 때마다 해당 코드 블록이 실행됩니다.

```js
import { writable } from 'svelte/store';

const count = writable(0);

$: console.log('현재 값:', $count);

// 스토어 값 변경
count.set(1);
count.set(2);
```

> 자동 구독의 경우 간단하게 표현할 수 있어 코드가 더 간결해지지만, 수동 구독의 경우 명시적으로 구독을 관리할 수 있어 더 세밀한 제어가 가능합니다.
