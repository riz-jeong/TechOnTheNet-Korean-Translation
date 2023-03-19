# SQL : GROUP BY 절

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **GROUP BY 절**을 사용하는 방법을 설명합니다.

## 설명
[SELECT 문](SELECT.md)에서 SQL GROUP BY 절을 사용하여 여러 레코드에서 데이터를 수집하고 하나 이상의 열을 기준으로 결과를 그룹화할 수 있습니다.

## 구문
SQL에서 GROUP BY 절의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n, 
       aggregate_function (aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n
[ORDER BY expression [ ASC | DESC ]];
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- 집계 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_function**
- [SUM](SUM.md), [COUNT](COUNT.md), [MIN](MIN.md), [MAX](MAX.md), [AVG](AVG.md) 함수와 같은 집계 함수입니다.
#### **aggregate_expression**
- aggregate_function이 사용될 열 또는 표현식입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하려면 반드시 충족해야 하는 조건입니다.
#### **ORDER BY expression**
- 선택 사항입니다. 결과 집합의 레코드를 정렬하는 데 사용되는 표현식입니다. 둘 이상의 표현식을 제공하는 경우 값을 쉼표로 구분해야 합니다.
#### **ASC**
- 선택 사항입니다. ASC는 결과 집합을 표현식별로 오름차순으로 정렬합니다. 작성하지 않은 경우 기본 동작입니다.
#### **DESC**
- 선택 사항입니다. DESC는 결과 집합을 표현식별로 내림차순으로 정렬합니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/group_by_ddl.php)**

---
## 예제 - SUM 함수와 함께 GROUP BY 사용
SQL에서 [SUM 함수](SUM.md)와 함께 GROUP BY 절을 사용하는 방법을 살펴 보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 employees라는 테이블이 있습니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT dept_id, SUM(salary) AS total_salaries
FROM employees
GROUP BY dept_id;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| dept_id | total_salaries |
| :------ | :------------- |
| 500     | 119500         |
| 501     | 113000         |

이 예제에서는 SUM 함수를 사용하여 각 dept_id에 대한 모든 급여를 더하고 SUM 함수의 결과를 total_salaries로 [별칭](ALIASES.md)을 지정했습니다. dept_id는 SUM 함수에 캡슐화되어 있지 않으므로 GROUP BY 절에 나열되어야 합니다.

---
## 예제 - 카운트 함수와 함께 GROUP BY 사용
SQL에서 [COUNT 함수](COUNT.md)와 함께 GROUP BY 절을 사용하는 방법을 살펴 보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 products라는 테이블이 있습니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT category_id, COUNT(*) AS total_products
FROM products
WHERE category_id IS NOT NULL
GROUP BY category_id
ORDER BY category_id;
```
3개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| category_id | total_products |
| :---------- | :------------- |
| 25          | 1              |
| 50          | 4              |
| 75          | 1              |

이 예제에서는 COUNT 함수를 사용하여 각 category_id에 대한 제품 수를 계산하고 COUNT 함수의 결과를 total_products로 [별칭](ALIASES.md)을 지정했습니다. NULL인 category_id 값은 WHERE 절에서 필터링하여 제외했습니다. category_id는 COUNT 함수에 캡슐화되어 있지 않으므로 GROUP BY 절에 나열되어야 합니다.

---
## 예제 - MIN 함수와 함께 GROUP BY 사용
다음으로 SQL에서 [MIN 함수](MIN.md)와 함께 GROUP BY 절을 사용하는 방법을 살펴보겠습니다.

이 예제에서는 다음 데이터로 채워진 employees 테이블을 다시 사용합니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT dept_id, MIN(salary) AS lowest_salary
FROM employees
GROUP BY dept_id;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| dept_id | lowest_salary |
| :------ | :------------ |
| 500     | 57500         |
| 501     | 42000         |

이 예제에서는 MIN 함수를 사용하여 각 dept_id에 대한 최저 급여를 반환하고 MIN 함수의 결과를 lowest_salary로 [별칭](ALIASES.md)을 지정했습니다. dept_id는 MIN 함수에 캡슐화되어 있지 않으므로 GROUP BY 절에 나열되어야 합니다.

---
## - MAX 함수와 함께 GROUP BY 사용
마지막으로 [MAX 함수](MAX.md)와 함께 GROUP BY 절을 사용하는 방법을 살펴보겠습니다.

employees 테이블을 다시 사용하되 이번에는 각 dept_id에 대한 최고 급여를 찾아보겠습니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT dept_id, MAX(salary) AS highest_salary
FROM employees
GROUP BY dept_id;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| dept_id | highest_salary |
| :------ | :------------- |
| 500     | 62000          |
| 501     | 71000          |

이 예제에서는 MAX 함수를 사용하여 각 dept_id에 대해 가장 높은 급여를 반환하고 MAX 함수의 결과를 highest_salary로 [별칭](ALIASES.md)을 지정했습니다. dept_id 열은 MAX 함수에 캡슐화되어 있지 않으므로 GROUP BY 절에 나열되어야 합니다.

---
**[< 이전](EXISTS.md) / [다음 : COUNT >](COUNT.md)**