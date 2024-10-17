# JPA(Java Persistence API)

JPA(`Java Persistence API`)는 자바 애플리케이션에서 관계형 데이터베이스를 쉽게 사용할 수 있도록 도와주는 ORM(`Object-Relational Mapping`) 기술입니다.

## JPA의 핵심 개념

### 엔티티(Entity)

엔티티는 데이터베이스 테이블과 매핑되는 자바 객체입니다.
`@Entity` 어노테이션을 사용하여 정의합니다.

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true)
    private String username;
    
    @Column(nullable = false)
    private String password;
    
    // getters and setters
}
```

### 리포지토리(Repository)

리포지토리는 엔티티에 대한 CRUD 연산을 수행하는 인터페이스입니다. `JpaRepository` 인터페이스를 상속받아 사용합니다.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
}
```

### JPA 사용 예제

#### 엔티티 저장

```java
User user = new User();
user.setUsername("johndoe");
user.setPassword("password123");
userRepository.save(user);
```

#### 엔티티 조회

```java
Optional<User> user = userRepository.findById(1L);
List<User> allUsers = userRepository.findAll();
```

#### 쿼리 메서드

메서드 이름으로 쿼리를 생성할 수 있습니다.

```java
List<User> findByAgeGreaterThan(int age);
User findByUsernameAndEmail(String username, String email);
```

#### @Query 어노테이션

복잡한 쿼리는 `@Query` 어노테이션을 사용하여 직접 작성할 수 있습니다.

```java
@Query("SELECT u FROM User u WHERE u.email LIKE %:domain%")
List<User> findUsersByEmailDomain(@Param("domain") String domain);
```

#### JPA의 장점

**1. 객체 지향적 접근:** 개발자는 SQL 대신 객체 지향적인 코드로 데이터베이스를 다룰 수 있습니다.
**2. 생산성 향상:** 반복적인 CRUD 쿼리 작성을 줄여 개발 시간을 단축시킵니다.
**3. 유지보수성:** 데이터베이스 스키마 변경 시 JPA가 자동으로 처리해주어 유지보수가 용이합니다.
**4. 데이터베이스 독립성:** JPA는 다양한 데이터베이스를 지원하므로 데이터베이스 변경이 쉽습니다.

#### 주의사항

**1. 성능 최적화:** 복잡한 쿼리의 경우 JPA가 생성하는 SQL이 비효율적일 수 있으므로 주의가 필요합니다.
**2. 학습 곡선:** JPA의 개념과 사용법을 익히는 데 시간이 필요할 수 있습니다.
**3. 트랜잭션 관리:** JPA를 사용할 때는 적절한 트랜잭션 관리가 중요합니다.
