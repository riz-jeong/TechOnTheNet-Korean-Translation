# SQL : MIN 함수

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **MIN 함수**를 사용하는 방법을 설명합니다.

## 설명
SQL MIN 함수는 SELECT 문에서 식의 최소값을 반환하는 데 사용됩니다.

## 구문
SQL에서 MIN 함수의 구문은 다음과 같습니다.
```SQL
SELECT MIN(aggregate_expression)
FROM tables
[WHERE conditions];
```
또는 하나 이상의 열을 기준으로 결과를 그룹화할 때 MIN 함수의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n,
       MIN(aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n
- MIN 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_expression
- 최소값이 반환될 열 또는 표현식입니다.
#### **tables
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)
- 선택 사항입니다. 레코드를 선택하려면 반드시 충족해야 하는 조건입니다.

---
## 예제 - 단일 표현식 사용
SQL MIN 함수를 사용하는 가장 간단한 방법은 MIN 값을 계산하는 단일 필드를 반환하는 것입니다.

예를 들어 모든 직원의 최저 급여를 알고 싶을 수 있습니다.
```SQL
SELECT MIN(salary) AS "Lowest salary"
FROM employees;
```
이 SQL MIN 함수 예제에서는 MIN(salary) 필드의 [별칭](ALIASES.md)을 "Lowest salary"로 지정했습니다. 결과적으로 결과 집합이 반환될 때 "Lowest salary"가 필드 이름으로 표시됩니다.

---
## 예제 - SQL GROUP BY 사용
경우에 따라 SQL [GROUP BY 절](GROUP_BY.md)을 SQL MIN 함수와 함께 사용해야 할 수도 있습니다.

예를 들어 SQL MIN 함수를 사용하여 각 부서의 이름과 해당 부서의 최소 급여를 반환할 수도 있습니다.
```SQL
SELECT department, MIN(salary) AS "Lowest salary"
FROM employees
GROUP BY department;
```
SQL [SELECT 문](SELECT.md)에 SQL MIN 함수에 캡슐화되지 않은 열 하나를 나열했기 때문에 SQL [GROUP BY 절](GROUP_BY.md)을 사용해야 합니다. 따라서 부서 필드는 GROUP BY 섹션에 나열되어야 합니다.

---
**[< 이전](MAX.md) / [다음 : AVG >](AVG.md)**