# POJO와 Java Bean, Spring Bean

POJO, Java Bean, 그리고 Spring Bean은 모두 Java 개발에서 자주 등장하는 개념으로, 객체지향 프로그래밍 및 Spring 프레임워크에서 중요한 역할을 합니다.

## POJO (Plain Old Java Object)

POJO는 프레임워크나 기술에 종속되지 않고 순수한 Java 객체로, 객체지향 프로그래밍의 기본 원칙을 따릅니다.

### 특징

- 특정 프레임워크나 기술에 종속되지 않음
- 일반적인 Java 객체로 설계됨 (생성자, 필드, 메서드 포함)
- 단순성, 유연성 제공
- 테스트가 용이

#### 장점

- 단순성과 유연성 제공
- 테스트 용이성
- 객체지향 원리 적용 용이

POJO는 모든 Java 객체가 될 수 있고, 기본적으로는 비즈니스 로직을 구현하는데 사용됩니다.

#### 예제 코드

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

## Java Bean

Java Bean은 POJO에서 파생된 개념으로, 몇 가지 특정한 규칙을 추가로 따르는 클래스입니다.

### 특징

- 기본 생성자(`no-arg constructor`)를 가져야 함
- 모든 필드는 `private`으로 선언
- `getter`와 `setter` 메서드를 제공하여 필드에 접근
- `Serializable` 인터페이스를 구현하여 직렬화 가능
- 캡슐화 원칙을 철저히 따름

#### 예제 코드

```java
public class Employee implements Serializable {
    private String name;
    private int id;

    public Employee() {
        // 기본 생성자
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}
```

Java Bean은 주로 데이터 전송 객체(DTO) 또는 값 객체(VO)로 사용됩니다.

## Spring Bean

Spring Bean은 Spring IoC (`Inversion of Control`) 컨테이너에 의해 생성하고 관리하는 객체입니다.

### 특징

- Spring IoC 컨테이너에 의해 생성 및 관리됨
- 객체 간 의존성을 자동으로 주입하여 설정
- 어노테이션(`@Component, @Service, @Repository 등`) 또는 XML/Java 설정을 통해 Bean 등록 가능
- 객체의 라이프사이클을 컨테이너가 관리
- 주로 애플리케이션의 서비스, 리포지토리, 컨트롤러 등을 Spring Bean으로 설정

#### 빈 등록 방법

**1. XML 설정:** 전통적인 방식으로 `Spring Bean`을 XML 파일에서 설정.
**2. 어노테이션 기반:** `@Component`, `@Service`, `@Repository`, `@Controller`를 사용하여 클래스 위에 어노테이션을 붙여 등록.
**3. Java Config:** `@Configuration`과 `@Bean`을 사용하여 Java 파일에서 설정.

#### 예제 코드

```java
@Service
public class EmployeeService {
    public Employee getEmployeeById(int id) {
        // 로직 처리
    }
}
```

Spring Bean은 애플리케이션의 핵심 객체로, Spring 프레임워크의 많은 기능을 활용할 수 있게 해줍니다.
