# 임시 테이블을 사용하여 데이터 관리하기

임시 테이블은 데이터베이스에서 일시적으로 데이터를 저장하고 관리하는 데 매우 유용한 도구입니다. 임시 테이블은 주로 복잡한 쿼리 성능을 향상시키거나, 세션 간 데이터를 임시로 저장하여 다양한 작업을 수행하는 데 사용됩니다.

## 임시 테이블이란?

임시 테이블(`Temporary Table`)은 데이터베이스 세션 동안만 존재하는 테이블로, 세션이 종료되면 자동으로 삭제됩니다. 임시 테이블은 SQL에서 `CREATE TEMPORARY TABLE` 문을 사용하여 생성할 수 있으며, 생성된 테이블은 해당 세션의 사용자만 접근할 수 있습니다.

#### 임시 테이블의 두 가지 유형

- **로컬 임시 테이블:** 세션 단위로 유지되며, 다른 세션에서는 접근할 수 없습니다.
- **글로벌 임시 테이블:** 전역적으로 사용되며, 다른 세션에서도 접근할 수 있지만, 데이터는 각 세션에서 독립적으로 관리됩니다.

## 임시 테이블 생성 방법

임시 테이블을 생성하는 방법 일반적인 테이블을 생성하는 것과 거의 유사하지만, `TEMPORARY` 키워드를 추가합니다.

```sql
CREATE TEMPORARY TABLE temp_table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```

- 이 테이블은 세션이 끝나면 자동으로 삭제되며, 다른 세션에서는 접근할 수 없습니다.

## 활용 예시

#### 복잡한 쿼리 최적화

복잡한 SQL 쿼리를 수행할 때, 중간 결과를 임시 테이블에 저장하여 반복 계산을 피하고 성능을 개선할 수 있습니다.

```sql
CREATE TEMPORARY TABLE temp_sales AS
SELECT product_id, SUM(sales_amount) AS total_sales
FROM sales
GROUP BY product_id;

SELECT product_id, total_sales
FROM temp_sales
WHERE total_sales > 1000;
```

- `sales` 테이블에서 중간 결과를 임시 테이블에 저장한 후, 그 결과를 기반으로 추가 쿼리를 실행합니다. 이 방식은 쿼리 성능을 크게 향상시킬 수 있습니다.

#### 세션 간 데이터 유지

어떤 경우에는 동일한 세션 내에서 여러 쿼리 간에 데이터를 공유해야 할 때가 있습니다. 예를 들어, 특정 작업의 중간 결과를 임시 테이블에 저장하고 이후의 작업에서 이를 참조할 수 있습니다.

```sql
CREATE TEMPORARY TABLE temp_user_actions (
    user_id INT,
    action VARCHAR(50),
    action_time TIMESTAMP
);

-- 사용자 행동 데이터 삽입
INSERT INTO temp_user_actions (user_id, action, action_time)
VALUES (1, 'login', NOW());

-- 삽입된 데이터 확인
SELECT * FROM temp_user_actions;
```

- `temp_user_actions` 테이블은 세션이 종료되면 자동으로 삭제되므로, 별도의 데이터 정리 작업이 필요 없습니다.

## 주의 사항

#### 자원 관리

임시 테이블은 메모리에 저장되기 때문에, 많은 양의 데이터를 저장하거나 여러 임시 테이블을 동시에 사용하면 서버의 메모리 자원을 많이 소모할 수 있습니다. 따라서, 필요하지 않은 임시 테이블은 즉시 삭제하거나, 데이터 양을 적절히 관리해야 합니다.

#### 세션 종료 시 데이터 손실

임시 테이블은 세션이 종료되면 자동으로 삭제되므로, 중요한 데이터를 임시 테이블에 저장하면 안 됩니다. 세션이 종료되면 임시 테이블에 저장된 데이터는 모두 사라지기 때문에, 장기적으로 저장해야 할 데이터는 영구 테이블에 저장해야 합니다.
