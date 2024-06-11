# JSP 기본 객체

## 1. request 객체

`request` 객체는 HTTP 요청과 관련된 정보를 담고 있습니다. 클라이언트가 서버로 보낸 데이터를 읽어올 때 사용합니다.

### 주요 메서드

- `getParameter(String name)`: 지정된 이름의 요청 파라미터 값을 반환합니다.

- `getAttribute(String name)`: 요청 속성 값을 반환합니다.

- `getHeader(String name)`: 요청 헤더 값을 반환합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<%@ page import="java.util.Enumeration" %>
<html>
<body>
    <h2>Request 객체 예제</h2>
    <p>요청 파라미터: <%= request.getParameter("username") %></p>
    <p>요청 헤더 User-Agent: <%= request.getHeader("User-Agent") %></p>
    <p>모든 요청 파라미터:</p>
    <ul>
        <% 
        Enumeration<String> parameterNames = request.getParameterNames();
        while(parameterNames.hasMoreElements()) {
            String paramName = parameterNames.nextElement();
            out.println("<li>" + paramName + " = " + request.getParameter(paramName) + "</li>");
        }
        %>
    </ul>
</body>
</html>
```

## 2. response 객체

`response` 객체는 서버가 클라이언트에게 응답을 보낼 때 사용합니다. 주로 콘텐츠 타입 설정, 쿠키 추가, 리다이렉트 등에 사용됩니다.

### 주요 메서드

- `setContentType(String type)`: 응답 콘텐츠 타입을 설정합니다.

- `sendRedirect(String location)`: 클라이언트를 다른 URL로 리다이렉트합니다.

- `addCookie(Cookie cookie)`: 쿠키를 응답에 추가합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<html>
<body>
    <h2>Response 객체 예제</h2>
    <% 
    // 쿠키 설정
    Cookie myCookie = new Cookie("username", "JSPUser");
    myCookie.setMaxAge(60*60); // 1시간 유효
    response.addCookie(myCookie);

    // 콘텐츠 타입 설정
    response.setContentType("text/html;charset=UTF-8");
    %>
    <p>쿠키가 설정되었습니다. (username=JSPUser)</p>
    <p>이 페이지의 콘텐츠 타입은: <%= response.getContentType() %></p>
</body>
</html>
```

## 3. session 객체

`session` 객체는 클라이언트별로 고유한 세션을 유지합니다. 로그인 상태 유지, 사용자 설정 정보 저장 등에 유용합니다.

### 주요 메서드

- `getAttribute(String name)`: 세션 속성 값을 반환합니다.

- `setAttribute(String name, Object value)`: 세션 속성을 설정합니다.

- `invalidate()`: 세션을 무효화합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<html>
<body>
    <h2>Session 객체 예제</h2>
    <% 
    // 세션에 속성 설정
    session.setAttribute("username", "JSPUser");
    %>
    <p>세션에 'username'이 설정되었습니다.</p>
    <p>세션에서 가져온 'username': <%= session.getAttribute("username") %></p>
    <% 
    // 세션 무효화
    session.invalidate(); 
    %>
    <p>세션이 무효화되었습니다.</p>
</body>
</html>
```

## 4. application 객체

`application` 객체는 웹 애플리케이션 전체에서 공유되는 정보를 저장합니다. 이는 서버의 모든 사용자가 공유할 수 있는 데이터를 관리할 때 사용합니다.

### 주요 메서드

- `getAttribute(String name)`: 애플리케이션 속성 값을 반환합니다.

- `setAttribute(String name, Object value)`: 애플리케이션 속성을 설정합니다.

- `removeAttribute(String name)`: 애플리케이션 속성을 제거합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<html>
<body>
    <h2>Application 객체 예제</h2>
    <% 
    // 애플리케이션에 속성 설정
    application.setAttribute("visitCount", 1);
    %>
    <p>애플리케이션에 'visitCount'가 설정되었습니다.</p>
    <p>애플리케이션에서 가져온 'visitCount': <%= application.getAttribute("visitCount") %></p>
</body>
</html>
```

## 5. out 객체

`out` 객체는 JSP 페이지에서 클라이언트에게 출력하는 데 사용됩니다. 주로 HTML, 텍스트, 스크립트 등을 출력합니다.

### 주요 메서드

- `print(String s)`: 문자열을 출력합니다.

- `println(String s)`: 문자열을 출력하고 줄 바꿈을 합니다.

- `flush()`: 출력 버퍼를 비웁니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<html>
<body>
    <h2>Out 객체 예제</h2>
    <% 
    out.println("이것은 JSP 페이지에서 출력한 텍스트입니다.");
    out.println("<br>이 텍스트는 줄 바꿈 후에 나옵니다.");
    %>
</body>
</html>
```

## 6. config 객체

`config` 객체는 JSP 페이지와 서블릿 컨테이너 간의 설정 정보를 제공합니다. 주로 초기화 파라미터를 읽는 데 사용됩니다.

### 주요 메서드

- `getInitParameter(String name)`: 초기화 파라미터 값을 반환합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<html>
<body>
    <h2>Config 객체 예제</h2>
    <p>JSP 초기화 파라미터: <%= config.getInitParameter("myParam") %></p>
</body>
</html>
```

## 7. pageContext 객체

`pageContext` 객체는 JSP 페이지의 모든 기본 객체와 다른 정보를 제공하는 범용 객체입니다.

### 주요 메서드

- `getAttribute(String name)`: 지정된 범위의 속성을 반환합니다.

- `setAttribute(String name, Object value)`: 지정된 범위의 속성을 설정합니다.

- `forward(String path)`: 다른 JSP 페이지로 요청을 전달합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" %>
<html>
<body>
    <h2>PageContext 객체 예제</h2>
    <% 
    pageContext.setAttribute("message", "Hello, JSP!", PageContext.PAGE_SCOPE);
    %>
    <p>PageContext에서 가져온 'message': <%= pageContext.getAttribute("message", PageContext.PAGE_SCOPE) %></p>
</body>
</html>
```

## exception 객체

`exception` 객체는 JSP 페이지에서 발생한 예외를 처리하는 데 사용됩니다. 일반적으로 오류 페이지에서 사용됩니다.

### 주요 메서드

- `getMessage()`: 예외 메시지를 반환합니다.

- `printStackTrace()`: 예외 스택 트레이스를 출력합니다.

#### 예제 코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" isErrorPage="true" %>
<html>
<body>
    <h2>Exception 객체 예제</h2>
    <% 
    if(exception != null) {
        out.println("예외 메시지: " + exception.getMessage());
        exception.printStackTrace(out);
    } else {
        out.println("예외가 없습니다.");
    }
    %>
</body>
</html>
```
