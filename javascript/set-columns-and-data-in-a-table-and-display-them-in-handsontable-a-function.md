# 테이블에 열과 데이터를 설정하고 Handsontable에 표시하는 함수

 이 함수는 동적으로 테이블의 컬럼과 데이터를 설정하고, 주어진 조건에 따라 데이터를 필터링하고 정렬하여 Handsontable에 표시합니다.

```js
function showTableUsage() {
  // 초기값 설정
  let s_source = "전력";
  let s_unit = "금액";
  let colHeaders = ['group1', 'group2', 'date'];
  let columns = [{ data: 'group1' }, { data: 'group2' }, { data: 'date' }];

  // 컬럼 동적 생성
  ["pwr", "eng"].forEach((v1) => {
    if (v1 === sel_data.target || sel_data.target === "all") {
      s_source = sel_labels.target[v1];

      ["amt", "money"].forEach((v2) => {
        if (v2 === sel_data.unit || sel_data.unit === "all") {
          s_unit = sel_labels.unit[v2];
          colHeaders.push(`${s_source}${s_unit}`);
          colHeaders.push(`${s_source}${s_unit} 누계`);
          columns.push({ data: `${v1}_${v2}`, type: 'numeric', numericFormat: { pattern: '0,0.0' } });
          columns.push({ data: `${v1}_${v2}_tot`, type: 'numeric', numericFormat: { pattern: '0,0.0' } });
        }
      });
    }
  });

  colHeaders.push(`전력단가`);
  columns.push({ data: 'pwr_price', type: 'numeric', numericFormat: { pattern: '0,0.0' } });
  colHeaders.push(`에너지단가`);
  columns.push({ data: 'eng_price', type: 'numeric', numericFormat: { pattern: '0,0.0' } });
  colHeaders.push(`최종수정일시`);
  columns.push({ data: 'date_modified' });

  // 주기에 따라 데이터 필터링
  let filter_data = [];
  switch (sel_data.cycle) {
    case "일":
      colHeaders[2] = "대상 일";
      filter_data = filterDataByDay(table_json);
      break;
    case "주":
      colHeaders[2] = "대상 주";
      filter_data = filterDataByWeek(table_json);
      break;
    case "월":
      colHeaders[2] = "대상 월";
      filter_data = filterDataByMonth(table_json);
      break;
  }

  // 그룹 필터 적용
  if (sel_data.group1 !== "") {
    filter_data = filter_data.filter((row) => row.group1 === sel_data.group1);
  }
  if (sel_data.group2 !== "") {
    filter_data = filter_data.filter((row) => row.group2 === sel_data.group2);
  }

  // 데이터 정렬
  filter_data = filter_data.sort((a, b) => a.group1.localeCompare(b.group1) || a.group2.localeCompare(b.group2) || a.date.localeCompare(b.date));

  // Handsontable에 설정 및 데이터 로드
  handsontable.updateSettings({ colHeaders: colHeaders, columns: columns });
  handsontable.loadData(filter_data);
}
```

- 변수 초기화
  - `colHeaders`는 `group1`, `group2`, `date`라는 세 개의 문자열을 포함하는 배열로 초기화됩
- 동적 컬럼 생성
  - 중첩된 루프가 실행되어, `pwr`, `eng` 이라는 값들에 대해 각각의 경우를 고려합니다.
- 그룹 필터 적용
  - 만약 `sel_data.group1`이나 `sel_data.group2`가 비어있지 않다면, 해당 그룹에 맞는 데이터만 필터링합니다.
- Handsontable에 설정 및 데이터 로드
  - `handsontable` 객체의 `updateSettings` 메서드를 사용하여 `Handsontable`에 새로운 컬럼 헤더 및 데이터를 설정합니다.
