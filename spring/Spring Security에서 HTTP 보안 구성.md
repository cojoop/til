# Spring Security에서 HTTP 보안 구성을 정의하는 방법

Spring Security에서 HTTP 보안 구성을 정의하는 방법은 주로 `WebSecurityConfigurerAdapter`를 확장하거나, `Spring Security 5.4`이후에는 `SecurityFilterChain`을 사용하여 설정할 수 있습니다. 이를 통해 애플리케이션의 HTTP 요청에 대한 접근 제어, 인증, 권한 부여 등의 보안 규칙을 정의할 수 있습니다.

## Spring Security에서 HTTP 보안 구성을 정의하는 주요 단계

### 1. 기본 설정 클래스 생성

우선 Spring Security 설정 클래스를 생성해야 합니다. 이 클래스는 `@Configuration`과 `@EnableWebSecurity` 애너테이션을 사용하여 Spring Security 구성을 활성화합니다.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        // HTTP 보안 설정 코드 작성
        return http.build();
    }
}
```

### 2. HTTP 보안 규칙 정의

`HttpSecurity` 객체를 사용하여 특정 URL 패턴에 대한 접근 규칙을 정의합니다. 예를 들어, 인증이 필요한 페이지와 공용 페이지를 구분할 수 있습니다.

```java
http
    .authorizeRequests()
        .antMatchers("/public/**").permitAll() // 누구나 접근 가능한 URL
        .antMatchers("/admin/**").hasRole("ADMIN") // ADMIN 역할이 있는 사용자만 접근
        .anyRequest().authenticated(); // 나머지 모든 요청은 인증 필요
```

#### 주요 메서드

- **antMatchers:** URL 패턴을 정의하고, 해당 경로에 접근할 수 있는 조건을 설정합니다.
- **permitAll:** 모든 사용자에게 접근을 허용합니다.
- **authenticated:** 인증된 사용자만 접근할 수 있습니다.
- **hasRole:** 특정 역할을 가진 사용자만 접근할 수 있도록 설정합니다.

### 3. 폼 로그인 및 로그아웃 설정

폼 기반 로그인을 설정하고, 기본 로그인 및 로그아웃 경로를 정의할 수 있습니다.

```java
http
    .formLogin()
        .loginPage("/login") // 사용자 정의 로그인 페이지
        .defaultSuccessUrl("/home") // 로그인 성공 후 이동 페이지
        .permitAll()
    .and()
    .logout()
        .logoutUrl("/logout") // 로그아웃 경로
        .logoutSuccessUrl("/login?logout") // 로그아웃 후 리다이렉션 경로
        .permitAll();
```

### 4. CSRF 및 CORS 설정

Spring Security는 기본적으로 `CSRF(Cross-Site Request Forgery)` 보호가 활성화되어 있습니다. 이 설정을 비활성화하거나 특정 요청에서만 적용하도록 할 수 있습니다.

```java
http
    .csrf()
        .disable(); // CSRF 보호 비활성화

http
    .cors(); // CORS 설정 활성화
```

### 5. 예외 처리 설정

인증 실패 시 발생하는 예외에 대한 처리 방법을 정의할 수 있습니다.

```java
http
    .exceptionHandling()
        .authenticationEntryPoint((request, response, authException) -> 
            response.sendError(HttpServletResponse.SC_UNAUTHORIZED, "Unauthorized"));
```
