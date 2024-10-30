# Request, Model, Session 비교

Spring MVC에서 Request, Model, Session은 각기 다른 범위(scope)와 용도로 데이터를 관리하는 방법으로, 요청별 데이터 전송, 컨트롤러와 뷰 간 데이터 공유, 세션 유지 등에서 사용됩니다.

### Request

- `HttpServletRequest` 객체를 통해 사용.
- 단일 HTTP 요청 내에서만 유효.
- 요청이 완료되면 데이터가 소멸됨.
- 주로 한 번의 요청-응답 사이클에서 데이터를 전달할 때 사용.

```java
@GetMapping("/example")
public String example(HttpServletRequest request) {
    request.setAttribute("data", "value");
    return "view";
}
```

### Model

- Spring MVC에서 제공하는 인터페이스.
- 컨트롤러에서 뷰로 데이터를 전달하는 용도.
- Request 스코프와 유사하게 동작하지만 더 추상화된 방식.
- 내부적으로 `HttpServletRequest`에 데이터를 저장.

```java
@GetMapping("/example")
public String example(Model model) {
    model.addAttribute("data", "value");
    return "view";
}
```

### Session

- `HttpSession` 객체를 통해 사용.
- 여러 요청에 걸쳐 데이터를 유지.
- 브라우저 세션이 유지되는 동안 데이터 보존.
- 로그인 정보 등 장기간 유지해야 하는 데이터에 적합.

```java
@GetMapping("/example")
public String example(HttpSession session) {
    session.setAttribute("user", userObject);
    return "view";
}
```

### 주요 차이점

#### 1. 데이터 유지 기간

- **Request, Model:** 단일 요청-응답 사이클
- **Session:** 여러 요청에 걸쳐 유지

#### 2. 사용 목적

- **Request, Model:** 일회성 데이터 전달
- **Session:** 지속적인 데이터 유지

#### 3. 메모리 사용

- **Request, Model:** 요청 완료 후 메모리에서 제거
- **Session:** 세션이 유지되는 동안 서버 메모리 사용

#### 4. 보안

- **Request, Model:** 단일 요청 내에서만 접근 가능
- **Session:** 여러 요청에서 접근 가능, 보안에 더 주의 필요

#### 5. 사용 편의성

- **Model:** Spring MVC에 최적화된 인터페이스로 사용이 간편
- **Request, Session:** 서블릿 API를 직접 다루어야 함

#### 적절한 사용

- **일회성 데이터 전달:** Model 사용
- **복잡한 요청 처리:** Request 사용
- **사용자별 지속 데이터:** Session 사용
