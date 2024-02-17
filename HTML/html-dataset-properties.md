# HTML의 데이터셋(Dataset) 속성

`HTML`의 데이터셋(`DataSet`)은 요소에 사용자 정의 데이터를 저장하는 데 사용됩니다. 데이터셋은 `data-`접두사를 가진 속성들의 모음으로 이루어져 있습니다.

&nbsp;

## 일반 속성과 DataSet 속성 비교

- **일반 속성:** 일반 속성은 `HTML` 요소의 특정 기능이나 스타일을 지정합니다. 이는 이미 정의된 목적에 따라 사용됩니다.
- **DataSet 속성:** DataSet 속성은 사용자 지정 데이터를 저장하기 위한 것입니다. 이 속성은 `JavsScript`와 `CSS`에서 활용될 수 있습니다.

&nbsp;

## DataSet 속성의 장점

- **유연성:** DataSet 속성을 사용하면 개발자가 원하는 어떠한 데이터도 저장할 수 있습니다.

- **의미 부여:** DataSet 속성은 요소에 추가적인 의미를 부여할 수 있습니다.

&nbsp;

## DataSet 사용사례

1. 추가 정보 저장

```html
<div id="book" data-title="JavaScript Cookbook" data-author="John Doe" data-category="Programming"></div>
```

- 요소에 관련된 정보를 저장할 수 있습니다.
  - ex. 책의 제목, 저자, 카테고리 등

2. 이벤트 처리 및 동적 UI 업데이트

```html
<button id="btn" data-action="submit">Submit</button>
```

- 특정 이벤트가 발생했을 때 데이터셋을 활용하여 `UI`를 동적으로 업데이트할 수 있습니다.

&nbsp;

## DataSet에 배열 객체 데이터 저장

데이터셋은 단일 값만 저장할 수 있습니다. 하지만 배열 객체 데이터를 문자열로 변환하여 저장하고 필요할 때 다시 파싱하여 사용할 수 있습니다.

```js
var data = [1, 2, 3, 4, 5];
var jsonString = JSON.stringify(data);
element.dataset.arrayData = jsonString;
```
