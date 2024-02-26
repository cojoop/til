# Padding과 Container의 차이

`Flutter`에서 UI를 설계할 때 `Padding`과 `Container`는 두 가지 주요한 위젯(`Widget`)입니다. 이 두 위젯은 UI 요소를 배치하고 레이아웃을 조정하는 데 사용됩니다.

&nbsp;

## Padding Widget

`Padding` 위젯은 자식 위젯 주위에 간격을 추가하는 데 사용됩니다. 주로 다른 위젯 주위에 여백을 추가하고 싶을 때 사용됩니다.

```dart
Padding(
  padding: EdgeInsets.all(16.0),
  child: Text('Hello, Flutter!'),
)
```

- `Text` 위젯 주위에 `16.0`의 모든 방향으로의 여백을 추가하고 있습니다.

> 버튼 주위에 여백을 추가하여 버튼을 다른 요소와 시각적으로 분리하고자 할 때 유용합니다.

&nbsp;

## Container Widget

`Container` 위젯은 여러 속성을 가진 다목적 위젯으로, 색상, 패딩, 여백, 경계선, 그림자 등을 지정할 수 있습니다. 따라서 더 많은 커스터마이징이 필요한 경우에 주로 사용됩니다.

```dart
Container(
  padding: EdgeInsets.all(16.0),
  margin: EdgeInsets.symmetric(vertical: 10.0),
  decoration: BoxDecoration(
    color: Colors.blue,
    borderRadius: BorderRadius.circular(8.0),
  ),
  child: Text('Container Example'),
)
```

- `Container` 위젯을 사용하여 여백을 설정하고, 배경색을 지정하고, 테두리를 둥글게 만들고 있습니다.

> `Container`는 레이아웃 구성 요소와 장식 요소를 모두 가질 수 있습니다.

&nbsp;

**_간단히 말해서, `Padding`은 자식 위젯 주위에 공간을 추가할 때 사용되며, `Container`는 UI를 커스터마이징하고 여러 요소를 그룹화하고 스타일을 적용할 때 사용됩니다._**
