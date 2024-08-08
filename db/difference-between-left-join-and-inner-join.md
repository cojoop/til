# LEFT JOIN과 INNER JOIN의 차이점

`LEFT JOIN`과 `INNER JOIN`은 SQL에서 두 테이블을 결합하는 데 사용하는 주요 조인 방식입니다. 이 두 가지 조인 방식은 데이터를 결합하는 방식에서 차이가 있습니다.

## INNER JOIN

`INNER JOIN`은 두 테이블 간의 공통된 값을 가진 레코드만 반환합니다. 즉, 두 테이블에서 일치하는 데이터만 결과에 포함됩니다.

#### 예제

다음과 같이 두 테이블이 있다고 가정했을 경우,

- Employees 테이블

EmployeeID|Name
----|----
1|Alice
2|Bob
3|Charlie

- Departments 테이블

EmployeeID|Department
----|----
1|HR
2|IT
4|Finance

이 두 테이블을 EmployeeID를 기준으로 INNER JOIN으로 결합하면 다음과 같습니다.

```sql
SELECT Employees.Name, Departments.Department
FROM Employees
INNER JOIN Departments
ON Employees.EmployeeID = Departments.EmployeeID;
```

#### 결과

Name|Department
----|----
Alice|HR
Bob|IT

이 쿼리는 `Employees` 테이블과 `Departments` 테이블 간에 `EmployeeID`가 일치하는 데이터만 반환합니다.

## LEFT JOIN (또는 LEFT OUTER JOIN)

`LEFT JOIN`은 왼쪽 테이블의 모든 레코드를 반환하고, 오른쪽 테이블의 일치하는 레코드가 있으면 그 레코드도 포함합니다. 오른쪽 테이블에서 일치하는 레코드가 없는 경우, 해당 컬럼은 `NULL`로 반환됩니다.

#### 예제

위와 같은 두 테이블을 `LEFT JOIN`으로 결합하면 다음과 같습니다:

```sql
SELECT Employees.Name, Departments.Department
FROM Employees
LEFT JOIN Departments
ON Employees.EmployeeID = Departments.EmployeeID;
```

#### 결과

Name|Department
----|----
Alice|HR
Bob|IT
Charlie|NULL

이 쿼리는 `Employees` 테이블의 모든 레코드를 반환하고, `Departments` 테이블에서 일치하는 레코드가 없는 경우 `Department` 컬럼이 `NULL`로 나타납니다.

### 요약

- **INNER JOIN:** 두 테이블에서 조건에 맞는 데이터만 반환합니다. 일치하지 않는 데이터는 결과에 포함되지 않습니다.

- **LEFT JOIN:** 왼쪽 테이블의 모든 데이터를 반환하며, 오른쪽 테이블의 일치하는 데이터가 있으면 함께 반환합니다. 오른쪽 테이블에 일치하는 데이터가 없으면 `NULL`로 표시됩니다.
