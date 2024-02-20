# data-sveltekit-prefetch로 데이터 사전 로딩하기

`SvelteKit`에는 페이지 전환 시에 필요한 데이터를 미리 로드하여 페이지 전환 속도를 향상시키는 `data-sveltekit-prefetch` 기능이 있습니다. 이 기능을 사용하면 사용자가 링크를 클릭하기 전에 페이지로 이동하는 동안 필요한 데이터를 백그라운드에서 미리 로드할 수 있습니다.

&nbsp;

## data-sveltekit-prefetch 속성

`data-sveltekit-prefetch`속성은 `<a>` 태그에 추가되는 특별한 속성입니다. 이 속성을 사용하면 `SvelteKit`이 해당 링크가 포함된 페이지로 이동하기 전에 브라우저가 해당 페이지에 필요한 데이터를 미리 가져올 수 있습니다.

#### 예제 코드

```html
<nav>
 <a href="/">Home</a>
 <a href="/shop" data-sveltekit-prefetch>Shop</a>
 <a href="/movies" data-sveltekit-prefetch>Movies</a>
</nav>
```

- 네비게이션 링크에 `data-sveltekit-prefetch` 속성이 추가되었습니다.
- 사용자가 `Shop` 또는 `Movies` 링크를 클릭하기 전에 `SvelteKit`은 백그라운드에서 해당 페이지에 필요한 데이터를 미리 가져옵니다.

&nbsp;

```html
<nav>
 <a href="/">Home</a>
 {#each categories as category}
  <a href={`/category/${category.id}`} data-sveltekit-prefetch>{category.name}</a>
 {/each}
</nav>
```

- 동적으로 생성된 카테고리 링크를 포함하고 있습니다.
- 각 카테고리에 대한 페이지로 이동하기 전에 `SvelteKit`은 해당 페이지에 필요한 데이터를 미리 가져옵니다.
