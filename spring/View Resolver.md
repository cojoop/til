# View Resolver란

View Resolver는 컨트롤러가 반환한 논리적 뷰 이름(`logical view name`)을 실제 뷰 파일로 변환해주는 컴포넌트입니다. 사용자가 요청한 경로를 처리하고, 결과를 특정 View(`JSP, Thymeleaf 등`)로 보여주는 역할을 합니다.

### View Resolver의 동작 과정

#### 1. 컨트롤러에서 논리적 뷰 이름 반환

- Spring MVC 컨트롤러 메서드는 “home”과 같은 논리적 뷰 이름을 반환합니다.

#### 2. 뷰 리졸버가 뷰 이름을 물리적 경로로 변환

- 뷰 리졸버는 반환된 뷰 이름을 바탕으로 설정된 경로와 확장자를 더해 물리적인 뷰 파일 경로를 만듭니다.
- 예를 들어, `InternalResourceViewResolver`가 기본 경로로 `/WEB-INF/views/`를, 확장자로 `.jsp`를 설정한 경우 "home"을 `/WEB-INF/views/home.jsp`로 변환합니다.

#### 3. 뷰 렌더링

- 변환된 물리적 경로의 뷰 파일이 존재하면, Spring MVC는 뷰 파일을 렌더링하여 사용자에게 결과를 반환합니다.

### 주요 View Resolver 종류

#### 1. InternalResourceViewResolver

- 주로 JSP와 같은 서버 사이드 뷰를 사용하기 위해 설정하며, 설정된 경로와 확장자를 결합하여 뷰를 찾습니다.
- prefix와 suffix를 설정해 경로를 지정합니다.

#### 2. ThymeleafViewResolver

- Thymeleaf 템플릿 엔진을 사용하는 경우에 적합한 뷰 리졸버입니다.
- ThymeleafViewResolver는 Thymeleaf의 템플릿 파일을 찾고 렌더링하는 데 사용됩니다.

#### 3. BeanNameViewResolver

- 뷰 이름과 동일한 이름을 가진 빈을 찾아서 그 빈을 사용하여 뷰를 반환합니다.
- 보통 뷰 리졸버로는 자주 사용되지 않지만, 특정 뷰 빈이 필요한 경우 사용됩니다.

#### 4. XmlViewResolver

- XML 파일에 정의된 뷰 빈을 기반으로 뷰를 찾습니다.
- 뷰를 명시적으로 설정 파일에서 정의할 때 사용됩니다.

#### 5. UrlBasedViewResolver

- 뷰 이름이 URL의 형태로 제공되는 경우 사용됩니다.
- prefix와 suffix를 조합하지 않고 URL 형식의 뷰 이름을 사용합니다.
