# transition으로 상태 변화를 부드럽게 처리하기

`transition` 속성은 웹 디자인에서 요소의 상태 변화를 부드럽게 처리하기 위한 강력한 기능 중 하나입니다. 이를 이용하면 마우스 오버, 클릭, 클래스 변경 등의 상태 변화에 따라 요소의 스타일이 부드럽게 전환되어 사용자에게 더 나은 시각적 경험을 제공할 수 있습니다.

&nbsp;

#### 기본 구문

```css
transition: property duration timing-function delay;
```

- `property`: 전환 효과를 적용할 CSS 속성의 이름을 지정합니다.
- `duration`: 전환의 지속 시간을 초(s)나 밀리초(ms)로 표기합니다.
- `timing-function`: 전환 효과의 타이밍 함수를 설정합니다.
- `delay`: 전환 효과가 시작되기 전의 대기 시간을 설정합니다.

&nbsp;

#### 사용 예시

```css
.element {
  width: 100px;
  height: 100px;
  background-color: blue;
  transition: width 1s ease-in-out 0.5s;
}

.element:hover {
  width: 200px;
}
```

> 이 예시에서 `.element`라는 요소에 마우스를 올리면 `width` 속성이 1초 동안 부드럽게 `200px`로 전환되며, 시작 대기 시간은 `0.5초`입니다.

&nbsp;

#### 주의사항

- `transition`은 속성 값의 변경에 대해서만 동작하므로 주의가 필요합니다.
- 여러 속성에 대한 전환을 설정할 때는 쉼표로 구분하여 나열할 수 있습니다.

```css
transition: width 1s ease-in-out 0.5s, height 1s ease-in-out 0.5s;
```
