# Outlet 컴포넌트 사용방법

`Outlet`은 `React Router v6`에서 도입된 새로운 개념으로, 중첩된 라우팅 구조를 구성할 수 있도록 해주는 컴포넌트입니다. `Outlet` 컴포넌트는 라우팅 컴포넌트 내부에서 사용되며, 중첩된 자식 라우트가 렌더링 되는 위치를 지정합니다.
<br />

## 중첩 라우팅(Nested Routes)이란

중첩 라우팅은 여러 수준의 라우트를 효과적으로 관리하기 위한 방법 중 하나입니다. 중첩 라우팅을 사용하면 하나의 부모 컴포넌트 안에 여러 하위 라우터를 넣어 각각의 라우터가 독립적으로 작동할 수 있습니다.
<br>

##### 중첩된 라우트를 사용하지 않은 코드

```jsx
export default function App() {
    return (
        <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/profiles" element={<Profile />} />
            <Route path="/profiles/:username" element={<Profile />} />
            <Route path="/articles" element={<Articles />} />
            <Route path="/articles/:id" element={<Article />} />
        </Routes>
  );
}
```

##### 중첩된 라우트를 사용한 코드

```jsx
export default function App() {
    return (
        <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/profiles" element={<Profile />} />
                <Route path=":username" element={<Profile />}>
            <Route path="/articles" element={<Articles />}>
                <Route path=":id" element={<Article />} />
            </Route>
        </Routes>
  );
}
```

> 경로를 중첩하여 사용하면 더 세분화하여 사용할 수 있습니다. 만약 경로가 `/profiles/1` 이 들어오게 되면 7번째 줄 코드가 실행되고, `/articles/2` 가 들어오면 9번째 줄 코드가 실행됩니다. 각각의 파라미터 값은 value가 됩니다.

<br>

## Outlet을 사용하여 공통된 레이아웃 만들기

```jsx
import { Outlet } from "react-router-dom";

export default function RootLayout() {
    return (
        <>
            <h1>Header</h1>
            <Outlet>
        </>
  );
}
```

각 페이지 컴포넌트가 보여져야 하는 부분에 `Outlet` 컴포넌트를 넣었습니다.

```jsx
export default function App() {
    return (
        <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />

            <Route element={<RootLayout />}>
                <Route path="/profiles" element={<Profile />} />
                    <Route path=":username" element={<Profile />}>
                <Route path="/articles" element={<Articles />}>
                    <Route path=":id" element={<Article />} />
            </Route>
        </Routes>
  );
}
```

`/articles`, `/profile` 경로로 들어가면 `RootLayout` 안의 `Outlet` 영역에 각 `Route`에 매칭 시켜놓은 `element` 들이 렌더링 되어 나타나게 됩니다.
