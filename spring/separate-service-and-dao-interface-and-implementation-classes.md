# Service와 DAO의 인터페이스와 구현 클래스 분리

서비스(`Service`)와 DAO(`Data Access Object`)를 인터페이스와 구현 클래스(`Impl`)로 분리하는 것은 객체 지향 설계에서 널리 사용되는 패턴으로, 시스템의 유연성과 유지보수성을 크게 향상시킬 수 있습니다. 하지만 모든 경우에 무조건적으로 분리해야 하는 것은 아니며, 상황에 따라 그 필요성과 이점이 달라질 수 있습니다.

#### Service 계층

- **역할:** 비즈니스 로직 처리, 사용자 요청을 받아 필요한 작업을 수행하고, 필요한 경우 DAO 계층과 상호작용하여 데이터 처리
- **예시:** 사용자 등록, 주문 처리, 결제 처리 등 비즈니스 로직을 포함하는 작업

#### DAO 계층

- **역할:** 데이터베이스와의 상호작용 담당, `CRUD(Create, Read, Update, Delete)` 작업 수행
- **예시:** 사용자 정보 저장, 제품 목록 조회, 주문 내역 업데이트 등 데이터베이스 관련 작업.

## 인터페이스와 구현 클래스의 분리 이유

#### 주요 이점

1. **유연성 향상:** 인터페이스를 통해 구현체를 쉽게 교체할 수 있습니다. 예를 들어, 데이터베이스를 변경하거나 테스트용 목(`mock`) 객체로 대체할 때 유용합니다.

2. **테스트 용이성:** 인터페이스를 사용하면 의존성 주입(`Dependency Injection`)을 통해 쉽게 목 객체를 주입하여 단위 테스트를 수행할 수 있습니다.

3. **의존성 감소:** 코드 간의 결합도를 낮춰 유지보수성을 높이고, 모듈 간의 독립성을 강화합니다.

4. **다형성 지원:** 다양한 구현체를 사용하여 동일한 인터페이스를 통해 다양한 동작을 수행할 수 있습니다.

### Service 계층에서의 인터페이스와 구현 클래스 분리

#### 주로 나누어지는 경우

- **복잡한 비즈니스 로직:** 비즈니스 로직이 복잡하거나 여러 구현체가 필요한 경우.
- **테스트 및 유지보수:** 서비스 로직을 쉽게 테스트하고 유지보수하려는 경우.
- **확장성:** 향후 서비스 로직이 변경되거나 확장될 가능성이 있는 경우.

#### 분리 시기

- **초기 설계 단계:** 애플리케이션의 아키텍처를 설계할 때.
- **기능 추가 시:** 새로운 비즈니스 로직이 추가될 때.
- **리팩토링 시:** 기존 코드의 유지보수성과 확장성을 개선하려 할 때.

##### 예제 코드

```java
// Service 인터페이스
public interface UserService {
    void registerUser(User user);
    User getUserById(Long id);
}

// Service 구현 클래스
public class UserServiceImpl implements UserService {
    private final UserDAO userDAO;
    
    public UserServiceImpl(UserDAO userDAO) {
        this.userDAO = userDAO;
    }
    
    @Override
    public void registerUser(User user) {
        // 비즈니스 로직 처리
        userDAO.save(user);
    }
    
    @Override
    public User getUserById(Long id) {
        return userDAO.findById(id);
    }
}
```

### DAO 계층에서의 인터페이스와 구현 클래스 분리

#### 주로 나누어지는 경우

- **데이터 소스 변경 가능성:** 데이터베이스 종류가 변경될 가능성이 있거나 여러 데이터 소스를 지원해야 하는 경우.
- **재사용성:** 동일한 데이터 접근 로직을 여러 서비스에서 재사용할 때.
- **테스트 용이성:** 데이터 접근 로직을 테스트할 때 목 DAO를 사용하고자 할 때.

#### 분리 시기

- **데이터 접근 전략 변경 시:** 예를 들어, JDBC에서 JPA로 변경할 때.
- **복잡한 데이터 접근 로직:** 복잡한 쿼리나 트랜잭션 관리가 필요한 경우.
- **다양한 데이터 소스 지원 시:** 여러 데이터베이스 또는 외부 데이터 소스를 지원할 때.

##### 예제 코드

```java
// DAO 인터페이스
public interface UserDAO {
    void save(User user);
    User findById(Long id);
}

// DAO 구현 클래스 (JPA 사용)
public class UserDAOImpl implements UserDAO {
    @PersistenceContext
    private EntityManager entityManager;
    
    @Override
    public void save(User user) {
        entityManager.persist(user);
    }
    
    @Override
    public User findById(Long id) {
        return entityManager.find(User.class, id);
    }
}
```

### Service와 DAO 계층의 분리 적용 시기

#### 공통 적용 시기

- **프로젝트 초기 단계:** 확장성과 유연성을 고려하여 초기부터 계층을 분리합니다.
- **복잡한 비즈니스 로직:** 단순한 CRUD 애플리케이션이 아닌 복잡한 로직을 처리해야 할 때.
- **팀 협업 시:** 여러 팀원이 동시에 작업할 때 각 계층을 명확히 분리하여 작업 효율을 높입니다.

#### 예외적인 경우

- **단순 애플리케이션:** 비즈니스 로직이 매우 단순하거나 데이터 접근이 최소화된 애플리케이션에서는 계층 분리가 과도할 수 있습니다.
- **프로토타입:** 빠른 개발이 필요하고 유지보수보다는 기능 구현이 우선인 경우.
