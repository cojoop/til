# Handsontable 인스턴스 초기화 및 구성하는 함수

이 함수는 Handsontable 표를 생성하고 표시하는 역할을 합니다.

```js
handsontable: null,
edit_rows: {},  // 객체로 수정된 행의 데이터를 추적하는 용도
init_table: function () {
    if (handsontable) {
        // 기존 Handsontable 인스턴스가 존재하면 제거
        handsontable.destroy();
        handsontable = null;
    }

    // 테이블을 표시할 HTML 컨테이너를 가져옵니다.
    const container = document.getElementById('handsontable');

    // Handsontable 인스턴스를 초기화합니다.
    handsontable = new Handsontable(container, {
        licenseKey: 'non-commercial-and-evaluation',
        data: [],
        colHeaders: ['header1', 'header2', 'header3'],
        rowHeaders: true,
        columns: [{ data: 'column1' }, { data: 'column2' }, { data: 'column3' }],
        plugins: ['exportFile'],
        columnSorting: { enabled: true, sortIndicator: true },
        stretchH: 'all',
        height: 900,
        afterChange: function (changes, source) {
            // 'edit' 또는 'CopyPaste.paste'로 인한 변경사항을 캐치하고 edit_rows 객체를 업데이트
            if (source === 'edit' || source === 'CopyPaste.paste') {
                changes.forEach(([row, , , newValue]) => {
                    const row_data = handsontable.getDataAtRow(row);
                    // 행의 데이터를 문자열로 합쳐서 고유한 키 생성
                    const row_key = Object.values(row_data).join('|');
                    edit_rows[row_key] = row_data;
                });
            }
        },
    });

    // 테이블의 선택된 행에 대한 후크를 추가합니다.
    handsontable.addHook('afterSelection', (col, row, col2, row2) => {
        // 선택된 행을 저장할 객체를 초기화합니다.
        const sel_rows = {};

        if (sel_rows.length > 0) {
            // 선택된 행의 정보를 추출하여 sel_rows 객체에 저장
            sel_rows.forEach(([startRow, , endRow]) => {
                for (let i = startRow; i <= endRow; i++) {
                    const row_data = handsontable.getDataAtRow(i) || {};
                    if (row_data.group1) {
                        // 선택된 행의 고유한 키를 생성하여 sel_rows 객체에 저장
                        const s_key = `${sel_data.target}_${row_data.cycle}_${row_data.date}`;
                        sel_rows[s_key] = row_data;
                    }
                }
            });

            // 선택된 행이 있으면 다운로드 버튼을 표시
            $("#btn_down_xlsx").toggleClass("hide", Object.keys(sel_rows).length === 0);
        } else {
            // 선택된 행이 없으면 다운로드 버튼을 숨김
            sel_rows = {};
            $("#btn_down_xlsx").addClass("hide");
        }
    });
},
```

- Handsontable 인스턴스 초기화 및 설정
  - 초기화 및 설정된 Handsontable은 특정 옵션들로 구성되어 있으며, 초기 데이터가 비어 있는 상태로 시작합니다.
- 이전 Handsontable 인스턴스의 제거
  - 이전에 생성된 `Handsontable` 인스턴스가 존재하면 (`handsontable` 변수가 존재할 때), 해당 인스턴스를 제거하고 메모리에서 해제합니다.
- 이벤트 핸들링 - `afterChange`
  - `afterChange` 이벤트 핸들러는 사용자에 의한 표의 변경 사항을 감지하고, 변경된 행의 데이터를 추적하는 `edit_rows` 객체를 업데이트합니다.
- 이벤트 후크 - `afterSelection`
  - `afterSelection` 후크는 사용자가 표에서 행을 선택할 때 호출됩니다.
  - 선택된 행의 데이터를 추출하고, 고유한 키를 생성하여 `sel_rows` 객체에 저장합니다.
