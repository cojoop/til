# DB 데이터를 이용하여 엑셀 파일 생성하는 함수

이 함수는 DB 데이터를 사용하여 엑셀 파일을 생성하는 함수입니다. `openpyxl` 라이브러리를 사용하여 엑셀 파일을 다룹니다.

```python
def create_excel_by_dashboard(self, file_name, rows):
    """DB 데이터를 이용하여 엑셀 파일 생성"""
    # 기본 엑셀 파일 경로
    base_xlsx = "dashapp/xlsx/base/form_dashboard.xlsx"
    # 엑셀 파일 열기
    wb = load_workbook(base_xlsx, data_only=False)
    ws = wb['data']  # 데이터 시트 선택
    iRow = 2

    # 대시보드 데이터를 엑셀에 입력
    for row in rows:
        ws.cell(row=iRow, column=1).value = row.get('group1', '')
        ws.cell(row=iRow, column=2).value = row.get('group2', '')
        ws.cell(row=iRow, column=3).value = row.get('cycle', '')
        ws.cell(row=iRow, column=4).value = row.get('bas_dt', '')
        ws.cell(row=iRow, column=5).value = row.get('pwr_amt', '')
        ws.cell(row=iRow, column=6).value = row.get('pwr_amt_tot', '')
        ws.cell(row=iRow, column=7).value = row.get('eng_amt', '')
        ws.cell(row=iRow, column=8).value = row.get('eng_amt_tot', '')
        ws.cell(row=iRow, column=9).value = row.get('out_amt', '')
        ws.cell(row=iRow, column=10).value = row.get('out_amt_tot', '')
        ws.cell(row=iRow, column=11).value = row.get('pwr_price', '')
        ws.cell(row=iRow, column=12).value = row.get('eng_price', '')

        iRow += 1

    # 생성된 엑셀 파일 저장
    output_file = f"dashapp/xlsx/{file_name}"
    wb.save(output_file)
    return output_file
```

<br>

#### 엑셀 파일 열기

- `load_workbook` 함수를 사용하여 기본 엑셀 파일을 엽니다.
- `data_only=False`는 수식이 아닌 값으로 데이터를 가져오도록 설정합니다.
- 선택된 시트의 객체를 `ws`에 할당합니다.

<br>

#### 데이터 입력

- `ws.cell(row=iRow, column=j).value = row.get(column_name, '')`를 사용하여 각 열에 데이터를 입력합니다.
- `row.get(column_name, '')`는 딕셔너리 `row`에서 `column_name`에 해당하는 값을 가져오는데, 만약 값이 없으면 `빈 문자열('')`을 사용합니다.
