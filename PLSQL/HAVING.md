# Oracle / PLSQL : HAVING 절

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **HAVING 절**을 사용하는 방법을 설명합니다.

## 설명
Oracle HAVING 절은 GROUP BY 절과 함께 사용하여 반환되는 행의 그룹을 조건이 TRUE인 행으로만 제한하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 HAVING 절의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n, 
       aggregate_function (aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n
HAVING having_condition;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- 집계 함수 내에 캡슐화되지 않은 표현식이며 GROUP BY 절에 포함되어야 하는 표현식입니다.
#### **aggregate_function**
- SUM, COUNT, MIN, MAX 또는 AVG 함수와 같은 함수일 수 있습니다.
#### **aggregate_expression**
- aggregate_function가 사용될 열 또는 표현식입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 하나 이상의 테이블이 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 선택할 레코드에 대한 조건입니다.
#### **having_condition**
- 반환되는 행의 그룹을 제한하기 위해 집계된 결과에만 적용되는 추가 조건입니다. 조건이 TRUE로 평가되는 그룹만 결과 집합에 포함됩니다.

---
## 예제 - SUM 함수 사용
[SUM 함수](SUM.md)를 사용하는 Oracle HAVING 절의 예를 살펴보겠습니다.

[SUM 함수](SUM.md)를 사용하여 각 부서와 연결된 부서의 총 매출을 반환할 수도 있습니다. Oracle HAVING 절은 매출액이 $25,000보다 큰 부서만 반환되도록 결과를 필터링합니다.
```SQL
SELECT department, SUM(sales) AS "Total sales"
FROM order_details
GROUP BY department
HAVING SUM(sales) > 25000;
```

---
## 예제 - COUNT 함수 사용
HAVING 절을 [COUNT 함수](COUNT.md)와 함께 사용하는 방법을 살펴봅시다.

[COUNT 함수](COUNT.md)를 사용하여 각 부서 이름과 연봉이 $49,500 미만인 관련 부서의 직원 수 를 반환할 수 있습니다. Oracle HAVING 절은 직원이 10명 이상인 부서만 반환되도록 결과를 필터링합니다.
```SQL
SELECT department, COUNT(*) AS "Number of employees"
FROM employees
WHERE salary < 49500
GROUP BY department
HAVING COUNT(*) > 10;
```

---
## 예제 - MIN 함수 사용
이제 [MIN 함수](MIN.md)와 함께 HAVING 절을 사용하는 방법을 살펴보겠습니다.

[MIN 함수](MIN.md)를 사용하여 각 부서와 해당 부서의 최소 급여를 반환할 수도 있습니다. Oracle HAVING 절은 최저 급여가 $42,000 미만인 부서만 반환합니다.
```SQL
SELECT department, MIN(salary) AS "Lowest salary"
FROM employees
GROUP BY department
HAVING MIN(salary) < 42000;
```

---
## 예제 - MAX 함수 사용
마지막으로 [MAX 함수](MAX.md)와 함께 HAVING 절을 사용하는 방법을 살펴보겠습니다.
예를 들어 [MAX 함수](MAX.md)를 사용하여 각 부서와 해당 부서의 최대 급여를 반환할 수도 있습니다. Oracle HAVING 절은 최대 급여가 $45,000보다 큰 부서만 반환합니다.
```SQL
SELECT department, MAX(salary) AS "Highest salary"
FROM employees
GROUP BY department
HAVING MAX(salary) > 45000;
```

---
**[< 이전](GROUP_BY.md) / [다음 : UNION >](UNION.md)**