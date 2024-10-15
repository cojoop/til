# Statement와 PreparedStatement의 차이

`Statement`와 `PreparedStatement`는 SQL 쿼리를 실행하는 데 사용되는 `Java JDBC API`의 두 가지 주요 인터페이스입니다.

## 주요 차이점

### 캐시 사용

`Statement`는 매번 쿼리를 실행할 때마다 다음 단계를 거칩니다.

1. 쿼리 문장 분석
2. 컴파일
3. 실행

반면 `PreparedStatement`는 처음 한 번만 위 세 단계를 거친 후 캐시에 저장하여 재사용합니다.

- 따라서 동일한 쿼리를 반복 실행할 때 `PreparedStatement`가 더 효율적입니다.

### SQL 인젝션 방지

`PreparedStatement`는 파라미터화된 쿼리를 사용하여 SQL 인젝션 공격을 방지합니다.
입력값을 이스케이프 처리하여 안전하게 쿼리에 삽입합니다.

### 가독성

`PreparedStatement`는 복잡한 쿼리의 경우 더 깔끔한 코드 작성이 가능합니다.

```java
PreparedStatement pstmt = conn.prepareStatement("UPDATE USER set name = ? where id = ?");
pstmt.setString(1, name);
pstmt.setString(2, id);
```

`Statement`는 문자열 연결로 인해 복잡해질 수 있습니다.

### 사용 시기

#### PreparedStatement 사용이 권장되는 경우

- 동일한 쿼리를 조건만 변경하여 반복 실행할 때
- 전달할 파라미터가 많을 때
- 사용자 입력을 쿼리에 포함할 때

#### Statement 사용이 적합한 경우

- 동적 쿼리를 사용해야 할 때 (`PreparedStatement`의 캐싱 이점을 활용할 수 없음)
-

`PreparedStatement`가 여러 장점이 있지만, 각 데이터베이스의 캐싱 한계를 고려하여 꼭 필요한 쿼리에만 사용하는 것이 좋습니다.
