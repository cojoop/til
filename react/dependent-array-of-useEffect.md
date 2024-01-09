# useEffect의 종속성 배열

**React**의 `useEffect` 훅은 함수 컴포넌트 안에서 `side effects`를 수행하기 위해 사용됩니다. 이 훅은 컴포넌트가 렌더링될 때마다 특정 작업을 수행하거나, 컴포넌트가 업데이트되었을 때 특정 작업을 수행하도록 설정할 수 있습니다. `useEffect`의 두 번째 매개변수인 종속성 배열(dependency array)은 `useEffect`가 실행되는 조건을 결정하는 중요한 역할을 합니다.
> Side Effect: 함수의 로컬 상태를 함수 외부에서 변경하는 경우

<br/>

종속성 배열은 `useEffect`가 특정 값들에 종속되어 있을 때, 해당 값들이 변경되었을 때만 `useEffect`가 실행되도록 지정하는 데 사용됩니다. 종속성 배열이 비어있을 경우, `useEffect`는 컴포넌트가 처음 마운트되었을 때 한 번만 실행되며, 컴포넌트가 언마운트될 때 정리(clean-up) 함수를 실행합니다.

##### 렌더링 될 때마다 useEffect가 실행되는 코드

```js
useEffect(() => {
 // Runs after EVERY rendering
}); 
```

##### 처음 렌더링 될 때에만 useEffect가 실행되는 코드

```js
useEffect(() => {
 // Runs once, after mounting
}, []); 
```

##### dependency1과 dependency2 값들이 변경될 때마다 useEffect가 실행되는 코드

```js
useEffect(() => {
 // Runs after EVERY rendering
}, [dependency1, dependency2]); 
```

> 종속성 배열의 값들이 변할 때마다 `useEffect`가 실행되므로,  불필요한 연산이 발생하지 않도록 주의해야 한다.
