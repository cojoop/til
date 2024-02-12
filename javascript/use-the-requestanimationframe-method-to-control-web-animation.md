# requestAnimationFrame 메서드로 웹 애니메이션 제어하기

웹 브라우저에서 애니메이션을 제어하는 방법 중 하나로 `requestAnimationFrame` 메서드가 있습니다. `requestAnimationFrame`은 브라우저에게 다음 번 리페인트가 발생하기 직전에 수행할 콜백 함수를 지정합니다. 이를 통해 브라우저는 최적의 시기에 애니메이션을 업데이트할 수 있습니다.
> 이 메서드는 브라우저의 최적화된 애니메이션 루프를 활용하여, 부드럽고 효율적인 애니메이션을 구현할 수 있게 도와줍니다.

&nbsp;

## 장점

#### 1. 자동 최적화

`requestAnimationFrame`은 브라우저의 내부 애니메이션 타이머와 연동되어 있어, 사용자의 환경에 따라 최적화된 애니메이션 루프를 제공합니다. 이를 통해 브라우저는 현재 시스템 상태에 맞게 애니메이션을 제어하고 성능을 향상시킵니다.

#### 2. 배터리 수명 절약

일반적으로 `setTimeout`이나 `setInterval`을 사용하여 애니메이션을 구현하면, 브라우저는 애니메이션 프레임을 계속해서 처리해야 하므로 배터리 수명이 저하될 수 있습니다. 그러나 `requestAnimationFrame`은 브라우저가 활성화된 탭만 업데이트하므로 배터리 수명을 절약할 수 있습니다.

#### 3. 다양한 장치와 브라우저 호환성

`requestAnimationFrame`은 대부분의 최신 브라우저에서 지원되며, 모바일 장치와 데스크톱 브라우저에서 일관되게 동작합니다. 이는 다양한 플랫폼에서 일관된 사용자 경험을 제공하는 데 도움이 됩니다.

&nbsp;

## 사용법 및 예제

```js
function animate() {
    // 애니메이션 업데이트 로직을 작성합니다.
    // ex) 객체의 위치를 변경하거나 스타일을 조절합니다.

    // 다음 프레임에 애니메이션을 업데이트하도록 요청합니다.
    requestAnimationFrame(animate);
}

// 애니메이션을 시작합니다.
animate();
```

- `requestAnimationFrame`을 호출하여 브라우저에 다음 프레임을 그릴 때 `animate` 함수가 호출되도록 합니다.

&nbsp;

```js
// 공을 움직이는 애니메이션
function animate() {
    positionX += speedX;
    positionY += speedY;

    if (positionX <= 0 || positionX >= containerWidth - ball.offsetWidth) {
        speedX = -speedX;
    }
    if (positionY <= 0 || positionY >= containerHeight - ball.offsetHeight) {
        speedY = -speedY;
    }

    ball.style.left = positionX + 'px';
    ball.style.top = positionY + 'px';

    requestAnimationFrame(animate);
}
```
