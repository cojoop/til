# props와 state의 차이점

**React**에서 `props`와 `state`는 둘 다 컴포넌트의 데이터를 다루는 데 사용되는 개념이지만, 각각의 목적과 특성은 다릅니다.

## Props (속성)

- **읽기 전용(Read-Only):** `props`는 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 데 사용됩니다. 그러나 자식 컴포넌트에서 `props`를 변경할 수 없습니다. `props`는 읽기 전용이며, 한 번 설정되면 해당 컴포넌트에서 변경할 수 없습니다.

- **부모에서 자식으로 전달:** 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 용도로 사용됩니다.

- **외부에서 관리:** 주로 외부에서 컴포넌트에게 데이터를 주입하는 데 사용됩니다.

- **함수형 및 클래스 컴포넌트에서 모두 사용 가능:** 함수형 컴포넌트 및 클래스 컴포넌트에서 모두 `props`를 사용할 수 있습니다.

```jsx
// 부모 컴포넌트에서 자식 컴포넌트로 데이터 전달
function ParentComponent() {
  return <ChildComponent message="안녕하세요!" />;
}

// 자식 컴포넌트에서 props를 받음
function ChildComponent(props) {
  return <div>{props.message}</div>;
}
```

<br/>

## State (상태)

- **변경 가능(Mutable):** `state`는 컴포넌트 내에서 변경 가능한 데이터를 관리합니다. 컴포넌트의 상태가 변경되면 리렌더링이 발생합니다.

- **컴포넌트 내부에서 관리:** 주로 컴포넌트 내부에서 필요한 데이터를 관리하는 데 사용됩니다.

- **setState로 업데이트:** 상태를 업데이트할 때에는 `setState` 메소드를 사용해야 합니다.

- **클래스 컴포넌트에서만 사용 가능:** 함수형 컴포넌트에서는 `React Hooks`를 사용하여 상태를 관리합니다.

```jsx
// 예시: 클래스 컴포넌트에서 state 사용
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  handleClick = () => {
    // setState를 사용하여 상태를 업데이트
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>카운트: {this.state.count}</p>
        <button onClick={this.handleClick}>증가</button>
      </div>
    );
  }
}
```

<br/>

> 즉, `props`는 컴포넌트 간의 데이터 흐름을 조절하고, `state`는 컴포넌트 내에서의 상태 관리를 담당합니다.
