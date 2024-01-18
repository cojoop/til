# splice 메서드로 배열의 내용을 추가하거나 제거하기

`splice` 메서드는 배열의 내용을 추가하거나 제거하는 데 사용됩니다. 이 메서드는 배열의 특정 위치에서 요소를 추가하거나 제거하고 배열의 길이를 조절하는 데 유용합니다.

splice 메서드의 일반적인 구문은 다음과 같습니다:

```js
array.splice(startIndex, deleteCount, item1, item2, ...);
```

- `startIndex`: 배열에서 변경을 시작할 인덱스입니다.
- `deleteCount`: 제거할 요소의 수입니다. 0이면 요소를 제거하지 않습니다.
- `item1, item2, ...`: 추가할 요소입니다. 이 부분은 선택적이며, 생략하면 요소를 제거만 합니다.

<br>

##### 배열에서 특정 인덱스의 요소를 제거한 후 업데이트된 배열을 상태로 설정하는 함수

```js
const onDeleteFavorite = (index) => {
    const updatedFavorites = [...favorites];
    updatedFavorites.splice(index, 1);
    setFavorites(updatedFavorites);s
};
```

> `splice` 메서드는 배열을 수정하므로 주의가 필요합니다. 필요에 따라 원본 배열을 변경하지 않고 새로운 배열을 생성하는 경우에는 `slice` 메서드를 사용하는 것이 좋습니다.
