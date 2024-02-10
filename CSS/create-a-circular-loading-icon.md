# 원형 로딩 아이콘 만들기

CSS로 원형 로딩 아이콘을 만들려면 몇 가지 중요한 스타일과 애니메이션을 설정해야 합니다.

## 클래스 스타일

`.loader`라는 클래스로 로딩 아이콘 스타일을 설정했습니다.

```css
.loader {
    border: 4px solid #f3f3f3;
    border-top: 4px solid #3498db;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    animation: spin 2s linear infinite;
    margin: auto;
}

```

- `border`: 로딩 아이콘의 테두리 스타일과 색상을 설정합니다.
- `border-top`: 로딩 바의 윗 부분을 나타내는 색상을 설정합니다.
- `border-radius`: 원형 로딩 아이콘을 만들기 위해 반지름을 설정합니다.
- `width` 및 `height`: 로딩 아이콘의 크기를 설정합니다.
- `animation`: `spin` 애니메이션을 적용하여 회전 효과를 만듭니다.
- `margin`: 로딩 아이콘을 수평으로 가운데 정렬합니다.

&nbsp;

## @keyframes spin 애니메이션

```css
@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}
```

- `@keyframes`: CSS 애니메이션을 정의하기 위한 키워드입니다.
0%와 100%: 애니메이션의 시작과 종료 지점을 나타냅니다.
- `transform`: `rotate()`: 요소를 회전시키는 CSS 속성으로, 시작 시점에서 종료 시점까지 360도 회전합니다.
