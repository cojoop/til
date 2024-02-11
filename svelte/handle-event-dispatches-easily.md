# 이벤트 디스패치를 간편하게 처리하기

`createEventDispatcher` 함수는 `Svelte`에서 이벤트 디스패치를 간편하게 처리하기 위한 함수입니다. 이 함수를 사용하면 컴포넌트 간 통신이나 부모 컴포넌트로부터 자식 컴포넌트로 이벤트를 전달할 수 있습니다.

## 사용 방법

```js
import { createEventDispatcher } from 'svelte';

const dispatch = createEventDispatcher();
```

- `createEventDispatcher` 함수를 가져와서 `dispatch`라는 이름으로 사용할 준비를 합니다.

&nbsp;

```js
dispatch('이벤트_이름', 데이터);
```

- `'이벤트_이름'`은 디스패치할 이벤트의 이름을 나타내며, 데이터는 이벤트와 함께 전달할 선택적인 데이터입니다.

&nbsp;

## 예제

```html
<!-- ParentComponent.svelte -->
<script>
    import ChildComponent from './ChildComponent.svelte';
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    function handleClick() {
        dispatch('buttonClick', { message: '버튼이 클릭되었습니다!' });
    }
</script>

<button on:click={handleClick}>버튼을 클릭하세요</button>
<ChildComponent />
```

- `ParentComponent.svelte`에서는 `createEventDispatcher`를 사용하여 이벤트를 생성하고, 버튼이 클릭되었을 때 해당 이벤트를 디스패치합니다.
- `handleClick` 함수는 버튼이 클릭될 때 호출되며, `dispatch` 함수를 사용하여 'buttonClick' 이벤트를 발송합니다. 이때 `{ message: '버튼이 클릭되었습니다!' }`와 같이 데이터를 함께 전달합니다.

&nbsp;

```html
<!-- ChildComponent.svelte -->
<script>
    import { onMount } from 'svelte';

    function handleButtonClick(event) {
        console.log('부모 컴포넌트에서 보낸 메시지:', event.detail.message);
    }
    
    onMount(() => {
        window.addEventListener('buttonClick', handleButtonClick);
        
        return () => {
            window.removeEventListener('buttonClick', handleButtonClick);
        };
    });
</script>

<div>자식 컴포넌트입니다</div>
```

- `createEventDispatcher` 함수를 호출하여 `dispatch` 함수를 만듭니다. 이 함수는 이벤트를 발송할 때 사용됩니다.
- `ChildComponent.svelte`에서는 `onMount` 라이프사이클 훅을 사용하여 컴포넌트가 마운트될 때 이벤트를 수신하도록 설정합니다.
- `handleButtonClick` 함수는 `window.addEventListener`를 사용하여 'buttonClick' 이벤트를 수신하고, 이벤트가 발생하면 콘솔에 메시지를 출력합니다.

&nbsp;

> 이 예제는 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 방법을 보여줍니다. 부모 컴포넌트에서 이벤트를 발송하고, 자식 컴포넌트에서 해당 이벤트를 수신하여 처리할 수 있습니다
