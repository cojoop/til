# 느슨한 결합(Loose Coupling)이란

스프링 프레임워크에서 느슨한 결합은 애플리케이션의 구성 요소들이 서로 강하게 의존하지 않고, 유연하게 연결되는 설계 원칙을 의미합니다. 느슨한 결합을 통해 시스템의 유지보수성과 확장성을 높일 수 있으며, 변경에 대한 영향을 최소화할 수 있습니다.

### 느슨한 결합의 중요성

1. **유지보수성 향상:** 컴포넌트 간의 의존성이 낮아지면, 한 부분의 변경이 다른 부분에 미치는 영향이 줄어듭니다.
2. **재사용성 증대:** 독립적인 컴포넌트는 다른 애플리케이션이나 모듈에서도 쉽게 재사용될 수 있습니다.
3. **테스트 용이성:** 독립적인 컴포넌트는 단위 테스트(`Unit Test`)를 수행하기 쉬워집니다.
4. **확장성:** 새로운 기능을 추가하거나 기존 기능을 수정할 때, 다른 부분에 영향을 덜 미치면서 확장이 가능합니다.

### 스프링에서 느슨한 결합을 구현하는 방법

스프링에서는 의존성 주입(`Dependency Injection`) 을 통해 느슨한 결합을 구현합니다. 의존성 주입은 객체가 필요한 의존성을 스스로 생성하지 않고 외부에서 주입받는 방식입니다. 이를 통해 컴포넌트 간의 직접적인 의존성을 줄일 수 있습니다.

#### 주요 방법

1. **인터페이스 사용:** 구체 클래스 대신 인터페이스를 사용하여 의존성을 주입받습니다.
2. **컨테이너 관리:** 스프링 컨테이너가 객체의 생명주기를 관리하고, 필요한 의존성을 주입합니다.
3. **애너테이션 기반 설정:** `@Autowired`, `@Inject`, `@Qualifier` 등의 애너테이션을 사용하여 의존성을 설정합니다.

#### 예제 코드

```java
// 서비스 인터페이스 정의
public interface PaymentService {
    void processPayment(double amount);
}
```

```java
// 서비스 구현 클래스
@Service
public class CreditCardPaymentService implements PaymentService {
    @Override
    public void processPayment(double amount) {
        // 신용카드 결제 처리 로직
        System.out.println("Processing credit card payment of $" + amount);
    }
}

@Service
public class PaypalPaymentService implements PaymentService {
    @Override
    public void processPayment(double amount) {
        // 페이팔 결제 처리 로직
        System.out.println("Processing PayPal payment of $" + amount);
    }
}
```

```java
// 의존성을 주입받는 클라이언트 클래스
@Controller
public class OrderController {

    private final PaymentService paymentService;

    @Autowired
    public OrderController(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void createOrder(double amount) {
        // 주문 생성 로직
        paymentService.processPayment(amount);
    }
}
```
