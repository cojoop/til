# 빈(Bean)이란

빈(`Bean`)은 스프링 컨테이너가 관리하는 자바 객체로, 스프링 컨테이너에 의해 생성되고 관리되는 재사용 가능한 소프트웨어 컴포넌트입니다.
인스턴스화된 객체를 의미하며, 스프링 컨테이너에 등록된 객체를 스프링 빈(`Bean`)이라고 합니다.

### 빈의 특징

- 클래스의 등록 정보, `Getter/Setter` 메서드를 포함합니다.
- 컨테이너에서 사용되는 설정 메타데이터로 생성됩니다.
- 스프링에서 사용하는 애플리케이션 객체라고 이해할 수 있습니다.

### 빈 등록 방법

#### 1. XML 설정 파일 사용

- `application.xml` 파일에 빈을 명시적으로 정의합니다.

#### 2. 어노테이션 사용

- `@Component`, `@Service`, `@Repository` 등의 어노테이션을 클래스에 추가하여 빈으로 등록합니다.

#### 3. @Bean 어노테이션 사용

- 메서드에 `@Bean` 어노테이션을 추가하여 해당 메서드가 반환하는 객체를 빈으로 등록합니다.

### 빈 정의(BeanDefinition)

빈은 `BeanDefinition`이라는 추상화를 통해 정의되며, `BeanDefinition`에는 다음과 같은 정보가 포함됩니다.

- **BeanClassName:** 생성할 빈의 클래스 이름
- **factoryBeanName:** 팩토리 역할의 빈 이름
- **factoryMethodName:** 빈을 생성할 팩토리 메서드 이름
- **Scope:** 빈의 범위 (기본값은 싱글톤)
- **lazyInit:** 지연 초기화 여부
- **InitMethodName:** 초기화 메서드 이름
- **DestroyMethodName:** 소멸 메서드 이름

### 빈(Bean) 접근 방법

#### 스프링에서 빈 접근

스프링에서는 주로 `ApplicationContext`를 통해 빈에 접근합니다.
`XML` 또는 `Java Config` 파일에서 빈을 정의한 후, `ApplicationContext`를 이용해 해당 빈을 불러올 수 있습니다.

```java
// XML 설정 파일을 사용하는 경우
ApplicationContext context = new ClassPathXmlApplicationContext("application.xml");
MyService myService = context.getBean("myService", MyService.class);
```

```java
// Java 설정에서 빈 접근
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}

ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
MyService myService = context.getBean(MyService.class);
```

- `AnnotationConfigApplicationContext`는 자바 설정 클래스에서 빈을 로드하는 데 사용됩니다.

#### 스프링 부트에서 빈 접근

스프링 부트에서는 `@SpringBootApplication` 어노테이션을 통해 자동으로 컨텍스트를 설정합니다.
스프링 부트 애플리케이션에서 빈을 가져오는 방법은 스프링과 거의 동일하지만, 스프링 부트에서는 명시적으로 `ApplicationContext`를 생성하지 않고도 빈을 사용할 수 있습니다.

- 주로 `@Autowired`를 사용하여 빈을 주입합니다.

```java
@Service
public class MyService {
    public String serve() {
        return "Hello World!";
    }
}

@RestController
public class MyController {

    @Autowired
    private MyService myService;

    @GetMapping("/hello")
    public String hello() {
        return myService.serve();
    }
}
```

<br>

> #### 빈의 중요성
>
> 빈은 스프링의 IoC(`Inversion of Control`) 및 DI(`Dependency Injection`) 기능의 기반이 됩니다.
> 스프링 컨테이너가 빈을 관리함으로써 객체 생성, 의존성 주입, 생명주기 관리 등을 자동화하고 애플리케이션의 결합도를 낮출 수 있습니다.
