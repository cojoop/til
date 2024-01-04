# Handsontable 라이브러리를 사용하여 표를 생성하고 표시하는 함수

이 코드는 웹 페이지에서 테이블을 생성하고 사용자가 데이터를 수정하면 해당 변경 내용을 추적하고, 선택한 행에 따라 다운로드 버튼을 표시하거나 숨깁니다. `Handsontable` 라이브러리의 여러 기능을 활용하여 유연한 테이블 기능을 구현하고 있습니다.

```js
let handsontableExample = null;  // Handsontable 인스턴스를 저장할 변수
let editRows = {};  // 수정된 행의 데이터를 추적하는 객체

// 테이블 초기화 및 Handsontable 인스턴스 생성 함수
function initializeTable() {
    if (handsontableExample) {
        handsontableExample.destroy();  // 이미 존재하는 Handsontable이 있다면 파괴
        handsontableExample = null;
    }

    const container = document.getElementById('example_table');  // HTML 요소에서 테이블 컨테이너 가져오기
    handsontableExample = new Handsontable(container, {
        licenseKey: 'your-license-key',  // 라이선스 키 설정
        data: [],  // 초기 데이터는 빈 배열
        colHeaders: ['header1', 'header2', 'header3'],  // 열 헤더 지정
        rowHeaders: true,  // 행 헤더 표시
        columns: [
            { data: 'column1' },
            { data: 'column2' },
            { data: 'column3' }
        ],  // 각 열의 데이터 속성 지정
        plugins: ['exportFile'],  // 파일 내보내기 플러그인 추가
        columnSorting: { enabled: true, sortIndicator: true },  // 열 정렬 활성화
        stretchH: 'all',  // 모든 열의 너비를 테이블 너비에 맞게 조절
        height: 500,  // 테이블의 높이 설정
        afterChange: function (changes, source) {
            // 'edit' 또는 'CopyPaste.paste'로 인한 변경사항을 캐치하고 editRows 객체를 업데이트
            if (source === 'edit' || source === 'CopyPaste.paste') {
                changes.forEach(([row, , , newValue]) => {
                    const rowData = handsontableExample.getDataAtRow(row);
                    const rowKey = Object.values(rowData).join('|');
                    editRows[rowKey] = rowData;
                });
            }
        },
    });

    handsontableExample.addHook('afterSelection', (col, row, col2, row2) => {
        const selectedRows = handsontableExample.getSelected() || [];
        const selectedRowsData = {};

        if (selectedRows.length > 0) {
            selectedRows.forEach(([startRow, , endRow]) => {
                for (let i = startRow; i <= endRow; i++) {
                    const rowData = handsontableExample.getDataAtRow(i) || {};
                    if (rowData.column1) {
                        const key = `${rowData.column1}_${rowData.column2}_${rowData.column3}`;
                        selectedRowsData[key] = rowData;
                    }
                }
            });

            // 선택된 행이 있으면 다운로드 버튼을 표시
            $("#downloadButton").toggleClass("hide", Object.keys(selectedRowsData).length === 0);
        } else {
            // 선택된 행이 없으면 다운로드 버튼 숨김
            $("#downloadButton").addClass("hide");
        }
    });
}
```

- `Handsontable` 인스턴스 초기화 및 설정
  - 초기화 및 설정된 `Handsontable`은 특정 옵션들로 구성되어 있으며, 초기 데이터가 비어 있는 상태로 시작합니다.
- 이전 `Handsontable` 인스턴스의 제거
  - 이전에 생성된 `example_table` 인스턴스가 존재하면 (`example_table` 변수가 존재할 때), 해당 인스턴스를 제거하고 메모리에서 해제합니다.
- 이벤트 핸들링 - `afterChange`
  - `afterChange` 이벤트 핸들러는 사용자에 의한 표의 변경 사항을 감지하고, 변경된 행의 데이터를 추적하는 `editRows` 객체를 업데이트합니다.
- 이벤트 후크 - `afterSelection`
  - `afterSelection` 후크는 사용자가 표에서 행을 선택할 때 호출됩니다.
  - 선택된 행의 데이터를 추출하고, 고유한 키를 생성하여 `selectedRowsData` 객체에 저장합니다.
