# 입력된 두 날짜를 비교하여 설정하고 날짜 정보를 객체에 저장하는 함수

이 함수는 두 개의 날짜 입력(`input`) 요소로부터 날짜를 읽어들이고, 이를 비교하여 조건에 맞게 날짜를 조정하고 선택된 날짜 정보를 객체에 저장하는 함수입니다.

```js
function handleDateChange(fromInput, toInput) {
    // 시작 날짜와 종료 날짜의 값을 가져옴
    const selFromDate = fromInput.val();
    const selToDate = toInput.val();

    // 시작 날짜가 종료 날짜보다 클 경우, 시작 날짜를 종료 날짜로 설정
    if (selFromDate > selToDate) {
        fromInput.val(selToDate);
    } else if (selToDate < selFromDate) {
        // 종료 날짜가 시작 날짜보다 클 경우, 종료 날짜를 시작 날짜로 설정
        toInput.val(selFromDate);
    }

    // 선택된 연도와 월을 추출하여 변수에 저장
    const selYear = selFromDate.substring(0, 4);
    const selMonth = selFromDate.substring(5, 7);

    // 선택된 연도나 월이 이전과 다를 경우, 객체에 새로운 연도와 월을 저장
    if (selYear !== selData.year || selMonth !== selData.month) {
        selData.year = selYear;
        selData.month = selMonth;
    }

    // 선택된 날짜 범위가 이전과 다를 경우, 로컬 스토리지에 저장
    if (selFromDate !== selData.from_date || selToDate !== selData.to_date) {
        localStorage.setItem('usage_sel_data', JSON.stringify(selData));
    }
}
```

- 시작 날짜가 종료 날짜보다 크면 시작 날짜를 종료 날짜로 설정하고, 종료 날짜가 시작 날짜보다 크면 종료 날짜를 시작 날짜로 설정합니다.
- 선택된 연도나 월이 이전과 다를 경우, `selData` 객체에 새로운 연도와 월을 업데이트합니다.
- 선택된 날짜 범위가 이전과 다를 경우, `localStorage`에 `usage_sel_data` 키로 `JSON` 문자열로 변환한 `selData` 객체를 저장합니다. 선택된 날짜 정보를 유지하기 위한 목적으로 사용될 수 있습니다.Z
