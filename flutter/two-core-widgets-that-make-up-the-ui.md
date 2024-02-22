# UI를 구성하는 두 가지 핵심 위젯(Widget)

`Flutter`는 UI를 구성하는 데 두 가지 핵심 위젯인 `StatelessWidget`과 `StatefulWidget`을 제공합니다. 각각의 위젯은 다른 상황에서 사용되며, 각자의 장단점을 가지고 있습니다.

&nbsp;

## StatelessWidget

`StatelessWidget`은 상태가 없는 위젯입니다. 한 번 그려지면 그 상태를 변경할 수 없습니다. 이는 데이터가 변경되지 않고 UI가 변하지 않는 경우에 사용됩니다.

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Text('Hello, World!'),
    );
  }
}
```

- 한 번 그려진 후에는 상태가 변하지 않음
- 빠르고 경제적인 렌더링을 지원

> 단순한 텍스트, 이미지, 아이콘 등을 표시하는 데 사용될 수 있습니다.

&nbsp;

## StatefulWidget

`StatefulWidget`은 상태를 가지는 위젯입니다. 화면의 상태가 변경될 수 있는 경우에 사용하고, 변경된 상태에 따라 UI를 업데이트할 수 있습니다.  `StatefulWidget`은 내부에 상태를 가지고 있어서 이 상태가 변경될 때마다 `Flutter` 프레임워크에 의해 다시 그려지게 됩니다.

```dart
class CounterWidget extends StatefulWidget {
  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Counter: $_counter'),
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

- 상태가 변경될 수 있음
- 동적인 UI를 구현할 수 있음
- 내부에 상태(State) 객체를 가지고 있음

> 주로 사용자 입력을 처리하거나, 동적으로 변경되는 데이터를 표시할 때 사용됩니다.

&nbsp;

## StatelessWidget과 StatefulWidget의 선택

어떤 위젯을 선택할지는 화면의 요구사항에 따라 달라집니다. 일반적으로 다음과 같은 지침을 따를 수 있습니다:

**정적인 UI:** 화면에 표시되는 내용이 사용자의 입력이나 데이터 변경에 관계없이 항상 동일한 경우, `StatelessWidget`을 사용합니다.

**동적인 UI:** 화면의 상태가 사용자의 입력이나 데이터 변경에 의해 변하는 경우, `StatefulWidget`을 사용합니다. 예를 들어, 리스트나 폼과 같은 동적인 컨텐츠를 표시할 때 사용됩니다.
