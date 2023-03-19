# SQL : COUNT 함수 연습 문제

SQL COUNT 함수를 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습 문제를 통해 COUNT 함수로 실력을 테스트할 수 있습니다.  
각 연습이 끝나면 정답을 확인할 수 있도록 풀이가 제공됩니다.

시작하세요!

**[튜토리얼로 돌아가기](COUNT.md)**

---
## 연습 문제 #1
다음 데이터로 채워진 products 테이블을 기준으로 category_id가 50인 제품 수를 계산합니다.
```SQL
CREATE TABLE products
( product_id int NOT NULL,
  product_name char(50) NOT NULL,
  category_id int,
  CONSTRAINT products_pk PRIMARY KEY (product_id)
);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(1,'Pear',50);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(2,'Banana',50);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(3,'Orange',50);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(4,'Apple',50);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(5,'Bread',75);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(6,'Sliced Ham',25);

INSERT INTO products
(product_id, product_name, category_id)
VALUES
(7,'Kleenex',null);
```

### 연습 문제 #1 풀이
성능 측면에서는 비효율적이지만 다음 SQL SELECT 문은 category_id가 50인 제품 수를 반환합니다. **[Try it](https://www.techonthenet.com/sql/count_try_sql.php)**
```SQL
SELECT COUNT(*) AS total
FROM products
WHERE category_id = 50;
```
다음은 표시되는 결과입니다.

| total |
| :---- |
| 4     |

동일한 솔루션을 보다 효율적으로 구현하는 방법은 다음과 같은 SELECT 문을 사용하는 것입니다. **[Try it](https://www.techonthenet.com/sql/count_try_sql.php)**
```SQL
SELECT COUNT(1) AS total
FROM products
WHERE category_id = 50;
```
이제 SQL COUNT 함수는 테이블에서 모든 필드(예: employee_number, employee_name, salary)를 검색할 필요 없이 조건이 충족될 때마다 숫자 값 1을 검색합니다. 따라서 SQL 문의 성능이 향상됩니다.

---
## 연습 문제 #2
다음 데이터로 채워진 suppliers 테이블을 기반으로 suppliers 테이블에 있는 고유한 city 값의 수를 계산합니다.
```SQL
CREATE TABLE suppliers
( supplier_id int NOT NULL,
  supplier_name char(50) NOT NULL,
  city char(50),
  state char(50),
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
**[Try it](https://www.techonthenet.com/sql/count_try_sql.php)**
```SQL
SELECT COUNT(DISTINCT city) AS total
FROM suppliers;
```
다음은 표시되는 결과입니다.

| total |
| :---- |
| 8     |

---
## 연습 문제 #3
다음 데이터로 채워진 orders 테이블을 기준으로 orders 테이블의 각 order_date에 대한 주문 수를 계산합니다.
```SQL
CREATE TABLE orders
( order_id int NOT NULL,
  customer_id int,
  order_date date,
  CONSTRAINT orders_pk PRIMARY KEY (order_id)
);

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
다음 SELECT 문은 orders 테이블의 각 order_date에 대한 주문 수를 반환합니다. **[Try it](https://www.techonthenet.com/sql/count_try_sql.php)**
```SQL
SELECT order_date, COUNT(*) AS total
FROM orders
GROUP BY order_date;
```
다음은 표시되는 결과입니다.

| order_date | total |
| :--------- | :---- |
| 2016/04/18 | 2     |
| 2016/04/19 | 1     |
| 2016/04/20 | 1     |
| 2016/05/01 | 1     |

동일한 솔루션을 보다 효율적으로 구현하는 방법은 다음과 같은 SELECT 문을 사용하는 것입니다. **[Try it](https://www.techonthenet.com/sql/count_try_sql.php)**
```SQL
SELECT order_date, COUNT(1) AS total
FROM orders
GROUP BY order_date;
```

---
**[튜토리얼로 돌아가기](COUNT.md)**