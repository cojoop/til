# Servlet과 JSP(JavaServer Pages)

Servlet과 JSP(`JavaServer Pages`)는 Java 기반의 웹 애플리케이션 개발을 위한 핵심 기술입니다.

### Servlet

Servlet은 서버에서 동적으로 웹 페이지를 생성하거나 데이터를 처리하기 위해 Java로 작성된 프로그램입니다.

#### 주요 특징

- Java 코드 안에 HTML 태그가 삽입되는 구조
- `.java` 확장자 사용
- 컴파일 후 배포 필요
- HTML 태그를 문자열로 처리해야 함

### JSP (JavaServer Pages)

JSP는 HTML 내부에 Java 코드를 삽입하는 형식의 서버 스크립트 기술입니다.
Servlet의 단점을 보완하기 위해 만들어졌습니다.

#### 주요 특징

- HTML 안에 Java 코드를 삽입하는 구조
- `.jsp` 확장자 사용
- 태그 형식으로 Java 코드 사용 가능 (`<% %> 등`)
- 간편한 웹 프로그래밍 구현 가능

### MVC 패턴에서의 역할

현대 웹 개발에서는 Servlet과 JSP를 함께 사용하는 MVC(`Model-View-Controller`) 패턴이 일반적입니다.

- **Controller:** Servlet이 담당
  - 사용자 요청 처리
  - 비즈니스 로직 호출
  - 결과를 View로 전달
- **View:** JSP가 담당
  - 사용자에게 결과 표시
  - 프레젠테이션 로직 처리

> 이러한 구조는 프레젠테이션 로직과 비즈니스 로직을 분리하여 유지보수를 용이하게 합니다.

Servlet과 JSP는 각각의 장단점을 가지고 있으며, 현대 웹 개발에서는 두 기술을 적절히 조합하여 사용합니다.
 Servlet은 컨트롤러 역할을, JSP는 뷰 역할을 담당하여 효율적인 웹 애플리케이션 개발을 가능하게 합니다.
