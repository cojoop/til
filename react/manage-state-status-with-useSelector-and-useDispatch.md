# useSelector와 useDispatch로 state 상태 관리하기

`useSelector`와 `useDispatch`는 `Redux` 라이브러리에서 제공하는 훅(`hook`) 중 일부입니다. 이 두 가지 훅은 `React` 애플리케이션에서 `Redux` 상태를 사용하고 상태를 변경하는 데 도움을 줍니다.

<br>

## useSelector

`useSelector`를 사용하여 스토어에 저장 되어 있는 데이터, `state`를 읽을 수 있도록 도와줍니다. 이를 통해 `React` 컴포넌트에서 `Redux`의 전역 상태를 가져와 해당 상태를 현재 컴포넌트에서 사용할 수 있게 됩니다.

```js
const favorites = useSelector((state) => state.favorites.favorites);
```

> `useSelector`의 결과물은 `store.getState()`했을 때의 결과물과 동일합니다.

<br>

## useDispatch

`useDispatch`는 리덕스 스토어의 `dispatch`를 함수에서 사용 할 수 있게 해주는 `Hook` 입니다. `Redux` 스토어에 액션을 디스패치(`dispatch`)하는 데 사용됩니다. 액션을 디스패치하면 `Redux` 스토어의 상태가 갱신되고, 이에 따라 연결된 `React` 컴포넌트들이 업데이트됩니다.

```js
const dispatch = useDispatch();

const onDeleteFavorite = (index) => {
    dispatch(deleteFavorite(index));
};
```

> 액션을 `Redux` 스토어에 발송, 전달을 도와주는 `Hook`입니다
