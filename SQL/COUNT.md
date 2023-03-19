# SQL : COUNT 함수

이 SQL 튜토리얼에서는 구문, 예제 및 [연습 문제](COUNT_Exercises.md)를 통해 SQL **COUNT 함수**를 사용하는 방법을 설명합니다.

## 설명
SQL COUNT 함수는 SELECT 문에서 반환되는 행 수를 계산하는 데 사용됩니다.

## 구문
SQL에서 COUNT 함수의 구문은 다음과 같습니다.
```SQL
SELECT COUNT(aggregate_expression)
FROM tables
[WHERE conditions]
[ORDER BY expression [ ASC | DESC ]];
```
또는 하나 이상의 열을 기준으로 결과를 그룹화할 때 COUNT 함수의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n,
       COUNT(aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n
[ORDER BY expression [ ASC | DESC ]];
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- COUNT 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_expression**
- 널이 아닌 값을 계산할 열 또는 표현식입니다.
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

**[DDL/DML 받기](https://www.techonthenet.com/sql/count_ddl.php)**

---
## 예제 - COUNT 함수에는 NOT NULL 값만 포함됩니다
모든 사람이 이 사실을 알고 있는 것은 아니지만, COUNT 함수는 COUNT(expression)에서 표현식이 NULL이 아닌 레코드만 카운트합니다. 표현식이 NULL 값인 경우, 해당 표현식은 COUNT 계산에 포함되지 않습니다. 이에 대해 자세히 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

COUNT 함수를 사용하는 다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/count_try_sql.php)**
```SQL
SELECT COUNT(customer_id)
FROM customers;
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| COUNT(customer_id) |
| :----------------- |
| 6                  |

이 예제에서는 customers 테이블에 6개의 레코드가 있고 모든 customer_id 값이 NULL이 아니므로(즉, customer_id가 테이블의 기본 키임) 쿼리에서 6을 반환합니다.

하지만 COUNT 함수에 NULL 값이 발생하면 어떻게 될까요? NULL 값을 포함할 수 있는 favorite_website 열을 카운트하는 다음 SELECT 문을 입력해 보겠습니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT COUNT(favorite_website)
FROM customers;
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| COUNT(favorite_website) |
| :---------------------- |
| 5                       |

이 두 번째 예제에서는 5를 반환합니다. favorite_website 값 중 하나가 NULL이므로 COUNT 함수 계산에서 제외됩니다. 결과적으로 쿼리는 6이 아닌 5를 반환합니다.

>팁: 계산에서 레코드가 제외되지 않도록 하려면 COUNT 함수의 기본 키를 사용하거나 COUNT(*)를 사용합니다.

---
## 예제 - COUNT 함수에서 단일 표현식 사용
쿼리에서 단일 표현식으로 COUNT 함수를 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 employees라는 테이블이 있습니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT COUNT(*) AS total
FROM employees
WHERE salary > 50000;
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| total |
| :---- |
| 3     |

이 예제에서는 salary가 $50,000 이상인 직원 수를 반환합니다. 쿼리 결과를 더 읽기 쉽게 만들기 위해 COUNT(*)의 [별칭](ALIASES.md)을 total로 지정했습니다. 이제 결과 집합이 반환될 때 열 제목으로 total이 표시됩니다.

---
## 예제 - COUNT 함수와 함께 GROUP BY 사용
경우에 따라 COUNT 함수와 함께 [GROUP BY 절](GROUP_BY.md)을 사용해야 하는 경우가 있습니다. 이는 SELECT 문에 COUNT 함수의 일부가 아닌 열이 나열된 경우 발생합니다. 이에 대해 자세히 살펴보겠습니다.

다시 다음 데이터로 채워진 employees 테이블을 사용합니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT dept_id, COUNT(*) AS total
FROM employees
WHERE salary > 50000
GROUP BY dept_id;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| dept_id | total |
| :------ | :---- |
| 500     | 2     |
| 501     | 1     |

이 예제에서 COUNT 함수는 각 dept_id에 대해 $50,000 이상을 버는 직원 수를 반환합니다. dept_id 열은 COUNT 함수에 포함되지 않으므로 [GROUP BY 절](GROUP_BY.md)에 열을 나열해야 합니다.

---
## 예제 - 카운트 함수와 함께 DISTINCT 사용
COUNT 함수 내에서 [DISTINCT 절](DISTINCT.md)을 사용할 수 있다는 사실을 알고 계셨나요? 이를 통해 고유한 값만 계산할 수 있습니다.

이전 예제와 동일한 employees 테이블을 사용합니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT COUNT(DISTINCT dept_id) AS total
FROM employees
WHERE salary > 50000;
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| total |
| :---- |
| 2     |

이 예제에서 COUNT 함수는 $50,000 이상의 salary를 가진 직원이 1명 이상 있는 dept_id 값의 고유 수를 반환합니다.

---
## 팁: COUNT 함수을 사용한 성능 튜닝
COUNT 함수는 COUNT 함수 매개변수(즉, 괄호 안)로 포함하는 NOT NULL 필드에 관계없이 동일한 결과를 반환하므로, 카운트(1)을 사용하면 더 나은 성능을 얻을 수 있습니다. 이제 데이터베이스 엔진은 데이터 필드를 가져올 필요 없이 1이라는 정수 값만 검색합니다.

예를 들어, 이 구문을 입력하는 대신에 **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT dept_id, COUNT(*) AS total
FROM employees
WHERE salary > 50000
GROUP BY dept_id;
```
더 나은 성능을 얻으려면 카운트(*)를 카운트(1)로 대체할 수 있습니다. **[Try it](https://www.techonthenet.com/sql/group_by_try_sql.php)**
```SQL
SELECT dept_id, COUNT(1) AS total
FROM employees
WHERE salary > 50000
GROUP BY dept_id;
```
이제 COUNT 함수는 COUNT(*) 구문을 사용할 때처럼 employees 테이블에서 모든 필드를 검색할 필요가 없습니다. 기준을 충족하는 각 레코드에 대해 1이라는 숫자 값만 검색합니다.

---
## 연습 문제
SQL COUNT 함수를 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습을 통해 COUNT 함수를 사용하여 자신의 실력을 시험해 볼 수 있습니다. 풀어야 하는 문제가 주어집니다. 각 연습이 끝나면 답을 확인할 수 있도록 솔루션을 제공합니다. 한번 도전해 보세요!

**[연습 문제로 이동](COUNT_Exercises.md)**

---
**[< 이전](GROUP_BY.md) / [다음 : SUM >](SUM.md)**