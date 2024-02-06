# goto 함수로 동적 라우팅 하기

`SvelteKit`의 `goto` 함수는 페이지 간의 이동을 처리하는 데 사용됩니다. 이 함수를 사용하여 사용자를 특정 페이지로 이동시킬 수 있습니다. `goto` 함수를 사용하면 내부적으로 페이지를 로드하고 필요한 데이터를 불러오는 등의 작업이 자동으로 처리됩니다.

```js
import { goto } from '@sveltejs/kit'

// 예시: '/about' 페이지로 이동
goto('/about')
```

&nbsp;

## 동적 라우팅

동적 라우팅은 `URL` 경로에 따라 동적으로 콘텐츠를 렌더링하는 방식을 의미합니다.

> 예를 들어, 블로그 게시물의 경우 `URL` 경로에 해당 게시물의 고유 식별자(`ID`)가 포함되어 있을 수 있습니다. 이를 통해 해당 게시물의 데이터를 가져와 렌더링할 수 있습니다.

&nbsp;

```js
// src/routes/[slug].svelte

<script context="module">
  export async function load({ params }) {
    const { slug } = params;
    // slug를 사용하여 해당 데이터를 불러옵니다.
    const postData = await fetch(`https://your-api.com/posts/${slug}`);
    const post = await postData.json();

    if (!post) {
      return {
        status: 404,
        error: new Error(`Post not found`)
      };
    }

    return { props: { post } };
  }
</script>

<script>
  export let post;
</script>

<h1>{post.title}</h1>
<p>{post.content}</p>
```

- `src/routes/[slug].svelte` 파일을 생성합니다.
- `[slug]`는 동적으로 변하는 부분을 의미합니다.

> 사용자가 `/posts/my-post`와 같은 `URL`로 접속하면 `SvelteKit`은 `[slug].svelte` 파일을 찾고 해당 `slug`에 해당하는 데이터를 가져와 렌더링합니다.

&nbsp;

```js
import { goto } from '@sveltejs/kit';

// 예시: 동적 라우팅 페이지로 이동
goto(`/posts/${post.slug}`);
```

- 사용자를 동적 라우팅 페이지로 이동시키려면 `goto` 함수를 사용합니다.
