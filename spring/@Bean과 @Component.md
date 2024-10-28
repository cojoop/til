# @Bean과 @Component 비교

`@Bean`과 `@Component`는 둘 다 Spring에서 `Bean`을 생성하는 데 사용되는 어노테이션입니다.

### 주요 차이점

#### 1. 적용 대상

**- @Component:** 클래스 레벨에 적용. 개발자가 작성한 클래스 자체를 스프링 빈으로 등록할 때 사용.
**- @Bean:** 메소드 레벨에 적용. 메소드가 반환하는 객체를 스프링 빈으로 등록할 때 사용.

#### 2. 사용 범위

**- @Component:** 서비스, 레포지토리, 컨트롤러 등 개발자가 직접 작성한 클래스에 사용
**- @Bean:** 주로 외부 라이브러리 클래스를 빈으로 등록할 때 사용

#### 3. 등록 방식

**- @Component:** `@ComponentScan` 또는 `@SpringBootApplication`에 포함된 컴포넌트 스캔 기능에 의해, 클래스패스 스캐닝(`classpath scanning`)을 통해 자동으로 빈 등록
**- @Bean:** `@Configuration`이 적용된 클래스 내에서, 개발자가 수동으로 작성한 `@Bean` 메소드의 반환 객체를 스프링 컨테이너가 빈으로 등록

### 사용 시기

#### @Component 사용

- 개발자가 직접 제어할 수 있는 클래스를 빈으로 등록할 때
- 비즈니스 로직을 담은 서비스 클래스, 리포지토리 등에 사용

#### @Bean 사용

- 외부 라이브러리의 클래스를 빈으로 등록해야 할 때
- 빈 생성 과정에서 추가적인 설정이 필요한 경우 (`ex. 초기화 파라미터 설정`)
- 같은 타입의 여러 빈을 만들어야 할 때
- 조건에 따라 빈을 생성하거나 수동으로 빈 등록 로직을 작성해야 할 때

### 예시

#### @Component 사용

```java
@Component
public class MyService {
    // 비즈니스 로직
}
```

#### @Bean 사용

```java
@Configuration
public class AppConfig {
    @Bean
    public ObjectMapper objectMapper() {
        return new ObjectMapper();
    }
}
```
