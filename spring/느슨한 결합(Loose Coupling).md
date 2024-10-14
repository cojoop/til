# 느슨한 결합(Loose Coupling)이란

스프링에서 느슨한 결합(`Loose Coupling`)은 객체 간의 의존성을 줄이고 유연성을 높이는 중요한 개념입니다.
이를 통해 코드의 유지보수성과 확장성이 향상됩니다.

### 느슨한 결합의 개념

느슨한 결합은 클래스 간의 결합도를 낮추는 것을 의미합니다.
이는 주로 인터페이스를 활용하여 구현됩니다.

#### 주요 특징

- 구체 클래스 대신 인터페이스에 의존
- 런타임 시 의존관계 결정
- 코드 수정 최소화

### 강한 결합 vs 느슨한 결합

#### 강한 결합

- 객체가 다른 객체를 직접 생성하고 사용
- 코드 변경 시 많은 수정 필요
- 유지보수 어려움

#### 느슨한 결합

- 인터페이스를 통한 의존성 주입
- 코드 변경 시 수정 최소화
- 유연성과 확장성 향상

### 스프링의 의존성 주입 (DI)

스프링은 의존성 주입을 통해 느슨한 결합을 구현합니다.

#### 주요 방식

- 생성자 주입
- 필드 주입
- `Setter` 주입

#### 장점

- **유연성:** 구현 클래스 변경 시 코드 수정 최소화
- **테스트 용이성:** 목(`mock`) 객체 사용 가능
- **재사용성:** 컴포넌트 재사용 용이

#### 예제 코드

```java
// 인터페이스
public interface PowerUnit {
    void useSource();
}

// 구현 클래스
public class GasolineEngine implements PowerUnit {
    @Override
    public void useSource() {
        // 가솔린 엔진 구현
    }
}

// 클라이언트 클래스
public class Car {
    private PowerUnit powerUnit;

    public Car(PowerUnit powerUnit) {
        this.powerUnit = powerUnit;
    }

    public void ride() {
        powerUnit.useSource();
    }
}
```

- `Car` 클래스는 구체적인 `GasolineEngine` 대신 `PowerUnit` 인터페이스에 의존합니다.
- 이를 통해 다른 종류의 엔진으로 쉽게 교체할 수 있는 유연성을 제공합니다.
