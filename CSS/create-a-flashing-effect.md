# 깜빡이는 효과 만들기

`CSS`의 애니메이션을 사용해서 `HTML` 요소에 깜빡이는 효과를 줄 수 있습니다.

```css
@keyframes blink-effect {
  50% {
    opacity: 0;
  }
}

.blink {
  animation: blink-effect 1s step-end infinite;
}
```

<br>

#### @keyframes 규칙

애니메이션의 키프레임(`keyframes`)을 정의하며, 50% 지점에서 `opacity` 속성을 0으로 설정하여 투명도를 조절합니다.
> 애니메이션은 0%에서 시작하여 100%까지 진행됩니다.

<br>

#### .blink 클래스 규칙

- `animation` 속성을 사용하여 애니메이션을 정의합니다.
- `blink-effect`는 위에서 정의한 키프레임 이름이고, `1s`는 애니메이션의 지속 시간을 나타냅니다.
- `step-end`는 각 키프레임 사이의 전환을 나타내는 함수로, 여기서는 갑자기 변화하는 것을 의미합니다.
- `infinite`는 애니메이션을 무한 반복하도록 설정합니다.
