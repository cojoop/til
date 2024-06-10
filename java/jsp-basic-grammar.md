# JSP 기본 문법

## 1. JSP 스크립틀릿 (Scriptlets)

스크립틀릿은 `JSP` 페이지 내에 `Java` 코드를 삽입하는 가장 기본적인 방법입니다. 스크립틀릿은 `<%`와 `%>` 사이에 `Java` 코드를 작성합니다.

#### 예제코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>JSP 스크립틀릿 예제</title>
</head>
<body>
    <h1>현재 시간:</h1>
    <%
        java.util.Date date = new java.util.Date();
        out.println(date.toString());
    %>
</body>
</html>
```

- `<% %>`: 이 안에 작성된 코드는 `Java` 코드로 실행됩니다.

- `java.util.Date date = new java.util.Date();`: 현재 날짜와 시간을 얻기 위한 Date 객체 생성.

- `out.println(date.toString());`: 현재 날짜와 시간을 출력합니다.

## 2. JSP 표현식 (Expressions)

JSP 표현식은 결과를 직접 출력하는 데 사용됩니다. `<%= %>` 태그를 사용하여 작성합니다.

#### 예제코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>JSP 표현식 예제</title>
</head>
<body>
    <h1>현재 시간:</h1>
    <%= new java.util.Date() %>
</body>
</html>
```

- `<%= %>`: 이 안에 작성된 `Java` 표현식의 결과가 `HTML`로 출력됩니다.

- `new java.util.Date()`: 현재 날짜와 시간을 생성하고 이를 바로 출력합니다.

## JSP 선언문 (Declarations)

JSP 선언문은 클래스 레벨에서 사용할 변수를 선언하거나 메서드를 정의할 때 사용합니다. `<%! %>` 태그를 사용합니다.

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>JSP 선언문 예제</title>
</head>
<body>
    <h1>2와 3을 더한 값:</h1>
    <%= add(2, 3) %>
</body>
</html>

<%! 
    public int add(int a, int b) {
        return a + b;
    }
%>
```

- `<%! %>`: 이 안에 작성된 코드는 선언문으로, `JSP` 페이지에서 전역적으로 사용됩니다.

- `public int add(int a, int b)`: 두 숫자를 더하는 메서드를 선언합니다.

- `<%= add(2, 3) %>`: 선언한 메서드를 호출하여 결과를 출력합니다.

## 4. JSP 지시자 (Directives)

JSP 지시자는 페이지, 포함, 태그 라이브러리 등을 설정하는 데 사용됩니다. `<%@ %>` 태그를 사용합니다.

#### 페이지 지시자 (Page Directive)

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
```

- `language="java"`: JSP 페이지에서 사용할 프로그래밍 언어를 지정합니다.

- `contentType="text/html; charset=UTF-8"`: 응답의 `MIME` 타입과 문자 인코딩을 설정합니다.

- `pageEncoding="UTF-8"`: JSP 페이지 파일의 인코딩을 지정합니다.

#### 포함 지시자 (Include Directive)

```java
<%@ include file="header.jsp" %>
```

- `file="header.jsp"`: 지정된 파일의 내용을 현재 JSP 파일에 포함시킵니다.

## 5. JSP 주석 (Comments)

JSP 주석은 페이지에 출력되지 않으며, JSP 파일 내에서 설명을 추가할 때 사용됩니다. `<%-- --%>` 태그를 사용합니다.

#### 예제코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>JSP 주석 예제</title>
</head>
<body>
    <h1>JSP 주석 예제</h1>
    <%-- 이 부분은 주석 처리되어 브라우저에 출력되지 않습니다. --%>
</body>
</html>
```

- `<%-- --%>`: 이 안에 작성된 내용은 JSP 주석으로 간주되어 브라우저에 출력되지 않습니다.

## 6. JSP 액션 태그 (Action Tags)

JSP 액션 태그는 특정 작업을 수행하는데 사용됩니다. `<jsp:action>` 형식을 사용합니다.

#### 예제코드

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>JSP 액션 태그 예제</title>
</head>
<body>
    <jsp:include page="header.jsp" />
    <h1>메인 콘텐츠</h1>
    <jsp:include page="footer.jsp" />
</body>
</html>
```

- `<jsp:include page="header.jsp" />`: `header.jsp` 파일의 내용을 포함합니다.

- `<jsp:include page="footer.jsp" />`: `footer.jsp` 파일의 내용을 포함합니다.
