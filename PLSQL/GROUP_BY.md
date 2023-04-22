# Oracle / PLSQL : GROUP BY 절

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **GROUP BY 절**을 사용하는 방법을 설명합니다.

## 설명
Oracle GROUP BY 절은 SELECT 문에서 여러 레코드에서 데이터를 수집하고 결과를 하나 이상의 열로 그룹화하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 GROUP BY 절의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n, 
       aggregate_function (aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- 집계 함수 내에 캡슐화되지 않은 표현식이며 GROUP BY 절에 포함되어야 하는 표현식입니다.
#### **aggregate_function**
- [SUM](SUM.md), [COUNT](COUNT.md), [MIN](MIN.md), [MAX](MAX.md), [AVG](MAX.md) 함수와 같은 함수일 수 있습니다.
#### **aggregate_expression**
- aggregate_function이 사용될 열 또는 표현식입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 하나 이상의 테이블이 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.

---
## 예제 - SUM 함수 사용
[SUM 함수](SUM.md)를 사용하는 Oracle GROUP BY 쿼리 예제를 살펴보겠습니다.

이 Oracle GROUP BY 예제에서는 SUM 함수를 사용하여 제품과 해당 제품의 총 매출을 반환합니다.
```SQL
SELECT product, SUM(sale) AS "Total sales"
FROM order_details
GROUP BY product;
```
SELECT 문에 SUM 함수에 캡슐화되지 않은 열(product 필드) 하나를 나열했으므로 GROUP BY 절을 사용해야 합니다. 따라서 product 필드는 GROUP BY 절에 나열되어야 합니다.

---
## 예제 - COUNT 함수 사용
GROUP BY 절을 [COUNT 함수](COUNT.md)와 함께 사용하는 방법을 살펴보겠습니다.

이 GROUP BY 예제에서는 COUNT 함수를 사용하여 카테고리와 해당 카테고리에서 45개 이상의 available_products를 보유한 공급업체 수를 반환합니다.
```SQL
SELECT category, COUNT(*) AS "Number of suppliers"
FROM suppliers
WHERE available_products > 45
GROUP BY category;
```

---
## 예제 - MIN 함수 사용
다음으로 GROUP BY 절을 [MIN 함수](MIN.md)와 함께 사용하는 방법을 살펴보겠습니다.

이 GROUP BY 예제에서는 MIN 함수를 사용하여 각 부서와 부서의 최소 급여를 반환합니다.
```SQL
SELECT department, MIN(salary) AS "Lowest salary"
FROM employees
GROUP BY department;
```

---
## 예제 - MAX 함수 사용
마지막으로 [MAX 함수](MAX.md)와 함께 GROUP BY 절을 사용하는 방법을 살펴보겠습니다.

이 GROUP BY 예제는 MAX 함수를 사용하여 각 부서와 해당 부서의 최대 급여를 반환합니다.
```SQL
SELECT department, MAX(salary) AS "Highest salary"
FROM employees
GROUP BY department;
```

---
**[< 이전](EXISTS.md) / [다음 : HAVING >](HAVING.md)**