# HTML 요소의 스타일을 변경하는 함수

이 함수는 JavaScript와 jQuery를 사용하며, 지정된 HTML 요소의 배경색과 테두리 색상이 매개변수로 전달된 값으로 변경됩니다.

```js
function applyCircleStyles(elementId, bgColor, borderColor) {
    $(elementId).css({
        'background-color': bgColor,
        border: `2px solid ${borderColor}`,
    });
}
```

- `$(elementId)`는 jQuery를 사용하여 해당 ID를 가진 HTML 요소를 선택합니다.
- `.css()` 함수는 선택된 요소의 CSS 스타일을 변경합니다.
- `${}` 구문은 템플릿 리터럴을 사용하여 변수 값을 문자열 안에 삽입합니다.
