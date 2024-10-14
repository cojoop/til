# Servlet API의 핵심 개념(세션, 쿠키, 필터, 리스터)와 스프링에서의 활용

Servlet API에서 세션(`Session`), 쿠키(`Cookie`), 필터(`Filter`), 리스너(`Listener`)는 웹 애플리케이션의 핵심 개념으로, 웹 애플리케이션의 상태 관리, 요청 처리, 그리고 이벤트 감시를 위해 사용됩니다.

## 세션 (Session)

세션은 웹 애플리케이션에서 클라이언트와 서버 간의 상태를 유지하기 위한 메커니즘입니다.

### 특징

- 서버 측에 저장되는 데이터 구조
- 각 클라이언트마다 고유한 세션 ID 할당
- 일정 시간 동안 유지되며, 타임아웃 후 소멸

### 스프링에서의 활용

- `@SessionAttributes` 어노테이션을 사용하여 컨트롤러 레벨에서 세션 데이터 관리
- `HttpSession` 객체를 통해 세션 데이터에 직접 접근 가능

```java
@Controller
@SessionAttributes("user")
public class UserController {
    @GetMapping("/login")
    public String login(Model model) {
        model.addAttribute("user", new User());
        return "loginForm";
    }
}
```

## 쿠키 (Cookie)

쿠키는 클라이언트 측에 저장되는 작은 데이터 조각입니다.

### 특징

- 클라이언트 브라우저에 저장
- `key-value` 쌍으로 구성
- 만료 기간 설정 가능

### 스프링에서의 활용

- `@CookieValue` 어노테이션을 사용하여 쿠키 값을 메서드 파라미터로 주입
- `HttpServletResponse`를 통해 쿠키 생성 및 전송

```java
@GetMapping("/welcome")
public String welcome(@CookieValue(value = "name", defaultValue = "Guest") String name, Model model) {
    model.addAttribute("name", name);
    return "welcome";
}
```

## 필터 (Filter)

필터는 HTTP 요청과 응답을 가로채어 처리하는 컴포넌트입니다.

### 특징

- 서블릿 컨테이너에서 동작
- 요청이 서블릿에 도달하기 전에 실행
- 여러 필터를 체인으로 구성 가능

### 스프링에서의 활용

- `@Component` 어노테이션과 함께 `Filter` 인터페이스 구현
- `FilterRegistrationBean`을 사용하여 필터 등록 및 순서 지정

```java
@Component
public class LogFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) 
            throws IOException, ServletException {
        chain.doFilter(request, response);
    }
}
```

## 리스너 (Listener)

리스너는 특정 이벤트가 발생했을 때 실행되는 컴포넌트입니다.

### 특징

- 애플리케이션, 세션, 요청 수준의 이벤트 감지
- 비동기적으로 동작

### 스프링에서의 활용

- `@WebListener` 어노테이션을 사용하여 리스너 등록
- 스프링의 이벤트 리스너 메커니즘과 통합 가능

```java
@WebListener
public class SessionListener implements HttpSessionListener {
    @Override
    public void sessionCreated(HttpSessionEvent se) {
        System.out.println("Session created: " + se.getSession().getId());
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent se) {
        System.out.println("Session destroyed: " + se.getSession().getId());
    }
}
```

### 스프링에서의 추가적인 활용

스프링은 서블릿 API의 개념을 확장하고 추상화하여 더 편리한 기능을 제공합니다.

- **인터셉터 (Interceptor):** 필터와 유사하지만 스프링 컨텍스트 내에서 동작하며, 더 세밀한 제어가 가능합니다.
- **핸들러 (Handler):** 요청을 처리하는 메서드나 클래스를 추상화한 개념으로, 컨트롤러의 메서드가 여기에 해당합니다.
- **뷰 리졸버 (View Resolver):** 컨트롤러가 반환한 뷰 이름을 실제 뷰 객체로 변환합니다.
