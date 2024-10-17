# Spring에서의 HTTP 데이터 처리

## 요청 처리

### 컨트롤러 레벨

Spring MVC의 컨트롤러는 클라이언트로부터 들어오는 HTTP 요청을 처리합니다.

#### @RequestMapping 어노테이션

- 특정 URL 패턴에 대한 요청을 처리할 메서드를 지정합니다.
- HTTP 메서드(GET, POST 등)를 명시할 수 있습니다.

#### 파라미터 바인딩

- **@RequestParam:** 쿼리 파라미터나 폼 데이터를 메서드 파라미터에 바인딩합니다.
- **@PathVariable:** URL 경로의 변수 부분을 메서드 파라미터에 바인딩합니다.
- **@RequestBody:** 요청 본문을 객체로 변환하여 메서드 파라미터에 바인딩합니다.

#### 헤더 처리

- **@RequestHeader:** 특정 HTTP 헤더 값을 메서드 파라미터에 바인딩합니다.

#### 서비스 레이어

비즈니스 로직을 처리하며, 컨트롤러로부터 받은 데이터를 가공하거나 저장소와 상호작용합니다.

### 응답 생성

#### ResponseEntity

HTTP 응답의 상태 코드, 헤더, 본문을 세밀하게 제어할 수 있습니다.

```java
@GetMapping("/example")
public ResponseEntity<String> example() {
    return ResponseEntity.ok()
        .header("Custom-Header", "Value")
        .body("Hello, World!");
}
```

#### @ResponseBody

메서드 반환값을 HTTP 응답 본문으로 직접 전송합니다.

```java
@GetMapping("/data")
@ResponseBody
public MyData getData() {
    return new MyData("example");
}
```

### 데이터 변환

#### HttpMessageConverter

요청 본문을 Java 객체로, 또는 Java 객체를 응답 본문으로 변환합니다.

- **JSON 변환:** Jackson 라이브러리를 사용하여 JSON <-> Java 객체 변환
- **XML 변환:** JAXB를 사용하여 XML <-> Java 객체 변환

### 예외 처리

#### @ExceptionHandler

특정 예외가 발생했을 때 처리할 메서드를 지정합니다.

```java
@ExceptionHandler(MyException.class)
public ResponseEntity<String> handleMyException(MyException e) {
    return ResponseEntity.badRequest().body(e.getMessage());
}
```

#### @ControllerAdvice

전역적인 예외 처리 로직을 구현할 수 있습니다.

### 인터셉터와 필터

#### sHandlerInterceptor

컨트롤러 실행 전후에 공통 로직을 수행할 수 있습니다.

#### Filter

서블릿 필터를 사용하여 `요청/응답`을 `전처리/후처리`할 수 있습니다.

#### 로깅

Spring은 `SLF4J`와 `Logback`을 기본 로깅 프레임워크로 사용합니다.
HTTP 요청과 응답을 로깅하여 디버깅과 모니터링에 활용할 수 있습니다.

```java
@Slf4j
@RestController
public class MyController {
    @GetMapping("/log")
    public String logExample() {
        log.info("Received a request to /log");
        return "Logged!";
    }
}
```
