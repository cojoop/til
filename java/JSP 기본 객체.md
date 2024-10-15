# JSP 기본 객체

JSP의 기본 객체(내장 객체)는 JSP 페이지를 실행할 때 자동으로 생성되어 사용할 수 있는 객체들입니다.
이 객체들은 JSP 페이지 작성 시 자주 사용되며, 웹 애플리케이션 개발에 필수적입니다.

### 주요 JSP 기본 객체

#### request

- 클라이언트의 HTTP 요청 정보를 저장합니다.
- 파라미터, 쿠키, HTTP 헤더 정보 등을 얻을 수 있습니다.

#### response

- 클라이언트로 보낼 HTTP 응답 정보를 저장합니다.
- HTML 코드, 이미지, 텍스트 파일 등을 클라이언트에게 전송할 수 있습니다.

#### out

- JSP 페이지의 출력 스트림을 관리합니다.
- HTML 코드, 텍스트 메시지 등을 출력할 수 있습니다.

#### session

- 클라이언트와 서버 간의 세션 정보를 저장합니다.
- 로그인 정보, 장바구니 정보 등을 유지할 수 있습니다.

#### application

- 웹 애플리케이션 전체에서 공유되는 정보를 저장합니다.
- 모든 사용자, 페이지, 세션에서 접근 가능합니다.

### 영역(Scope)

JSP 기본 객체는 각각 다른 영역(`scope`)을 가지고 있습니다.

- **page 영역:** 하나의 JSP 페이지 내에서만 유효 (`pageContext` 객체)
- **request 영역:** 하나의 HTTP 요청을 처리하는 동안 유효 (`request` 객체)
- **session 영역:** 하나의 웹 브라우저와 관련된 영역에서 유효 (`session` 객체)
- **application 영역:** 웹 애플리케이션 전체에서 유효 (`application` 객체)

### 속성 관리

기본 객체들은 속성을 통해 정보를 저장하고 공유할 수 있습니다.

### 주요 메소드

- `setAttribute(String name, Object value)`: 속성 설정
- `getAttribute(String name)`: 속성 값 반환
- `removeAttribute(String name)`: 속성 삭제
- `getAttributeNames()`: 속성 이름 목록 반환 (`pageContext` 제외)

이러한 JSP 기본 객체들을 효과적으로 활용하면 웹 애플리케이션의 다양한 기능을 구현할 수 있습니다.
