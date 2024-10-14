# 스프링 Model이란

스프링 MVC의 `Model`은 컨트롤러와 뷰 사이에서 데이터를 전달하는 중요한 역할을 합니다.

### Model의 개념

- Model은 `key-value` 쌍으로 이루어진 `HashMap` 형태의 객체입니다.
- 컨트롤러에서 뷰로 데이터를 전달하는 데 사용됩니다.
- `Servlet`의 `request.setAttribute()`와 유사한 역할을 합니다.

### Model 사용 방법

#### 컨트롤러에서 Model 사용

컨트롤러 메서드의 파라미터로 Model 객체를 선언하면 스프링이 자동으로 Model 객체를 생성해 주입합니다.
`addAttribute()` 메서드를 사용해 데이터를 추가합니다:

```java
@GetMapping("/example")
public String exampleMethod(Model model) {
    model.addAttribute("message", "Hello World");
    return "exampleView";
}
```

#### 뷰에서 Model 데이터 접근

JSP에서는 `${key}` 형식으로 Model에 저장된 데이터에 접근할 수 있습니다.

```html
<h1>${message}</h1>
```

### @ModelAttribute 어노테이션

- 파라미터를 자동으로 Model에 추가할 때 사용합니다.
- 객체나 기본 타입 변수에 사용 가능합니다.

```java
@GetMapping("/test")
public String test(@ModelAttribute("number") int number) {
    return "testPage";
}
```

### Model의 특징

- Java Beans 규칙을 따르는 객체는 자동으로 Model에 추가되어 뷰로 전달됩니다.
- 기본 자료형은 자동으로 전달되지 않으므로 `@ModelAttribute` 어노테이션을 사용하거나 명시적으로 Model에 추가해야 합니다.

#### Model vs ModelAndView

- `Model`은 데이터만 저장하는 반면, `ModelAndView`는 데이터와 뷰 이름을 함께 저장할 수 있습니다.

#### 주의사항

- Model은 요청 스코프(`request scope`)에 저장되므로, 해당 요청-응답 주기 내에서만 유효합니다.
- 대량의 데이터나 복잡한 객체를 Model에 저장할 때는 성능에 주의해야 합니다.

스프링의 Model 객체를 효과적으로 사용하면 컨트롤러와 뷰 사이의 데이터 전달을 간편하고 깔끔하게 처리할 수 있습니다.
