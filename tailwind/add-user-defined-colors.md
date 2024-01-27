# 사용자 정의 색상 추가하기

`Tailwind`는 사전 정의된 색상 팔레트를 제공하지만, 사용자 정의 테마를 만들어서 프로젝트에 고유한 색상을 추가하는 것도 가능합니다.

### 사용자 정의 색상 추가

```js
// tailwind.config.js

export default {
    content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
    theme: {
        extend: {
            // 사용자 정의 색상 추가
            colors: {
                rec: '#212121',
                btn: '#ff8a00',
                // 원하는 만큼 색상 추가 가능
            },
        },
    },
    plugins: [],
};
```

- `rec`와 `btn`과 같은 사용자 정의 색상을 `Tailwind CSS` 클래스로 사용할 수 있습니다.

&nbsp;

### 색상 적용하기

```jsx
<div className="bg-reg p-4">
    <button className='bg-btn text-white itens-center'>버튼</button>
</div>
```
