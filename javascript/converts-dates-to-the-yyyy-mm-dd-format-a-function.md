# 날짜를 "yyyy-mm-dd" 형식으로 변환하는 함수

이 함수는 주어진 날짜 객체를 `"yyyy-mm-dd"` 형식의 문자열로 변환합니다.

```js
function getFormattedDate(date) {
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');
    return `${year}-${month}-${day}`;
}
```

- 하나의 매개변수인 `date`를 받으며, 이 `date`는 JavaScript의 `Date` 객체로 전달되어야 합니다.
- `return ${year}-${month}-${day};`으로 년도, 월, 일을 조합하여 "yyyy-mm-dd" 형식의 문자열을 생성하고 반환합니다.
