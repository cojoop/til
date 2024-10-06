# 의존성 주입(Dependency Injection, DI)이란

의존성 주입(`Dependency Injection`)은 객체지향 프로그래밍에서 객체 간의 의존성을 외부에서 주입해주는 디자인 패턴입니다. 객체는 필요한 의존성을 직접 생성하거나 관리하지 않고, 외부에서 주입받아 사용하게 됩니다.

> 객체 간의 결합도를 낮추고, 코드의 유연성과 테스트 가능성을 높일 수 있습니다.

## 의존성 주입의 핵심 개념

- **의존성(Dependency):** 하나의 객체가 다른 객체를 필요로 할 때, 그 필요로 하는 객체를 ‘의존성’이라고 합니다.

- **주입(Injection):** 의존성을 필요로 하는 객체에 외부에서 그 의존성을 주입하는 행위를 말합니다.

의존성 주입의 주요 목적은 객체들 간의 강한 결합을 `느슨한 결합`으로 바꿔줌으로써, 코드의 유지보수성을 높이고, 확장성과 테스트 용이성을 제공하는 것입니다.

## 의존성 주입 방법

1. **생성자 주입(Constructor Injection):** 의존성을 클래스의 생성자를 통해 주입하는 방식

2. **세터 주입(Setter Injection):** 의존성을 세터 메서드를 통해 주입하는 방식

3. **필드 주입(Field Injection):** 클래스의 필드에 직접 의존성을 주입하는 방식

이 중 생성자 주입이 가장 많이 사용되며, 권장되는 방식입니다.

### 생성자 주입이 주로 사용되는 이유

1. **불변성 보장:** 생성자 주입은 객체가 생성될 때 의존성을 모두 주입받기 때문에, 주입 후에는 해당 의존성이 변경될 수 없습니다.

2. **필수 의존성 강제:** 생성자 주입은 객체 생성 시 반드시 의존성을 제공해야 하기 때문에, 객체가 정상적으로 작동하기 위해 필요한 의존성을 강제로 주입할 수 있습니다.

3. **테스트 용이성:** 의존성을 생성자를 통해 주입하면, 테스트 코드에서 필요한 의존성을 쉽게 **모의 객체(Mock Object)**로 대체할 수 있습니다.

4. **객체의 상태 완전성 보장:** 생성자 주입을 사용하면 객체가 생성되는 순간 모든 의존성이 주입되기 때문에, 해당 객체는 완전한 상태로 바로 사용할 수 있습니다. 반면 세터 주입이나 필드 주입은 의존성이 나중에 주입될 수 있어, 주입되지 않은 상태에서 객체가 잘못 사용될 가능성이 있습니다.

5. **불변 필드 사용 가능:** 생성자 주입을 사용하면 의존성을 `final`로 선언할 수 있습니다. 이는 주입된 후 변경되지 않음을 컴파일러 수준에서 보장할 수 있다는 점에서 안정성을 더해줍니다.

#### 예제 코드

```java
// 의존성 클래스
public class AccountService {
    public void processAccount() {
        System.out.println("Account processed");
    }
}

// 의존성을 주입받는 클래스
public class TransactionService {
    private final AccountService accountService;

    // 생성자 주입
    public TransactionService(AccountService accountService) {
        this.accountService = accountService;
    }

    public void saveTransaction() {
        accountService.processAccount();
        System.out.println("Transaction saved");
    }
}

// 사용
public class Main {
    public static void main(String[] args) {
        // 의존성 생성
        AccountService accountService = new AccountService();
        
        // 의존성 주입
        TransactionService transactionService = new TransactionService(accountService);
        
        // 메서드 호출
        transactionService.saveTransaction();
    }
}
```
