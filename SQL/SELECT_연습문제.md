# SQL : SELECT 문 연습 문제
SQL SELECT 문을 사용하여 자신의 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.  
이러한 연습 문제를 통해 SELECT 문을 사용하여 실력을 테스트할 수 있습니다.  
각 연습이 끝나면 정답을 확인할 수 있도록 해답이 제공됩니다.

시작하세요!
### [튜토리얼로 돌아가기](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT_튜토리얼.md)

#
## 연습 문제 #1
아래 employees 테이블을 기준으로 employees 테이블에서 salary가 $52,500 이하인 모든 필드를 선택합니다. (정렬할 필요 없음)
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
다음 SQL SELECT 문은 employees 테이블에서 이러한 레코드를 선택합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT *
FROM employees
WHERE salary <= 52500;
```
다음은 표시되는 결과입니다.

| employee_number | last_name | first_name | salary | dept_id |
| --------------- | --------- | ---------- | ------ | ------- |
| 1004            | Horvath   | Jack       | 42000  | 501     |

#
## 연습 문제 #2
아래 suppliers 테이블을 기준으로 'California' state에 있는 고유한 city 값을 선택하고 결과를 city 별로 내림차순으로 정렬합니다.
```SQL
CREATE TABLE suppliers
( supplier_id int NOT NULL,
  supplier_name char(50) NOT NULL,
  city char(50),
  state char(25),
  CONSTRAINT suppliers_pk PRIMARY KEY (supplier_id)
);

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(100, 'Microsoft', 'Redmond', 'Washington');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(200, 'Google', 'Mountain View', 'California');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(300, 'Oracle', 'Redwood City', 'California');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(400, 'Kimberly-Clark', 'Irving', 'Texas');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(500, 'Tyson Foods', 'Springdale', 'Arkansas');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(600, 'SC Johnson', 'Racine', 'Wisconsin');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(700, 'Dole Food Company', 'Westlake Village', 'California');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(800, 'Flowers Foods', 'Thomasville', 'Georgia');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(900, 'Electronic Arts', 'Redwood City', 'California');
```

### 연습 문제 #2 풀이
다음 SELECT 문은 suppliers 테이블에서 이러한 레코드를 선택합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT DISTINCT city
FROM suppliers
WHERE state = 'California'
ORDER BY city DESC;
```
다음은 표시되는 결과입니다.

| city             |
| ---------------- |
| Westlake Village |
| Redwood City     |
| Mountain View    |

#
## 연습 문제 #3
아래의 customers 테이블과 orders 테이블을 기준으로 customers 테이블에서 customer_id 및 last_name을 선택하고,  
customers 테이블과 orders 테이블 모두에 일치하는 customer_id 값이 있는 orders 테이블에서 order_date를 선택합니다.  
결과를 customer_id별로 내림차순으로 정렬합니다.
```SQL
CREATE TABLE customers
( customer_id int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  favorite_website char(50),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);

CREATE TABLE orders
( order_id int NOT NULL,
  customer_id int,
  order_date date,
  CONSTRAINT orders_pk PRIMARY KEY (order_id)
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

INSERT INTO orders
(order_id, customer_id, order_date)
VALUES
(1,7000,'2016/04/18');

INSERT INTO orders
(order_id, customer_id, order_date)
VALUES
(2,5000,'2016/04/18');

INSERT INTO orders
(order_id, customer_id, order_date)
VALUES
(3,8000,'2016/04/19');

INSERT INTO orders
(order_id, customer_id, order_date)
VALUES
(4,4000,'2016/04/20');

INSERT INTO orders
(order_id, customer_id, order_date)
VALUES
(5,null,'2016/05/01');
```

### 연습 문제 #3 풀이
다음 SQL SELECT 문은 고객 및 주문 테이블에서 이러한 레코드를 선택합니다. ([INNER JOIN](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/INNER_JOIN_튜토리얼.md) 사용) **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT customers.customer_id, customers.last_name, orders.order_date
FROM customers 
INNER JOIN orders
ON customers.customer_id = orders.customer_id
ORDER BY customers.customer_id DESC;
```
다음은 표시되는 결과입니다.

| customer_id | last_name | order_date |
| ----------- | --------- | ---------- |
| 8000        | Anderson  | 2016/04/19 |
| 5000        | Smith     | 2016/04/18 |
| 7000        | Reynolds  | 2016/04/18 |
| 4000        | Jackson   | 2016/04/20 |

#
## 연습 문제 #4
연습 문제 #3의 customers 및 orders 테이블을 기반으로,  
customers 테이블에서 orders 테이블에 해당 customer_id에 대한 레코드가 있는 customer_id 및 last_name을 선택합니다.  
결과를 last_name 순으로 오름차순으로 정렬한 다음 customer_id 순으로 내림차순으로 정렬합니다.
```SQL
CREATE TABLE customers
( customer_id int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  favorite_website char(50),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);

CREATE TABLE orders
( order_id int NOT NULL,
  customer_id int,
  order_date date,
  CONSTRAINT orders_pk PRIMARY KEY (order_id)
);
```

### 연습 문제 #4 풀이
다음 SQL SELECT 문은 customers 및 orders 테이블에서 레코드를 선택합니다. ([SQL EXISTS 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/EXISTS_튜토리얼.md) 사용) **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT customer_id, last_name
FROM customers
WHERE EXISTS
  ( SELECT orders.customer_id
    FROM orders
    WHERE orders.customer_id = customers.customer_id )
ORDER BY last_name ASC, customer_id DESC;
```
또는 [ORDER BY 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/ORDER_BY_튜토리얼.md)에서 customer_name에 대한 ASC 키워드를 제외할 수도 있습니다. 두 SELECT 문 모두 동일한 결과를 생성합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT customer_id, last_name
FROM customers
WHERE EXISTS
  ( SELECT orders.customer_id
    FROM orders
    WHERE orders.customer_id = customers.customer_id )
ORDER BY last_name, customer_id DESC;
```
다음은 표시되는 결과입니다.

| customer_id | last_name |
| ----------- | --------- |
| 8000        | Anderson  |
| 4000        | Jackson   |
| 7000        | Reynolds  |
| 5000        | Smith     |

#
### [튜토리얼로 돌아가기](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT_튜토리얼.md)