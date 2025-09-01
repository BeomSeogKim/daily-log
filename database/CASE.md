# CASE
> 데이터 자체를 동적으로 가공할 수 있는 도구

CASE 문의 경우 크게 두가지 방식으로 나뉜다.
- Simple Case Expression
- Searched Case Expression

## Simple Case Expression
> 특정 하나의 컬럼이나 표현식의 값에 따라 결과를 다르게 하고 싶을 때 사용

```sql
CASE col
    WHEN val1 THEN result1
    WHEN val2 THEN result2
    ...
    ELSE default_result
END
```
***실행 순서: 위에서 아래 순서대로 조건을 평가하며, 가장 먼저 일치하는 WHEN절을 만나면 THEN의 결과를 반환하고 즉시 평가 종료***

## Searched Case Expression
> 각 WHEN 절에 독립적인 조건식을 사용하여 복잡한 논리를 구현할 때 사용

```sql
CASE col
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE default_result
END
```

## CASE Grouping
> CASE로 변환 한 값들을 토대로 그룹핑을 진행할 수 있다.

```sql
SELECT
    CASE
        WHEN YEAR(birth_date) >= 1990 THEN '1990년대생'
        WHEN YEAR(birth_date) >= 1980 THEN '1980년대생'
        ELSE '그 이전 출생'
    END AS birth_decade,
COUNT(*) AS customer_count
    FROM
        users
GROUP BY
        birth_decade;
```
*원리대로라면 GROUP BY절이 SELECT 절 보다 먼저처리되지만, MySQL에서는 이러한 별칭 사용을 예외적으로 허용*

## CASE - 조건부 집계
> 집계함수의 인자로 CASE문을 넣어 '조건에 맞을 때만 세거나 더하게' 만드는 패턴

### Pattern 1 COUNT(CASE ...)
COUNT 함수는 NULL이 아닌 모든 값을 센다는 특징을 이용

```sql
SUM(CASE WHEN status = 'COMPLETED' THEN 1 END)
```

### Pattern 2 SUM(CASE ...)
SUM 함수로 숫자들의 합계를 구함

```sql
SUM(CASE WHEN status = 'COMPLETED' THEN 1 ELSE 0 END)
```
