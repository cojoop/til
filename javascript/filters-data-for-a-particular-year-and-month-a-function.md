# 특정 연도와 월에 해당하는 데이터를 필터링하는 함수

이 함수는 주어진 연도와 월에 해당하는 데이터만 포함된 새로운 배열이 반환됩니다. 이 때, `data` 배열은 변경되지 않습니다.

```js
function filterByYearAndMonth(data, year, month) {
    return data.filter((item) => {
        const itemYear = parseInt(item.bas_dt.substr(0, 4));
        const itemMonth = parseInt(item.bas_dt.substr(5, 2));
        return itemYear === year && itemMonth === month;
    });
}
```

- `filter` 함수는 배열의 각 요소에 대해 주어진 조건을 기반으로 필터링된 배열을 생성합니다.
- `item.bas_dt`는 배열 요소의 `bas_dt` 속성을 나타냅니다. 이 속성은 날짜 정보를 가진 문자열로 가정합니다. (예: "YYYY-MM-DD" 형식)
- `return itemYear === year && itemMonth === month;`는 주어진 year와 month 값과 각 데이터 요소의 연도 및 월을 비교하여 조건을 검사합니다.
