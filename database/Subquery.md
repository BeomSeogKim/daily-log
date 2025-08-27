# Subquery
하나의 SQL 쿼리문 안에 포함된 또 다른 쿼리를 의미한다.

서브쿼리의 경우 바깥쪽의 메인 쿼리가 실행되기 전에, 괄호 안의 서브 쿼리가 먼저 실행된다.

```sql
SELECT p.name, p.price
FROM products p
WHERE p.price > (SELECT AVG(price) FROM products);
```

해당 쿼리에서 `SELECT AVG(price) FROM products` 가 제일 먼저 실행된다.

## 서브 쿼리의 종류와 특징
| 구분 | 반환 형태 | 주요 사용 위치 | 명칭 |
|----|-------|----------|----|
| 단일 컬럼| 단일 행 | SELECT, WHERE, HAVING| 스칼라 서브쿼리 |
| | 다중 행 | WHERE, HAVING | 다중 행 서브쿼리 |
| 다중 컬럼 | 단일 행 | WHERE, HAVING | 다중 컬럼 서브 쿼리 |
| | 다중 행 | WHERE, HAVING | 다중 컬럼 서브 쿼리 |
| 다중 컬럼 | 다중 행 | FROM | 테이블 서브 쿼리|

