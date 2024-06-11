# JSP 파일이 처리되는 과정(라이프사이클)

JSP 파일이 처리되는 과정은 여러 단계로 나뉘며, 이를 JSP의 라이프사이클이라고 부릅니다. JSP 라이프사이클은 다음과 같은 단계로 구성됩니다.

1. 번역(`Translation`) 단계

2. 컴파일(`Compilation`) 단계

3. 로딩 및 초기화(`Loading and Initialization`) 단계

4. 요청 처리(`Request Processing`) 단계

5. 종료(`Destroy`) 단계

### 1. 번역(Translation) 단계

JSP 파일이 클라이언트로부터 처음 요청될 때, 웹 컨테이너(예: `Apache Tomcat`)는 JSP 파일을 서블릿 자바 파일(`.java`)로 변환합니다. 이 단계에서 JSP 태그와 Java 코드는 서블릿 코드로 변환됩니다.

##### 예제코드

```java
// hello.jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>Hello JSP</title>
</head>
<body>
    <h1>Hello, <%= request.getParameter("name") %>!</h1>
</body>
</html>
```

```java
// Servlet 코드로 변환
public class hello_jsp extends HttpJspBase {
    public void _jspService(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
        response.setContentType("text/html;charset=UTF-8");
        JspWriter out = response.getWriter();
        try {
            out.write("<!DOCTYPE html>\n");
            out.write("<html>\n");
            out.write("<head>\n");
            out.write("    <title>Hello JSP</title>\n");
            out.write("</head>\n");
            out.write("<body>\n");
            out.write("    <h1>Hello, ");
            out.write(request.getParameter("name"));
            out.write("!</h1>\n");
            out.write("</body>\n");
            out.write("</html>\n");
        } finally {
            out.close();
        }
    }
}
```

### 2. 컴파일(Compilation) 단계

번역된 `Servlet` 자바 파일은 자바 컴파일러에 의해 컴파일되어 `.class` 파일로 변환됩니다. 이 단계에서는 자바 코드가 `JVM`에서 실행 가능한 바이트코드로 변환됩니다.

### 3. 로딩 및 초기화(Loading and Initialization) 단계

컴파일된 `Servlet` 클래스 파일은 웹 컨테이너에 의해 메모리에 로드되고 초기화됩니다. 초기화 단계에서는 `jspInit()` 메서드가 호출되어 JSP 페이지의 초기 설정 작업을 수행합니다.

```java
public class hello_jsp extends HttpJspBase {
    public void jspInit() {
        // 초기화 작업
    }
    ...
}
```

### 4. 요청 처리(Request Processing) 단계

JSP 페이지가 초기화된 후, 클라이언트의 요청이 들어오면 `_jspService()` 메서드가 호출되어 요청을 처리합니다. 이 메서드는 각 요청마다 호출되며, 클라이언트의 요청을 처리하고 응답을 생성합니다.

```java
public void _jspService(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
    // 요청 처리 로직
}
```

### 5. 종료(Destroy) 단계

JSP 페이지가 더 이상 필요 없게 되면, 웹 컨테이너는 `jspDestroy()` 메서드를 호출하여 JSP 페이지를 종료합니다. 이 단계에서는 JSP 페이지에서 사용된 리소스를 해제하는 작업이 수행됩니다.

```java
public class hello_jsp extends HttpJspBase {
    public void jspDestroy() {
        // 리소스 해제 작업
    }
    ...
}
```

## JSP 파일이 처리되는 상황별 라이프사이클

### 1. 톰캣에 JSP의 서블릿 객체가 없는 상태

#### 초기 요청(서블릿 객체가 없는 상태)

1. 번역 단계 (`Translation`):

    - 클라이언트가 JSP 파일을 처음 요청하면 톰캣 서버는 JSP 파일을 서블릿 자바 파일로 변환합니다.

2. 컴파일 단계 (`Compilation`):

    - 변환된 서블릿 자바 파일은 자바 컴파일러에 의해 컴파일됩니다. 이로 인해 `.class` 파일이 생성됩니다.

3. 로딩 및 초기화 단계 (`Loading and Initialization`):

    - 컴파일된 서블릿 클래스 파일이 톰캣 서버에 의해 메모리에 로드됩니다. 초기화 작업이 수행되며 `jspInit()` 메서드가 호출됩니다.

4. 요청 처리 단계 (`Request Processing`):

    - 클라이언트의 요청이 들어오면 톰캣은 `_jspService()` 메서드를 호출하여 요청을 처리하고 응답을 생성합니다.

5. 종료 단계 (`Destroy`):

    - 서블릿 객체가 더 이상 필요 없게 되면 `jspDestroy()` 메서드가 호출되어 리소스를 해제합니다.

### 2. 톰캣에 JSP의 서블릿 객체가 있는 상태

#### 이후 요청 (서블릿 객체가 이미 존재하는 상태)

1. 번역 단계 생략:

    - 이미 서블릿 자바 파일이 존재하므로 번역 단계는

2. 컴파일 단계 생략:

    - 이미 서블릿 클래스 파일이 존재하므로 컴파일 단계도 생략됩니다.

3. 로딩 및 초기화 생략 (이미 로드된 상태):

    - 서블릿 객체가 이미 메모리에 로드되고 초기화된 상태라면 이 단계도 생략됩니다.

4. 요청 처리 단계 (`Request Processing`):

    - 클라이언트의 요청이 들어오면 톰캣은 `_jspService()`메서드를 호출하여 요청을 처리하고 응답을 생성합니다.

### 3. 톰캣에 의해 모든 서블릿 객체가 언로드된 후

#### 서버 재시작 또는 서블릿 언로드 후 요청

1. 번역 단계 생략:

    - 기존에 번역된 서블릿 자바 파일이 존재하므로 번역 단계는 생략됩니다.

2. 컴파일 단계 생략:

    - 기존에 컴파일된 서블릿 클래스 파일이 존재하므로 컴파일 단계도 생략됩니다.

3. 로딩 및 초기화 단계 (다시 로드):

    - 서버 재시작 후 처음 요청 시, 서블릿 클래스 파일이 다시 메모리에 로드되고 초기화됩니다. `jspInit()` 메서드가 호출되어 초기화 작업이 수행됩니다.

4. 요청 처리 단계 (`Request Processing`):

    - 초기화가 완료된 후 톰캣은 `_jspService()` 메서드를 호출하여 클라이언트의 요청을 처리하고 응답을 생성합니다.

### 4. 서버에서 JSP 파일이 수정된 후

#### JSP 파일 수정 후 첫 요청

1. 번역 단계 (`Re-Translation`):

    - JSP 파일이 수정된 것을 톰캣이 감지하면 기존의 서블릿 자바 파일을 삭제하고 새로운 JSP 파일로 대체하여 다시 번역합니다.

2. 컴파일 단계 (`Re-Compilation`):

    - 수정된 서블릿 자바 파일이 다시 컴파일됩니다.

3. 로딩 및 초기화 단계 (`Re-Initialization`):

    - 수정된 서블릿 클래스 파일이 메모리에 로드되고 초기화됩니다. 기존의 서블릿 객체는 언로드되고 새로운 서블릿 객체가 생성됩니다. `jspInit()` 메서드가 호출되어 초기화 작업이 수행됩니다.

4. 요청 처리 단계 (`Request Processing`):

    - 초기화가 완료된 후 톰캣은 `_jspService()` 메서드를 호출하여 클라이언트의 요청을 처리하고 응답을 생성합니다.

5. 종료 단계 (`Destroy`):

    - 수정 전의 서블릿 객체가 언로드될 때 `jspDestroy()` 메서드가 호출되어 리소스를 해제합니다.
