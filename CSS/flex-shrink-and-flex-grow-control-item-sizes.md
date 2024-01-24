# flex-shrink와 flex-grow로 아이템 크기 제어하기

`Flexbox`는 유연한 레이아웃을 구성하기 위한 강력한 `CSS` 속성 중 하나입니다. 이 중에서도 `flex-shrink`와 `flex-grow`는 Flex 아이템의 크기를 어떻게 조절할지를 결정하는 핵심적인 속성들입니다.

&nbsp;

## flex-shrink

`flex-shrink`는 `Flex` 아이템이 부모 컨테이너 내에서 어떤 비율로 줄어들 수 있는지를 결정합니다. 예를 들어, `flex-shrink: 0;`은 해당 아이템이 축소되지 않음을 의미합니다. 다른 아이템이 축소할 때 해당 아이템은 크기를 고정적으로 유지합니다.

&nbsp;

## flex-grow

`flex-grow`는 `Flex` 아이템이 부모 컨테이너 내에서 어떤 비율로 늘어날 수 있는지를 결정합니다. `flex-grow: 0;`은 해당 아이템이 추가적인 공간을 차지하지 않고 크기를 늘리지 않음을 의미합니다.

&nbsp;

### 사용 예시

```css
.item {
  flex-shrink: 0; /* 아이템이 축소되지 않음 */
  flex-grow: 0;   /* 아이템이 늘어나지 않음 */
  width: 100px;   /* 초기 크기 */
}
```

&nbsp;

> `.item` 클래스를 가진 `Flex` 아이템은 초기 크기를 유지하며, `flex-shrink`와 `flex-grow`가 모두 0으로 설정되어 있어 늘어나거나 축소되지 않습니다.
