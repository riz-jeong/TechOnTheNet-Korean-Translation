# SQL : LIKE 조건 연습 문제

SQL LIKE 조건을 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습 문제를 통해 LIKE 조건을 사용하여 실력을 테스트할 수 있습니다.  
각 연습이 끝나면 정답을 확인할 수 있도록 풀이가 제공합니다.

시작하세요!

**[튜토리얼로 돌아가기](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/LIKE.md)**

---
## 연습 문제 #1
다음 데이터로 채워진 employees 테이블을 기반으로 last_name에 문자 'h'가 포함된 모든 레코드를 찾습니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  salary int,
  dept_id int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1001, 'Smith', 'John', 62000, 500);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1002, 'Anderson', 'Jane', 57500, 500);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1003, 'Everest', 'Brad', 71000, 501);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1004, 'Horvath', 'Jack', 42000, 501);
```

### 연습 문제 #1 풀이
다음 SELECT 문은 LIKE 조건을 사용하여 last_name에 문자 "h"가 포함된 레코드를 반환합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM 
WHERE last_name LIKE '%h%';
```
그러면 다음과 같은 결과 집합이 반환됩니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

---
## 연습 문제 #2
다음 데이터로 채워진 employees 테이블을 기반으로 first_name이 문자 'B'로 시작하는 모든 레코드를 찾습니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  salary int,
  dept_id int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1001, 'Smith', 'John', 62000, 500);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1002, 'Anderson', 'Jane', 57500, 500);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1003, 'Everest', 'Brad', 71000, 501);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1004, 'Horvath', 'Jack', 42000, 501);
```
### 연습 문제 #2 풀이
다음 SELECT 문은 LIKE 조건을 사용하여 first_name이 문자 "B"로 시작하는 레코드를 반환합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM employees
WHERE first_name LIKE 'B%';
```
그러면 다음과 같은 결과 집합이 반환됩니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1003            | Everest   | Brad       | 71000  | 501     |

---
## 연습 문제 #3
다음 데이터로 채워진 customers 테이블을 기반으로 first_name이 4자리 길이고 'J'로 시작하는 모든 고객을 찾습니다.
```SQL
CREATE TABLE customers
( customer_id int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  favorite_website char(50),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);

INSERT INTO customers
(customer_id, last_name, first_name, favorite_website)
VALUES
(4000, 'Jackson', 'Joe', 'techonthenet.com');

INSERT INTO customers
(customer_id, last_name, first_name, favorite_website)
VALUES
(5000, 'Smith', 'Jane', 'digminecraft.com');

INSERT INTO customers
(customer_id, last_name, first_name, favorite_website)
VALUES
(6000, 'Ferguson', 'Samantha', 'bigactivities.com');

INSERT INTO customers
(customer_id, last_name, first_name, favorite_website)
VALUES
(7000, 'Reynolds', 'Allen', 'checkyourmath.com');

INSERT INTO customers
(customer_id, last_name, first_name, favorite_website)
VALUES
(8000, 'Anderson', 'Paige', NULL);

INSERT INTO customers
(customer_id, last_name, first_name, favorite_website)
VALUES
(9000, 'Johnson', 'Derek', 'techonthenet.com');
```
### 연습 문제 #2 풀이
다음 SELECT 문은 LIKE 조건을 사용하여 first_name이 4자리 길이고 "J"로 시작하는 레코드를 반환합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE first_name LIKE 'J___';
```
그러면 다음과 같은 결과 집합이 반환됩니다.

| customer_id | last_name | first_name | favorite_website |
| :---------- | :-------- | :--------- | :--------------- |
| 5000        | Smith     | Jane       | digminecraft.com |

---
**[튜토리얼로 돌아가기](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/LIKE.md)**