# Svelte에서 마우스 이벤트 다루기

마우스 이벤트는 웹 애플리케이션에서 상호작용을 추가하는 데 중요한 요소입니다. `Svelte`에서는 이러한 이벤트를 간단하게 처리할 수 있습니다.

&nbsp;

## click 이벤트

마우스 클릭 이벤트는 사용자가 요소를 클릭할 때 발생합니다. 이를 다루기 위해서는 `on:click` 디렉티브를 사용합니다.

```html
<script>
  function handleClick() {
    console.log('마우스를 클릭했습니다!');
  }
</script>

<button on:click={handleClick}>클릭하세요!</button>
```

&nbsp;

## hover 이벤트

요소에 마우스를 올리거나 내릴 때 발생하는 이벤트입니다. 이를 다루기 위해서는 `on:mouseover`와 `on:mouseout`를 사용합니다.

```html
<script>
  function handleMouseOver() {
    console.log('마우스가 요소 위로 올라갔습니다!');
  }

  function handleMouseOut() {
    console.log('마우스가 요소를 벗어났습니다!');
  }
</script>

<div on:mouseover={handleMouseOver} on:mouseout={handleMouseOut}>마우스를 올려보세요!</div>
```

&nbsp;

## 마우스 위치 추적

`on:mousemove` 이벤트를 사용하여 마우스의 현재 위치를 추적할 수 있습니다.

```html
<script>
  function handleMouseMove(event) {
    console.log('마우스의 위치: ', event.clientX, event.clientY);
  }
</script>

<div on:mousemove={handleMouseMove}>마우스를 이동하세요!</div>
```
