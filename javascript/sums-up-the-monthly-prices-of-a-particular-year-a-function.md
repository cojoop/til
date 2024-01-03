# 특정 연도의 월 가격을 합하는 함수

이 함수는 특정 연도, 가격 조건 및 계획 조건에 따라 총 가격을 계산하는 JavaScript 함수입니다.

```js
function calculateTotalPrice(data, year, conditionPrice, conditionPlan) {
    return data.reduce((total, item) => {
        const itemYear = parseInt(item.bas_dt.substr(0, 4));
        if (itemYear === year) {
            const price =
                item[conditionPrice] !== 0
                    ? item[conditionPrice]
                    : item[conditionPlan];
            return total + price;
        }
        return total;
    }, 0);
}
```

- `reduce` 메서드를 사용하여 데이터 배열을 반복하며 특정 연도의 가격을 합산합니다.
- 각 항목의 연도가 주어진 연도와 일치하는 경우, 해당 항목의 가격을 가져와 조건에 따라 계산합니다.
- 만약 `conditionPrice`에 해당하는 가격이 0이 아니라면 해당 가격을 사용하고, 그렇지 않으면 `conditionPlan`에 해당하는 계획 가격을 사용합니다.
