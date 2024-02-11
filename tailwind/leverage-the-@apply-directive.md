# @apply 디렉티브 활용하기

`Tailwind CSS`의 `@apply` 디렉티브는 사용자 정의 클래스나 컴포넌트에서 `Tailwind`의 기본 클래스를 적용할 수 있도록 해줍니다.

&nbsp;

## @apply 디렉티브의 장점

1. **재사용성 향상:** `@apply`를 사용하면 여러 곳에서 동일한 스타일을 쉽게 적용할 수 있습니다.
2. **가독성 향상:** 코드를 읽고 이해하기 쉽도록 스타일을 모듈화하여 관리할 수 있습니다.
3. **유지보수 용이성:** 스타일 변경이 필요한 경우, 한 곳에서만 수정해도 모든 사용처에 적용됩니다.

&nbsp;

## 활용 예시

```css
/* 사용자 정의 클래스에 Tailwind 클래스 적용하기 */
.custom-button {
  @apply bg-blue-500 text-white font-bold py-2 px-4 rounded;
}
```

- `@apply`를 이용하여 사용자 정의 클래스에 `Tailwind CSS`의 클래스를 적용했습니다.

```html
<button class="custom-button">Click me</button>
```

- 이제 `HTML`에서 `.custom-button` 클래스를 사용하면 Tailwind의 스타일이 적용됩니다.

&nbsp;

```css
/* 중첩 클래스에 @apply 디렉티브 사용하기 */
.button {
  @apply font-bold py-2 px-4 rounded;
}

.primary-button {
  @apply bg-blue-500 text-white;
}

.secondary-button {
  @apply bg-gray-300 text-gray-700;
}
```

- `.button` 클래스에 공통 스타일을 정의하고, 이를 `.primary-button` 및 `.secondary-button` 클래스에 적용하고 있습니다.

```html
<button class="button primary-button">Primary Button</button>
<button class="button secondary-button">Secondary Button</button>
```

- 이렇게 하면 .`button` 클래스에 포함된 스타일과 `.primary-button` 또는 .`secondary-button` 클래스에 포함된 스타일이 모두 버튼에 적용됩니다.
