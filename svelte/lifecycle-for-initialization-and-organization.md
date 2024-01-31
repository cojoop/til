# 초기화와 정리를 위한 라이프사이클

스벨트(`Svelte`)에서 각 컴포넌트는 생명주기(LifeCycle)를 거칩니다. 그중 `onMount`와 `onDestroy`는 컴포넌트의 라이프 사이클을 다루는 함수입니다.

&nbsp;

## onMount

`onMount`는 스벨트 컴포넌트가 `DOM`에 마운트될 때 실행되는 함수입니다. 이 함수는 주로 컴포넌트가 처음으로 화면에 나타날 때 초기화 작업을 수행하는 데 사용됩니다. 주로 `API` 호출, 이벤트 리스너 등을 등록하는 데 활용됩니다.

```html
<script>
    import { onMount } from 'svelte';

    let data;

    onMount(async () => {
        const response = await fetch('https://api.example.com/data');
        data = await response.json();
    });
</script>

{#if data}
    {#each data as item}
        <div>{item.name}</div>
    {/each}
{/if}
```

- `onMount`를 사용하여 `API`를 호출하고, 데이터를 가져와 변수 data에 할당하고 있습니다.
- 이는 컴포넌트가 마운트되면 `API`를 호출하여 데이터를 가져오는 초기화 작업을 수행합니다.

&nbsp;

## onDestroy

`onDestroy`는 컴포넌트가 파괴되기 전에 실행되는 함수입니다. 이 함수는 컴포넌트에서 사용한 리소스를 정리하거나 이벤트 리스너를 제거하는 등의 작업을 수행하는 데 사용됩니다.

```html
<script>
    import { onDestroy } from 'svelte';

    function cleanup() {
        // 이벤트 리스너 제거 또는 기타 정리 작업 수행
    }

    onDestroy(() => {
        cleanup();
    });
</script>
```

- `onDestroy`를 사용하여 컴포넌트가 파괴되기 전에 `cleanup` 함수를 실행하여 정리 작업을 수행합니다.
- 이는 컴포넌트에서 사용한 리소스를 해제하거나 이벤트 리스너를 제거하는 등의 작업을 수행합니다.
