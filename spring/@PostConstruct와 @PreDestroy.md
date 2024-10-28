# @PostConstruct와 @PreDestroy

`@PostConstruct`와 `@PreDestroy`는 Java 애노테이션으로, 스프링의 빈 생명 주기에서 초기화와 종료 작업을 정의할 때 사용합니다.

## @PostConstruct

@PostConstruct는 빈이 생성되고 의존성 주입이 완료된 후 초기화 작업을 수행합니다.

- **동작 시점:** 빈의 생성과 의존성 주입이 끝난 뒤, 빈이 준비되어 컨테이너에 추가되기 전에 호출.

### 주요 특징

- WAS가 시작될 때 빈이 생성된 직후 딱 한 번만 실행됩니다.
- 초기화 작업이나 기본 설정을 수행하는 데 적합합니다.
- 모든 접근 제어자를 가질 수 있지만, `static` 메서드일 수 없습니다.

#### 사용 예시

```java
@Component
public class MyService {
    
    @PostConstruct
    public void init() {
        // 초기화 작업
        System.out.println("MyService 빈 초기화 완료");
    }
}
```

## @PreDestroy

@PreDestroy는 빈이 소멸되기 전, 리소스를 해제하거나 종료 작업을 수행합니다.

- **동작 시점:** 스프링 컨테이너가 빈을 소멸하기 직전에 호출.

### 주요 특징

- 애플리케이션 컨텍스트에서 빈이 제거되기 직전에 한 번만 호출됩니다.
- 리소스 해제나 정리 작업을 수행하는 데 적합합니다.
- 모든 접근 제어자를 가질 수 있지만, `static` 메서드일 수 없습니다.

#### 사용 예시

```java
@Component
public class MyService {

    @PreDestroy
    public void destroy() {
        // 종료 작업
        System.out.println("MyService 빈 종료 전 작업 수행");
    }
}
```

#### 주의 사항

- `@PostConstruct`와 `@PreDestroy`는 빈이 **_싱글톤으로 관리될 때_** 유용하게 사용할 수 있으며, **_프로토타입 스코프 빈_** 에는 기본적으로 `@PreDestroy`가 적용되지 않습니다. 이 경우 프로토타입 빈의 종료 작업은 직접 관리해야 합니다.
- `@PostConstruct`와 `@PreDestroy`는 Java 표준 애노테이션(`javax.annotation 패키지`)로, Java EE 및 Spring에서 모두 사용 가능합니다.
