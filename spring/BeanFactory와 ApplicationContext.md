# BeanFactory와 ApplicationContext

`BeanFactory`와 `ApplicationContext`는 Spring 프레임워크의 핵심 인터페이스로, 두 개 모두 IoC (`Inversion of Control`) 컨테이너 역할을 합니다.
하지만 `ApplicationContext`는 `BeanFactory`의 상위 인터페이스로, `Bean` 관리 외에 추가 기능을 제공합니다.

## BeanFactory

BeanFactory는 스프링 컨테이너의 최상위 인터페이스입니다.

### 주요 특징

- 스프링 빈을 관리하고 조회하는 기본적인 기능을 제공합니다.
- `getBean()` 메서드를 통해 빈을 조회할 수 있습니다.
- 빈의 생성을 지연시켜 실제로 빈이 필요할 때까지 인스턴스화를 미룹니다.

## ApplicationContext

`ApplicationContext`는 `BeanFactory`를 확장한 인터페이스로, 더 많은 기능을 제공합니다.

### 주요 특징

- BeanFactory의 모든 기능을 상속받아 제공합니다12.
- 빈 관리 기능에 더해 다양한 부가 기능을 제공합니다12.

#### ApplicationContext가 제공하는 주요 부가 기능

1. 메시지 소스를 활용한 국제화 기능: 다국어 지원을 위한 기능을 제공합니다.
2. 환경변수 관리: 로컬, 개발, 운영 등 다양한 환경을 구분하여 처리할 수 있습니다.
3. 애플리케이션 이벤트: 이벤트 발행 및 구독 모델을 지원합니다.
4. 리소스 조회: 파일, 클래스패스, 외부 등에서 리소스를 쉽게 조회할 수 있습니다.

### BeanFactory vs ApplicationContext

- `BeanFactory`는 기본적인 DI 컨테이너 기능에 중점을 둡니다.
- `ApplicationContext`는 `BeanFactory`의 기능을 포함하면서 엔터프라이즈 애플리케이션에 필요한 추가 기능을 제공합니다.
- 실제 개발에서는 대부분 `ApplicationContext`를 사용하며, `BeanFactory`를 직접 사용하는 경우는 거의 없습니다.
