# contenteditable 속성을 이용하여 사용자 지정 입력 상자 만들기

`HTML`에서는 사용자의 입력을 받기 위해 `input` 요소를 주로 사용합니다. 그러나 때로는 `input` 요소가 아닌 다른 요소를 사용하여 사용자의 입력을 받고자 할 때가 있습니다. 이럴 때 `contenteditable` 속성이 유용하게 활용될 수 있습니다.

&nbsp;

## contenteditable란

contenteditable 속성은 `HTML` 요소가 텍스트 입력이 가능하도록 만들어주는 속성입니다. 이를 이용하면 사용자가 텍스트를 직접 수정할 수 있는 요소를 생성할 수 있습니다. 이 속성은 주로 `<div>`나 `<span>`과 같은 블록 수준 요소에 적용됩니다.

```html
<div contenteditable="true">
    여기에 편집 가능한 텍스트를 입력할 수 있습니다.
</div>
```

&nbsp;

### 사용 예제

다음은 `contenteditable` 속성을 사용하여 타이머를 만드는 코드입니다.

```html
<div id="timer" contenteditable="true">
    00<span>:</span>00
</div>
```

- `<div>` 요소에 `contenteditable="true"` 속성이 적용되어 있습니다.
- 해당 `<div>` 요소 내부의 텍스트를 직접 수정할 수 있습니다.

&nbsp;

> 이렇게 생성된 요소는 일종의 사용자 지정 입력 상자처럼 동작하지만, 내부적으로는 `<div>` 요소이기 때문에 <`input>` 요소를 사용하지 않고도 사용자의 입력을 받을 수 있습니다.
