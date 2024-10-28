# @Component와 @ComponentScan

`@Component`와 `@ComponentScan`은 Spring Framework에서 빈(`Bean`) 등록을 자동화하는 중요한 기능을 제공합니다.

## @Component

`@Component`는 클래스 레벨에서 사용되는 애노테이션으로, 해당 클래스를 스프링의 빈으로 등록하도록 지정합니다.

### 주요 특징

- 클래스에 `@Component`를 붙이면 스프링이 해당 클래스를 빈으로 자동 등록합니다.
- 기본적으로 클래스명을 카멜케이스로 변환한 이름을 빈 이름으로 사용합니다.
- `@Component("customName")`과 같이 빈의 이름을 직접 지정할 수도 있습니다.

#### 관련 애노테이션

`@Component`를 특화한 다음 애노테이션들도 컴포넌트 스캔의 대상이 됩니다

- **@Controller:** 스프링 MVC 컨트롤러로 사용
- **@Service:** 비즈니스 로직을 담당하는 서비스 계층에 사용
- **@Repository:** 데이터 접근 계층에 사용
- **@Configuration:** 스프링 설정 정보를 담당

## @ComponentScan

`@ComponentScan`은 `@Component`가 붙은 클래스들을 자동으로 스캔하여 빈으로 등록하는 기능을 제공합니다.

### 주요 특징

- 설정 클래스에 `@ComponentScan`을 붙이면, 해당 클래스가 있는 패키지부터 하위 패키지까지 모두 스캔합니다.
- `basePackages` 속성을 통해 스캔할 패키지를 지정할 수 있습니다.

#### 사용 예시

```java
@Configuration
@ComponentScan(basePackages = {"com.example.myapp.controllers", "com.example.myapp.services"})
public class AppConfig {
    // 설정 내용
}
```

#### 스캔 과정

1. `@ComponentScan`이 선언된 클래스부터 스캔을 시작합니다.
2. 지정된 패키지와 하위 패키지의 모든 클래스를 검사합니다.
3. `@Component`(또는 관련 애노테이션)가 붙은 클래스를 발견하면 빈으로 등록합니다.

### 의존성 주입

컴포넌트 스캔을 사용할 때 의존성 주입은 주로 @Autowired를 통해 이루어집니다.

```java
@Component
public class MemberServiceImpl implements MemberService {
    private final MemberRepository memberRepository;
    
    @Autowired
    public MemberServiceImpl(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
    
    // 서비스 메소드 구현
}
```

#### 주의사항

- 컴포넌트 스캔은 편리하지만, 애플리케이션이 커질수록 모든 빈을 자동으로 등록하는 것이 복잡성을 증가시킬 수 있습니다.
- 필요한 경우 `excludeFilters`를 사용하여 특정 클래스나 패키지를 스캔 대상에서 제외할 수 있습니다
