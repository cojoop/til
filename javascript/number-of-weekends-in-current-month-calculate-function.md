# 현재 월의 주말 개수를 계산하는 함수

이 함수는 이번 달의 첫째 날부터 마지막 날까지의 날짜를 반복하고, 각 날짜가 주말인지 확인하여 카운트합니다. 이후 주말 수를 반환합니다.

```js
function countWeekendsInMonth() {
    const currentDate = new Date();
    const year = currentDate.getFullYear();
    const month = currentDate.getMonth();

    const firstDayOfMonth = new Date(year, month, 1);
    const lastDayOfMonth = new Date(year, month + 1, 0);

    let weekendCount = 0;

    for (let i = firstDayOfMonth.getDate(); i <= lastDayOfMonth.getDate(); i++) {
        const tempDate = new Date(year, month, i);
        if (tempDate.getDay() === 0 || tempDate.getDay() === 6) {
            weekendCount++;
        }
    }

    return weekendCount;
}
```

- `const firstDayOfMonth = new Date(year, month, 1);`을 통해 해당 월의 첫째 날을 나타내는 Date 객체를 생성합니다.
- `const lastDayOfMonth = new Date(year, month + 1, 0);`을 사용하여 해당 월의 마지막 날을 나타내는 Date 객체를 생성합니다. d
- `tempDate.getDay() === 0 || tempDate.getDay() === 6` 조건을 사용하여 토요일(6) 또는 일요일(0)인 경우 주말로 간주하고 weekendCount를 증가시킵니다.
