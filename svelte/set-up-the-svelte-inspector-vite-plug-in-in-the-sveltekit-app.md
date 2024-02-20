# SvelteKit 앱에서 svelte-inspector vite 플러그인 설정하기

`Svelte Inspector`는 `Svelte` 애플리케이션을 디버깅하고 모니터링하기 위한 도구 중 하나입니다. `Svelte Inspector`를 사용하면 애플리케이션의 동작을 더 쉽게 이해하고 디버깅할 수 있습니다.

&nbsp;

#### `svelte.config.js` 파일 내 `SvelteKit`의 경우 다음을 추가합니다

```js
//in svelte.config.js
const config = {
  // ...
  vitePlugin: {
    inspector: true,   
  },
}
```
