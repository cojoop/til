# Querydsl

`Querydsl`은 Java 기반의 타입 안전한 쿼리 생성기를 제공하는 라이브러리로, SQL과 같은 질의를 코드로 표현할 수 있게 합니다.
전통적인 SQL 쿼리문과는 다르게, 도메인 모델에 기반한 쿼리를 작성할 수 있어, 쿼리 작성 중 발생할 수 있는 오류를 컴파일 시점에서 미리 감지할 수 있습니다.

### 주요 특징

- 정적 타입을 이용해 SQL과 같은 쿼리를 생성할 수 있게 해줍니다.
- `JPA`, `JDO`, `JDBC` 등 다양한 백엔드 기술을 지원합니다.
- 도메인 모델을 기반으로 쿼리 타입을 자동 생성합니다.

#### 장점

- **타입 안정성:** 컴파일 시점에 오류를 잡을 수 있어 런타임 오류를 방지합니다.
- **코드 자동완성:** IDE의 자동완성 기능을 활용할 수 있습니다.
- **동적 쿼리:** 복잡하고 동적인 쿼리 작성이 용이합니다.
- **가독성:** 자바 코드로 작성되어 SQL 문자열보다 가독성이 좋습니다.

### JPQL과의 비교

#### JPQL

```java
String jpql = "select m from Member m where m.username = :username";
List<Member> result = em.createQuery(query, Member.class).getResultList();
```

#### Querydsl

```java
List<Member> result = queryFactory
  .select(member)
  .from(member)
  .where(usernameEq(username))
  .fetch();
```

- `Querydsl`은 `JPQL`의 문자열 기반 쿼리 작성의 단점을 극복하고 타입 안전성과 유지보수성을 크게 향상시킵니다.

#### 사용 방법

1. 엔티티 클래스 생성
2. `Querydsl` 플러그인으로 `Q-Type` 클래스 자동 생성
3. 생성된 `Q-Type` 클래스를 사용해 쿼리 작성
4. 작성된 `Querydsl` 쿼리는 내부적으로 `JPQL`로 변환되어 실행됩니다.

`Querydsl`을 사용하면 타입 안전성, 유지보수성, 가독성 등 여러 측면에서 이점을 얻을 수 있어 복잡한 쿼리 작성에 매우 유용합니다.
