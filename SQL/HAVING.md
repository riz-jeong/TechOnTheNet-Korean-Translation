# SQL : HAVING 절

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL HAVING 절을 사용하는 방법을 설명합니다.

## 설명
SQL HAVING 절은 [GROUP BY 절](GROUP_BY.md)과 함께 사용하여 반환되는 행의 그룹을 조건이 TRUE인 행으로만 제한합니다.

## 구문
SQL에서 HAVING 절의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n, 
       aggregate_function (aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n
HAVING condition;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- 집계 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_function**
- [SUM](SUM.md), [COUNT](COUNT.md), [MIN](MIN.md), [MAX](MAX.md), [AVG](AVG.md) 함수와 같은 집계 함수입니다.
#### **aggregate_expression**
- aggregate_function가 사용될 열 또는 표현식입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions**
- 선택 사항입니다. 레코드를 선택하기 위한 조건입니다.
#### **HAVING condition**
- 반환되는 행의 그룹을 제한하기 위해 집계된 결과에만 적용되는 추가 조건입니다. 조건이 TRUE로 평가되는 그룹만 결과 집합에 포함됩니다.

---
## 예제 - SUM 함수 사용
SQL [SUM 함수](SUM.md)를 사용하는 SQL HAVING 절의 예를 살펴보겠습니다.

SQL [SUM 함수](SUM.md)를 사용하여 부서 이름과 연결된 부서의 총 매출을 반환할 수도 있습니다. SQL HAVING 절은 매출액이 $1000보다 큰 부서만 반환되도록 결과를 필터링합니다.
```SQL
SELECT department, SUM(sales) AS "Total sales"
FROM order_details
GROUP BY department
HAVING SUM(sales) > 1000;
```

---
## 예제 - COUNT 함수 사용
SQL [COUNT 함수](COUNT.md)에 HAVING 절을 어떻게 사용할 수 있는지 살펴보겠습니다.

SQL [COUNT 함수](COUNT.md)를 사용하여 부서 이름과 연간 $25,000 이상을 버는 관련 부서의 직원 수를 반환할 수 있습니다. SQL HAVING 절은 직원이 10명 이상인 부서만 반환되도록 결과를 필터링합니다.
```SQL
SELECT department, COUNT(*) AS "Number of employees"
FROM employees
WHERE salary > 25000
GROUP BY department
HAVING COUNT(*) > 10;
```

---
## 예제 - MIN 함수 사용
이제 SQL [MIN 함수](MIN.md)와 함께 HAVING 절을 사용하는 방법을 살펴보겠습니다.

SQL [MIN 함수](MIN.md)를 사용하여 각 부서의 이름과 해당 부서의 최저 급여를 반환할 수도 있습니다. SQL HAVING 절은 최저 급여가 $35,000보다 큰 부서만 반환합니다.
```SQL
SELECT department, MIN(salary) AS "Lowest salary"
FROM employees
GROUP BY department
HAVING MIN(salary) > 35000;
```

---
## 예제 - MAX 함수 사용
마지막으로 SQL [MAX 함수](MAX.md)와 함께 HAVING 절을 사용하는 방법을 살펴보겠습니다.
예를 들어 SQL [MAX 함수](MAX.md)를 사용하여 각 부서의 이름과 해당 부서의 최대 급여를 반환할 수도 있습니다. SQL HAVING 절은 최대 급여가 $50,000 미만인 부서만 반환합니다.
```SQL
SELECT department, MAX(salary) AS "Highest salary"
FROM employees
GROUP BY department
HAVING MAX(salary) < 50000;
```

---
**[< 이전](AVG.md) / [다음 : SELECT LIMIT >](SELECT_LIMIT.md)**