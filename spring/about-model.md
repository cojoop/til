# Model이란

Spring에서 Model은 MVC(`Model-View-Controller`) 패턴에서 데이터를 전달하고 관리하는 중요한 구성 요소로, 주로 도메인 객체, 데이터베이스에서 가져온 데이터, 폼 데이터를 처리한 결과 등을 포함합니다.
컨트롤러와 뷰 사이에서 데이터를 전달하는 매개체 역할을 하며, 데이터의 상태와 비즈니스 로직을 처리합니다.

## Spring MVC에서의 모델 구성

Spring MVC에서는 컨트롤러 메서드에서 데이터를 뷰로 전달하기 위해 `Model`, `ModelMap`, 또는 `ModelAndView` 객체를 사용합니다.

### Model

- Spring에서는 Model 인터페이스를 제공하여, 데이터를 뷰로 전달하기 위해 사용되며, `model.addAttribute()`로 데이터를 설정합니다.
- Model은 기본적으로 `key-value` 형태로 데이터를 저장하며, 이 데이터는 뷰에서 렌더링될 때 사용됩니다.

#### 예제 코드

```java
@Controller
public class MyController {
    @GetMapping("/hello")
    public String hello(Model model) {
        model.addAttribute("message", "Hello, Spring!");
        return "greeting";
    }
}
```

### ModelMap

- ModelMap은 `Model`의 변형으로, `HashMap`을 상속받아 좀 더 유연한 데이터를 처리하는 데 사용됩니다.

- 데이터를 `Map` 형태로 처리할 수 있는 기능이 필요할 때 유용합니다.

```java
@Controller
public class MyController {
    @GetMapping("/product")
    public String getProductInfo(ModelMap modelMap) {
        Product product = new Product("Laptop", 1200.00);
        modelMap.addAttribute("product", product);
        return "productDetail";
    }
}
```

### ModelAndView

- ModelAndView는 모델 데이터와 뷰 정보를 함께 처리할 수 있는 클래스입니다.
- 이를 통해 모델과 뷰 정보를 명시적으로 한 번에 설정할 수 있습니다.

```java
@Controller
public class MyController {
    @GetMapping("/profile")
    public ModelAndView getProfile() {
        ModelAndView mav = new ModelAndView("profileView");  // 뷰 이름 설정
        mav.addObject("username", "JohnDoe");  // 모델 데이터 설정
        return mav;
    }
}
```

## @ModelAttribute 어노테이션

`@ModelAttribute`는 컨트롤러의 메서드 파라미터나 리턴값에 적용되어, 모델 데이터를 자동으로 추가하거나 폼 데이터를 바인딩하는 데 사용됩니다.

### 메서드 수준에서의 @ModelAttribute

- `@ModelAttribute` 어노테이션을 사용하면, 특정 데이터를 모든 뷰에 공통적으로 전달할 수 있습니다.
- 이는 매번 컨트롤러에서 동일한 데이터를 전달할 필요 없이 자동으로 모델에 추가하는 방식입니다.

```java
@Controller
public class MyController {
    @ModelAttribute("greetingMessage")
    public String greetingMessage() {
        return "Welcome to our site!";
    }

    @GetMapping("/home")
    public String home() {
        return "home";
    }
}
```

- 이 경우 `greetingMessage`는 `home`뷰 뿐만 아니라 다른 뷰에서도 사용할 수 있습니다.

### 폼 데이터 바인딩

- `@ModelAttribute`는 폼 데이터를 특정 객체에 자동으로 바인딩하는 기능도 제공합니다.
ex. HTML 폼에서 입력된 데이터를 `@ModelAttribute`를 통해 도메인 객체로 바인딩할 수 있습니다.

```java
@Controller
public class UserController {

    @GetMapping("/signup")
    public String showSignupForm(Model model) {
        model.addAttribute("user", new User());
        return "signupForm";
    }

    @PostMapping("/signup")
    public String submitSignupForm(@ModelAttribute User user) {
        // 바인딩된 User 객체를 처리
        System.out.println("User name: " + user.getName());
        return "signupSuccess";
    }
}
```

- 폼 데이터를 `User` 객체로 자동 바인딩하여 컨트롤러 메서드에서 처리할 수 있게 합니다.

### Model의 역할

모델은 단순히 데이터 전달 역할을 넘어, 애플리케이션의 비즈니스 로직을 반영하는 중요한 역할을 담당합니다.

#### 도메인 객체와의 연결

- 모델은 주로 서비스 계층에서 처리된 도메인 객체를 뷰에 전달하는 데 사용됩니다.
ex. 데이터베이스에서 조회한 고객 정보, 상품 리스트, 주문 내역 등을 컨트롤러에서 모델에 담아 뷰로 넘겨줍니다.

#### 뷰와 데이터 통신

- Spring의 모델은 컨트롤러와 뷰 사이에서 데이터를 안전하게 전달하는 역할을 합니다.
- 특히 Spring의 Model은 뷰에서 직접 사용할 수 있는 데이터를 설정하여 템플릿 엔진(`Thymeleaf, JSP 등`)에서 이를 손쉽게 렌더링할 수 있게 합니다.

#### REST API와 JSON

- Spring에서는 `@ResponseBody` 또는 `RestController`를 사용하여 모델 데이터를 JSON 형식으로 응답할 수 있습니다.
- `REST API`에서는 모델을 활용해 다양한 비즈니스 로직을 처리하고 이를 API 응답으로 제공하는 방식이 일반적입니다.

```java
@RestController
public class ApiController {

    @GetMapping("/api/user")
    public User getUser() {
        return new User("John", "Doe");
    }
}
```

#### 폼 바인딩과 데이터 검증

- Spring MVC에서는 모델을 사용하여 폼 데이터를 객체로 바인딩하고, 이를 검증(`Validation`)할 수 있습니다.
- `@Valid` 어노테이션을 사용하여 자동 검증을 할 수 있고, 검증 결과를 `BindingResult` 객체로 받아 처리합니다.

```java
@Controller
public class UserController {

    @PostMapping("/register")
    public String registerUser(@Valid @ModelAttribute User user, BindingResult result) {
        if (result.hasErrors()) {
            return "registerForm";
        }
        // 등록 로직
        return "registrationSuccess";
    }
}
```
