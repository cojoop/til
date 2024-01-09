# react-router-dom v6을 이용한 라우팅 기능 구현하기

`React Router v6`은 React 애플리케이션의 라우팅을 관리하기 위한 `React Router` 라이브러리의 버전 중 하나입니다. `React Router`는 React 애플리케이션에서 페이지 간의 네비게이션과 URL을 통한 라우팅을 쉽게 관리할 수 있도록 도와주는 라이브러리입니다.
<br/>

### 설치

아래의 명령어를 입력하여 `React Router V6`를 설치합니다.

```bash
npm install react-router-dom@next
```

<br/>

### Index.jsx 세팅

`index.jsx` 파일을 다음과 같이 세팅해야 합니다.

```jsx
import { BrowserRouter } from 'react-router-dom';
```

```jsx
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

<br/>

### <Routes\>와 <Route\> 사용

```jsx
<Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
    <Route path="/contact" element={<Contact />} />
</Routes>
```

- `<Routes>`: 라우트의 집합을 나타냅니다. 여기에 여러 `<Route>` 요소를 넣어서 각 경로에 대한 컴포넌트를 정의할 수 있습니다.
- `<Route>`: 경로와 매핑되는 컴포넌트를 정의합니다. `path prop`으로 경로를 지정하고, `element prop`으로 해당 경로에 매칭될 컴포넌트를 지정합니다.

> `Routes` 안에 `Route` 컴포넌트를 만들고 `path` 값으로 이동할 경로를 넣고 `element` 값으로 보여줄 컴포넌트 or `HTML` 태그를 작성해야 합니다.

<br />

### <Link\> 사용

```jsx
<Link to="/">HOME</Link>
```

`<Link>`는 `to prop`을 받아 해당 경로로 이동하는 링크를 생성합니다. 이때 `to prop`에는 이동하고자 하는 경로를 지정합니다.

> `React Router v6`에서는 `NavLink`라는 컴포넌트도 제공되는데, 이는 `Link`와 유사하지만 현재 페이지와 링크된 페이지가 동일할 때 추가적인 스타일을 적용할 수 있도록 해줍니다.

<br/>

### 라우터 적용하기

```jsx
/* App.js */
<>
    <Link to="/">HOME</Link>
    <br />
    <Link to="/about">ABOUT</Link>
    <br />
    <Link to="/contact">CONTACT</Link>
    <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
    </Routes>
</>
```
