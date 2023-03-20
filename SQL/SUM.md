# SQL : SUM 함수

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **SUM 함수**를 사용하는 방법을 설명합니다.

## 설명
SQL SUM 함수는 SELECT 문에서 식의 합계를 반환하는 데 사용됩니다.

## 구문
SQL에서 SUM 함수의 구문은 다음과 같습니다.
```SQL
SELECT SUM(aggregate_expression)
FROM tables
[WHERE conditions];
```
또는 하나 이상의 열을 기준으로 결과를 그룹화할 때 SUM 함수의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n,
       SUM(aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- SUM 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_expression**
- 합산할 열 또는 표현식입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하려면 반드시 충족해야 하는 조건입니다.

---
## 예제 - 단일 표현식 사용
예를 들어 salary가 25,000달러 이상인 모든 직원의 총 salary를 합산한 금액을 알고 싶을 수 있습니다.
```SQL
SELECT SUM(salary) AS "Total Salary"
FROM employees
WHERE salary > 25000;
```
이 SQL SUM 함수 예제에서는 SUM(salary) 식의 [별칭](ALIASES.md)을 "Total Salary"로 지정했습니다. 따라서 결과 집합이 반환될 때 "Total Salary"가 필드 이름으로 표시됩니다.

---
## 예제 - SQL DISTINCT 사용
SQL SUM 함수 내에서 SQL [DISTINCT 절](DISTINCT.md)을 사용할 수 있습니다. 예를 들어, 아래의 SQL SELECT 문은 salary가 $25,000 이상인 고유한 salary 값의 합산 총 salary를 반환합니다.
```SQL
SELECT SUM(DISTINCT salary) AS "Total Salary"
FROM employees
WHERE salary > 25000;
```
salary가 $30,000인 salary가 두 개 있는 경우, 이 중 하나의 값만 SQL SUM 함수에 사용됩니다.

---
## 예제 - 공식 사용
SQL SUM 함수에 포함된 표현식은 단일 필드일 필요는 없습니다. 수식을 사용할 수도 있습니다. 예를 들어 비즈니스의 순이익이 필요할 수 있습니다. 순이익은 총 수입에서 총 비용을 뺀 값으로 계산됩니다.
```SQL
SELECT SUM(income - expenses) AS "Net Income"
FROM gl_transactions;
```
SQL SUM 함수 내에서 수학 연산을 수행할 수도 있습니다. 예를 들어 총 커미션을 총 매출의 10%로 결정할 수 있습니다.
```SQL
SELECT SUM(sales * 0.10) AS "Commission"
FROM order_details;
```

---
## 예제 - SQL GROUP BY 사용
경우에 따라 SQL SUM 함수와 함께 SQL [GROUP BY 절](GROUP_BY.md)을 사용해야 할 수도 있습니다.

예를 들어, SQL SUM 함수를 사용하여 부서 이름과 (관련 부서의) 총 매출을 반환할 수도 있습니다.
```SQL
SELECT department, SUM(sales) AS "Total sales"
FROM order_details
GROUP BY department;
```
SQL [SELECT 문](SELECT.md)에 SQL SUM 함수에 캡슐화되지 않은 열 하나를 나열했으므로 SQL [GROUP BY 절](GROUP_BY.md)을 사용해야 합니다. 따라서 부서 필드는 SQL GROUP BY 섹션에 나열되어야 합니다.

---
**[< 이전](COUNT.md) / [다음 : MAX >](MAX.md)**