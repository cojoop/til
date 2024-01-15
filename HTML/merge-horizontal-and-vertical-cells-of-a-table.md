# 테이블(table) 가로, 세로 셀 병합하기

테이블에서의 가로와 세로 셀 병합은 웹 페이지에서 정보를 구조화하고 시각적으로 표현하는 데 매우 중요한 부분입니다. 가로 셀 병합은 제목 행을 강조하거나 여러 열을 하나로 합칠 때, 세로 셀 병합은 특정 항목을 강조하거나 세부 정보를 표현하는데 활용될 수 있습니다.

## 세로 셀 병합 (rowspan)

```html
<<table>
  <tr>
    <th>항목 1</th>
    <th colspan="2">항목 2 (가로 병합)</th>
    <th>항목 3</th>
  </tr>
  <tr>
    <td>데이터 1</td>
    <td>데이터 2</td>
    <td>데이터 3</td>
    <td>데이터 4</td>
  </tr>
</table>
```

- 병합을 시작하려는 `cell`에 `rowspan`을 정의하고,
병합할 `row`의 갯수를 지정합니다.

<br>

## 가로 셀 병합 (colspan)

```html
<table>
  <tr>
    <th>학년</th>
    <th>반</th>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
  </tr>
  <tr>
    <td colspan='2'>2-1</td>
  </tr>
</table>
```

- 병합하려는 `cell`에 `'colspan'` 속성을 정의하고, 병합할 `cell`의 갯수를 지정합니다.

<br>

## 가로/세로 셀 모두 병합 (rowspan, colspan)

```html
<table>
  <tr>
    <td rowspan='2' colspan='2'>1</td>
    <td>3</td>
  </tr>
  <tr>
    <td>6</td>
  </tr>
  <tr>
    <td>7</td>
    <td>8</td>
    <td>9</td>
  </tr>
</table>
```

- 병합하려는 첫번째 셀에 `colspan`과 `rowspan`을 정의합니다.
