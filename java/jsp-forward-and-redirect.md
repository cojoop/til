# JSP의 forward와 redirect

JSP(`JavaServer Pages`)에서의 페이지 이동 방식인 `forward`와 `redirect`는 각각의 목적과 사용 방법이 다른 중요한 기능입니다.

## forward와 redirect의 개념

### forward란

`forward`는 서버 내부에서 요청을 다른 JSP 페이지나 서블릿으로 전달하는 방법입니다. 이 과정에서 클라이언트는 URL의 변화를 인식하지 못합니다. 서버가 요청을 다른 자원으로 전달하고 그 자원에서 처리가 완료되면 클라이언트에게 응답이 전달됩니다.

#### 특징

- 클라이언트의 URL이 변경되지 않음.

- 서버 내부에서만 동작.

- 같은 요청과 응답 객체를 공유.

- 빠른 처리 속도.

### redirect란

`redirect`는 서버가 클라이언트에게 새로운 URL로 이동하도록 지시하는 방법입니다. 서버는 클라이언트에게 `HTTP 302` 상태 코드와 새로운 URL을 보내고, 클라이언트는 해당 URL로 새로운 요청을 보냅니다. 클라이언트의 브라우저는 URL이 변경된 것을 인식합니다.

#### 특징

- 클라이언트의 URL이 변경됨.

- 클라이언트 측에서 새로운 요청이 발생.

- 새로운 요청과 응답 객체를 사용.

- 비교적 느린 처리 속도(클라이언트와의 추가 통신 필요).

## forward와 redirect의 차이점

특징|forward|redirect
----|----|----
URL 변경 여부|클라이언트에게 URL이 변경되지 않음|클라이언트에게 URL이 변경됨
요청 처리 위치|서버 내부에서 처리|클라이언트 측에서 새로운 요청 처리
처리 속도|빠름|느림 (클라이언트-서버 간 추가 통신 필요)
요청/응답 객체|동일한 객체를 사용|새로운 객체가 생성
상태 유지|상태 정보가 그대로 유지됨|새로운 요청으로 상태가 초기화됨
주로 사용되는 경우|내부 페이지 이동, 데이터를 유지한 채로 페이지 이동|외부 페이지로 이동, URL 변경이 필요한 경우

## forward와 redirect 사용 예제

### forward 예제: 로그인 후 사용자 정보를 프로필 페이지로 전달

사용자가 로그인 폼을 제출한 후, 서버는 자격 증명을 확인하고 프로필 페이지로 요청을 전달합니다. 이때 `forward`를 사용하여 서버 내부에서 요청을 전달합니다.

#### 예제 코드

```java
// LoginServlet.java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;

public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        
        if (isValidUser(username, password)) {
            // 유효한 사용자일 경우 profile.jsp로 forward
            RequestDispatcher dispatcher = request.getRequestDispatcher("profile.jsp");
            request.setAttribute("username", username);
            dispatcher.forward(request, response);
        } else {
            // 유효하지 않은 경우 로그인 페이지로 리다이렉트
            response.sendRedirect("login.jsp?error=1");
        }
    }
    
    private boolean isValidUser(String username, String password) {
        // 사용자 검증 로직 (예: 데이터베이스 확인)
        return "admin".equals(username) && "password".equals(password);
    }
}
```

- 사용자가 로그인 정보를 제출하면 자격 증명을 확인하고, 성공 시 `profile.jsp`로 요청을 전달합니다.

```html
<!-- profile.jsp -->
<%@ page contentType="text/html; charset=UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>Profile</title>
</head>
<body>
    <h1>Welcome, <%= request.getAttribute("username") %>!</h1>
</body>
</html>
```

- 전달된 요청 객체에서 사용자 정보를 받아 표시합니다.

> 위 코드에서 `RequestDispatcher`를 사용하여 로그인 검증이 성공한 후 `profile.jsp`로 요청을 전달합니다. 이때 클라이언트는 `login.jsp` URL에 남아 있으며, 브라우저 URL은 변경되지 않습니다.

### redirect 예제: 로그인 성공 후 대시보드 페이지로 이동

로그인 성공 후 사용자를 대시보드 페이지로 리다이렉트합니다. 이때 `redirect`를 사용하여 클라이언트가 새로운 URL로 이동하도록 합니다.

#### 예제 코드

```java
// LoginServlet.java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;

public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        
        if (isValidUser(username, password)) {
            // 유효한 사용자일 경우 대시보드 페이지로 리다이렉트
            response.sendRedirect("dashboard.jsp");
        } else {
            // 유효하지 않은 경우 로그인 페이지로 리다이렉트
            response.sendRedirect("login.jsp?error=1");
        }
    }
    
    private boolean isValidUser(String username, String password) {
        // 사용자 검증 로직 (예: 데이터베이스 확인)
        return "admin".equals(username) && "password".equals(password);
    }
}
```

- 사용자가 로그인 정보를 제출하면 자격 증명을 확인하고, 성공 시 `dashboard.jsp`로 리다이렉트합니다.

> 위 코드에서 `response.sendRedirect("dashboard.jsp");`를 사용하여 로그인 검증이 성공한 후 클라이언트가 `dashboard.jsp`로 이동하도록 합니다. 이때 클라이언트의 브라우저 URL이 변경됩니다.

### 언제 forward와 redirect를 사용해야 하는지

#### forward를 사용해야 하는 경우

- **내부 자원 간 이동**: 동일한 웹 애플리케이션 내에서 요청을 처리하고 결과를 전달할 때 유용합니다. 예를 들어, 로그인 검증 후 동일한 요청 객체를 사용하여 사용자 정보를 다른 JSP 페이지로 전달할 때 적합합니다.

- **상태 정보 유지**: 같은 요청 객체와 응답 객체를 유지하면서 다른 자원으로 이동해야 할 때 사용합니다.

- **빠른 처리 필요**: 서버 내부에서 처리되기 때문에 빠르게 요청을 전달할 수 있습니다.

#### redirect를 사용해야 하는 경우

- **외부 페이지로 이동**: 다른 도메인이나 웹 애플리케이션으로 이동할 때 사용합니다. 예를 들어, 사용자가 로그인 후 외부 사이트로 이동해야 할 때 적합합니다.

- **URL 변경 필요**: 클라이언트가 URL 변경을 인식해야 하는 경우에 사용합니다. 예를 들어, 로그인 후 대시보드 페이지로 이동할 때 클라이언트가 URL 변경을 확인해야 할 경우 유용합니다.

- **데이터 변경 후 페이지 갱신**: 데이터베이스나 서버 상태가 변경된 후, 새로 고침을 통한 데이터 중복 전송을 방지하기 위해 사용합니다. 예를 들어, 폼 제출 후 페이지를 다시 로드할 때 중복 제출을 방지할 수 있습니다.
