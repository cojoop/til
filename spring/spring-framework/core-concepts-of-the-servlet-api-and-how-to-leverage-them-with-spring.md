# 서블릿 API의 핵심 개념과 스프링에서의 활용

서블릿 API에서 세션(`Session`), 쿠키(`Cookie`), 필터(`Filter`), 리스너(`Listener`)는 웹 애플리케이션의 핵심 개념으로, 웹 애플리케이션의 상태 관리, 요청 처리, 그리고 이벤트 감시를 위해 사용됩니다.

## 세션(Session)

세션은 서버가 클라이언트의 상태를 유지하기 위한 방법입니다. 클라이언트가 서버에 접속할 때마다 서버는 각 클라이언트마다 고유한 세션 ID를 부여하고, 이 세션 ID를 기반으로 서버에 저장된 클라이언트의 데이터를 참조합니다.

#### 동작 방식

- 클라이언트가 서버에 접속하면 서버는 고유한 세션 ID를 생성하여 클라이언트에게 전달합니다.
- 클라이언트는 이 세션 ID를 쿠키 또는 URL 파라미터로 서버에 다시 전달하며, 서버는 세션 ID를 확인하여 클라이언트에 맞는 데이터를 조회합니다

#### 사용 예시

- 로그인 상태 유지
- 장바구니 기능 등

### 스프링에서의 사용

스프링에서는 `HttpSession`을 통해 세션을 쉽게 사용할 수 있습니다. 세션에 값을 저장하거나 읽을 때 `@SessionAttribute` 또는 `HttpSession` 객체를 사용합니다.

```java
// 세션 값 저장
session.setAttribute("user", user);

// 세션 값 가져오기
User user = (User) session.getAttribute("user");
```

스프링 MVC에서는 **@SessionAttributes**를 사용하여 특정 모델 객체를 세션에 자동으로 저장할 수도 있습니다.

```java
@Controller
@SessionAttributes("user")
public class UserController {
    @GetMapping("/user")
    public String getUser(Model model) {
        model.addAttribute("user", new User());
        return "user";
    }
}
```

## 쿠키(Cookie)

쿠키는 클라이언트에 저장되는 작은 데이터 파일로, 서버가 클라이언트의 정보를 저장할 수 있도록 하는 방법입니다. 서버는 클라이언트가 쿠키를 통해 전달한 데이터를 활용하여 클라이언트의 상태를 추적할 수 있습니다.

#### 동작 방식

서버가 클라이언트에게 쿠키를 전송하면 클라이언트는 이를 저장하고, 이후 요청마다 서버에 쿠키를 다시 전송합니다.
이를 통해 서버는 클라이언트가 누구인지 식별할 수 있습니다.

#### 사용 예시

- 자동 로그인
- 사용자 맞춤형 설정 등

### 스프링에서의 사용

스프링에서는 `@CookieValue` 어노테이션을 사용하여 컨트롤러에서 쿠키 값을 직접 받을 수 있습니다.

```java
@GetMapping("/welcome")
public String welcome(@CookieValue(value = "username", defaultValue = "Guest") String username) {
    return "Welcome, " + username;
}
```

쿠키를 생성하고 설정할 때는 `HttpServletResponse`를 사용합니다.

```java
Cookie cookie = new Cookie("username", "john");
cookie.setMaxAge(7 * 24 * 60 * 60);  // 쿠키 유효기간 7일
response.addCookie(cookie);
```

## 필터(Filter)

필터는 서블릿이 처리하기 전 또는 후에 요청과 응답을 가로채서 처리하는 역할을 합니다. 필터는 주로 요청이나 응답을 변환하거나 인증, 로깅, 권한 관리 등의 기능을 수행합니다.

#### 동작 방식

클라이언트 요청이 서블릿에 도달하기 전에 필터가 이를 가로채서 필요한 작업을 수행하고, 그 후 서블릿으로 요청을 전달합니다.
응답이 클라이언트로 전달되기 전에 필터가 다시 한번 가로채서 작업을 수행할 수 있습니다.

#### 사용 예시

- 요청 인증
- 인코딩 설정
- 요청 로깅 등

### 스프링에서의 사용

스프링에서는 `OncePerRequestFilter`를 상속받아 필터를 구현할 수 있습니다. 스프링 부트에서는 `FilterRegistrationBean`을 사용하여 필터를 등록할 수 있습니다.

```java
@Component
public class MyFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) 
            throws ServletException, IOException {
        // 필터 처리 로직
        filterChain.doFilter(request, response); // 다음 필터나 서블릿으로 요청 전달
    }
}
```

## 리스너(Listener)

리스너는 특정 이벤트가 발생할 때 이를 감지하고 처리할 수 있는 객체입니다. 서블릿에서는 주로 세션, 애플리케이션 컨텍스트 등의 상태 변화를 감지하는데 사용됩니다.

#### 동작 방식

리스너는 서버의 특정 이벤트(`ex. 세션 생성, 소멸, 애플리케이션 시작, 종료 등`)를 감지하고, 그에 따라 자동으로 동작하는 콜백 메서드를 정의합니다.

#### 사용 예시

- 세션 수명 주기 관리
- 애플리케이션 초기화 작업 등

### 스프링에서의 사용

스프링에서는 리스너로 `@EventListener` 어노테이션을 사용하여 이벤트 처리를 할 수 있습니다. 특정 이벤트를 감지하고 그에 맞는 로직을 실행할 수 있습니다.

```java
@Component
public class MyEventListener {
    @EventListener
    public void handleContextRefresh(ContextRefreshedEvent event) {
        // 애플리케이션 초기화 시 실행할 로직
    }
}
```

> 또한, 스프링 부트는 기본적으로 많은 서블릿 리스너를 자동으로 등록하고 관리하기 때문에 추가적인 설정 없이 리스너 기능을 사용할 수 있습니다.
