# Join
데이터베이스에서는 데이터를 잘 관리하기 위해서 [정규화](./Normalization.md)과정을 거친다.

이러한 정규화를 진행하게 되면, 데이터가 모두 흩어지게 되는데, 이 때 의미있는 정보를 얻기 위해 `Join`이라는 기술이 필요하다.

조인이란 두 개 이상의 테이블을 특정 컬럼 기준으로 연결해, 마치 처음부터 하나의 테이블인 것 처럼 보여주는 기능

> 기본 키 (Primary Key)와 외래 키(Foreign Key)를 사용해 데이터를 합친다.

## Inner Join
> 두 테이블에 공통적으로 존재하는 데이터만을 결과로 보여준다.

```sql
SELECT *
FROM tableA
(INNER) JOIN tableB
    ON tableA.연결컬럼 = tableB.연결 컬
```

## Outer Join
> 두 테이블을 조인 할 때, 특정 테이블의 데이터는 ON 조건이 맞지 않더라도 모두 결과에 포함한다.

- Left Join : JOIN 키워드를 기준으로 왼쪽 테이블의 모든 데이터 포함, 오른쪽 테이블은 일치하는 것만
- Right Join : JOIN 키워드를 기준으로 오른쪽 테이블의 모든 데이터 포함, 왼쪽 테이블은 일치하는 것만
- Cross Join : 두 테이블의 모든 가능한 조합

## SELF Join
> 테이블이 자기 자신과 조인하는

```sql
SELECT
    e.Name AS "직원 이름",
    m.Name AS "관리자 이름"
FROM
    Employees e -- 직원용 테이블
INNER JOIN
    Employees m ON e.ManagerID = m.EmployeeID; -- 관리자용 테이블
```

## Natural Join
> 두 테이블에서 이름이 같은 모든 컬럼을 기준으로 자동으로 연결한다.

`ON`절을 따로 작성하지 않아도, 알아서 공통된 이름을 가진 컬럼을 찾아 연결 해 줌

다만 예상치 못한 컬럼이 연결 기준으로 사용 될 수 있어 사용을 지양하는 편