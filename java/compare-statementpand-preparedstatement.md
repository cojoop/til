# Statement와 PreparedStatement의 비교

`Java Database Connectivity (JDBC)`는 Java 프로그램이 데이터베이스에 연결하고 쿼리를 실행할 수 있게 해주는 API입니다. JDBC의 핵심 클래스 중 두 가지는 `Statement`와 `PreparedStatement`입니다.

> 이 두 클래스를 이해하고 적절하게 사용하는 것은 효율적이고 안전한 데이터베이스 작업을 수행하는 데 중요합니다.

## Statement

`Statement`는 정적 SQL 쿼리를 실행하는 데 사용됩니다.

- 동적 파라미터를 포함하지 않는 단순 쿼리 작업에 적합합니다.

### 특징

- **단순성:** 동적 파라미터가 없는 단순한 쿼리에 적합합니다.

- **유연성 부족:** 파라미터가 있는 쿼리를 효율적으로 처리할 수 없습니다.

- **보안 문제:** SQL 인젝션 공격에 취약합니다.

#### 사용 예제

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class StatementExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";
        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {

            String query = "SELECT * FROM users";
            ResultSet rs = stmt.executeQuery(query);
            while (rs.next()) {
                System.out.println("User ID: " + rs.getInt("id"));
                System.out.println("Username: " + rs.getString("username"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## PreparedStatement

`PreparedStatement`는 동적 파라미터를 포함하는 SQL 쿼리를 실행하는 데 사용됩니다.

- 반복적으로 실행될 쿼리나 입력 파라미터가 있는 쿼리에 적합합니다.

### 특징

- **효율성:** 미리 컴파일된 SQL 문을 재사용할 수 있어 성능이 향상됩니다.

- **보안:** 파라미터 바인딩을 통해 SQL 인젝션 공격을 방지합니다.

- **유연성:** 동적 파라미터 처리가 용이합니다.

#### 사용 예제

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class PreparedStatementExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";
        try (Connection conn = DriverManager.getConnection(url, user, password);
             PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM users WHERE id = ?")) {

            pstmt.setInt(1, 1); // 첫 번째 파라미터를 1로 설정
            ResultSet rs = pstmt.executeQuery();
            while (rs.next()) {
                System.out.println("User ID: " + rs.getInt("id"));
                System.out.println("Username: " + rs.getString("username"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Statement와 PreparedStatement의 비교

특성|Statement|PreparedStatement
----|----|---
보안|SQL 인젝션에 취약|파라미터 바인딩으로 SQL 인젝션 방지
성능|단순 쿼리에 적합|반복 실행 시 성능 우수
유연성|정적 쿼리만 가능|동적 파라미터 처리 용이
재사용성|재사용 불가|미리 컴파일된 SQL 재사용 가능

## ResultSet

`ResultSet`은 SQL 쿼리의 결과를 포함하는 객체입니다.

- `Statement` 또는 `PreparedStatement`의 `executeQuery` 메서드 호출 시 반환됩니다.

### 특징

- **탐색:** 결과 집합을 반복하여 탐색할 수 있습니다.

- **데이터 접근:** 열 이름 또는 인덱스를 통해 데이터에 접근할 수 있습니다.

- **커서 위치:** 커서를 통해 현재 위치를 유지하고, 이를 기반으로 데이터를 읽습니다.

#### ResultSet 사용 예제

위의 `Statement` 및 `PreparedStatement` 예제에서 사용된 `ResultSet` 객체는 결과 집합을 탐색하여 각 행의 데이터를 출력합니다.

`ResultSet`의 `next()` 메서드를 사용하여 커서를 다음 행으로 이동하고, 각 열의 데이터를 `getInt`, `getString` 등의 메서드를 통해 읽습니다.
