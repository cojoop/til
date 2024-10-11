# Service와 DAO에서 인터페이스와 구현 클래스를 나누는 이유

Service와 DAO(`Data Access Object`) 계층에서 인터페이스와 구현 클래스(일반적으로 `Impl` 접미사를 사용)를 분리하여 사용하는 것은 소프트웨어 설계에서 매우 일반적인 패턴입니다.
이러한 분리는 유지보수성, 확장성, 테스트 용이성 등을 향상시키며, 다양한 상황에서 유용하게 활용됩니다.

## 기본 개념 이해

#### DAO (Data Access Object)

- **역할:** 데이터베이스와의 상호작용을 담당합니다. CRUD(`Create, Read, Update, Delete`) 작업을 수행하며, 데이터 소스에 독립적인 방식으로 데이터를 조작합니다.

#### Service

- **역할:** 비즈니스 로직을 처리합니다. 여러 DAO를 조합하거나, 비즈니스 규칙을 적용하는 등의 작업을 수행합니다.

#### 인터페이스와 구현 클래스

- **인터페이스:** 기능의 명세를 정의합니다. 어떤 메서드가 제공되는지, 어떤 동작을 해야 하는지를 선언합니다.
- **구현 클래스 (Impl):** 인터페이스에서 정의한 메서드를 실제로 구현합니다.

## 인터페이스와 구현 클래스를 나누는 이유

#### 1. 추상화와 결합도 낮추기

- 인터페이스는 구현과 분리된 추상화를 제공하여, 코드의 결합도를 낮추고 유연성을 높입니다.
- 클라이언트는 인터페이스에 의존하고, 실제 구현은 변경될 수 있습니다.

#### 2. 유지보수성과 확장성 향상

- 인터페이스를 사용하면 구현을 변경하거나 새로운 구현체를 추가할 때 기존 코드를 수정할 필요가 줄어듭니다.
- 예를 들어, 데이터 소스가 변경될 경우 DAO 구현체만 교체하면 됩니다.

#### 3. 테스트 용이성

- 인터페이스를 통해 의존성을 주입하면, 단위 테스트 시에 목(`Mocking`) 객체을 쉽게 사용할 수 있습니다.
- 이는 테스트의 독립성과 신뢰성을 높여줍니다.

#### 4. 다형성 활용

- 동일한 인터페이스를 구현하는 여러 클래스 간의 다형성을 활용할 수 있습니다.
- 상황에 따라 다른 구현체를 선택적으로 사용할 수 있습니다.

## Service와 DAO 계층에서의 인터페이스 분리

### DAO 계층에서의 인터페이스와 Impl 분리

#### 주로 나누어지는 경우

- **데이터 소스 변경 가능성:** 데이터베이스 종류나 ORM(`Object-Relational Mapping`) 프레임워크 변경 시.
- **복잡한 데이터 접근 로직:** 여러 데이터 소스나 복잡한 쿼리가 필요한 경우.
- **테스트 용이성:** 데이터 접근 로직을 목킹하여 서비스 계층을 테스트할 때.

#### 예제 코드

```java
// DAO 인터페이스
public interface UserDao {
    User findById(Long id);
    void save(User user);
    // 기타 CRUD 메서드
}

// DAO 구현 클래스
public class UserDaoImpl implements UserDao {
    // 실제 데이터베이스 접근 로직 구현
    @Override
    public User findById(Long id) {
        // 데이터베이스 조회 로직
    }

    @Override
    public void save(User user) {
        // 데이터베이스 저장 로직
    }
}
```

#### 언제 나누는지

- 프로젝트 초기 단계부터 인터페이스를 정의하여, 데이터 소스 변경에 대한 유연성을 확보하고자 할 때.
- 여러 구현체가 필요할 가능성이 있거나, 특정 구현체를 확장할 필요가 있을 때.

### Service 계층에서의 인터페이스와 Impl 분리

#### 주로 나누어지는 경우

- **비즈니스 로직의 복잡성:** 여러 DAO를 조합하거나, 복잡한 비즈니스 규칙을 적용할 때.
- **다양한 서비스 구현 필요:** 다른 방식의 비즈니스 로직을 제공하는 여러 서비스 구현이 필요할 때.
- **테스트 용이성:** 서비스 계층을 단위 테스트할 때, 실제 구현 대신 목 객체를 사용하고자 할 때.

#### 예제 코드

```java
// Service 인터페이스
public interface UserService {
    User getUserById(Long id);
    void registerUser(UserDto userDto);
    // 기타 비즈니스 메서드
}

// Service 구현 클래스
public class UserServiceImpl implements UserService {
    private final UserDao userDao;
    
    // 생성자 주입 등으로 UserDao 의존성 주입
    public UserServiceImpl(UserDao userDao) {
        this.userDao = userDao;
    }
    
    @Override
    public User getUserById(Long id) {
        return userDao.findById(id);
    }
    
    @Override
    public void registerUser(UserDto userDto) {
        // 비즈니스 로직 처리 후 DAO를 통해 저장
        User user = new User(userDto);
        userDao.save(user);
    }
}
```

#### 언제 나누는지

- 서비스 계층에서 다양한 비즈니스 로직을 적용하거나, 여러 DAO를 조합할 때.
- 여러 서비스 구현체가 필요할 가능성이 있거나, 특정 구현체를 확장할 필요가 있을 때.
- 인터페이스 기반의 의존성 주입(`DI`)을 활용하여 유연성을 높이고자 할 때.

> Service와 DAO 에서 인터페이스와 구현 클래스를 분리하여 사용하는 것은 코드의 유연성, 유지보수성, 테스트 용이성을 크게 향상시킬 수 있습니다.
> 그러나 모든 프로젝트에 무조건적으로 적용할 필요는 없으며, 프로젝트의 규모, 복잡성, 미래의 확장 가능성 등을 고려하여 적절하게 적용하는 것이 중요합니다.
