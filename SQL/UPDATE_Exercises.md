# SQL : UPDATE 문 연습 문제

SQL UPDATE 문을 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습 문제를 통해 UPDATE 문 사용 실력을 테스트할 수 있습니다.  
각 연습이 끝나면 정답을 확인할 수 있도록 풀이가 제공됩니다.

시작하세요!

**[튜토리얼로 돌아가기](UPDATE.md)**

---
## 연습 문제 #1
다음 데이터로 채워진 products 테이블을 기반으로 product_name이 'Apple'인 모든 레코드에 대해 product_name을 'Grapefruit'으로 업데이트합니다.
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
다음 SQL UPDATE 문은 이 업데이트를 수행합니다. **[Try it](https://www.techonthenet.com/sql/update_try_sql.php)**
```SQL
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_name = 'Apple';
```
이제 products 테이블은 다음과 같이 표시됩니다.

| product_id | product_name   | category_id |
| :--------- | :------------- | :---------- |
| 1          | Pear           | 50          |
| 2          | Banana         | 50          |
| 3          | Orange         | 50          |
| 4          | **Grapefruit** | 50          |
| 5          | Bread          | 75          |
| 6          | Sliced Ham     | 25          |
| 7          | Kleenex        | NULL        |

---
## 연습 문제 #2
다음 데이터로 채워진 suppliers 테이블을 기반으로 supplier_name이 "Microsoft"인 모든 레코드에 대해 city를 'Boise'로, state를 'Idaho'로 업데이트합니다.
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
다음 SQL UPDATE 문은 SQL에서 이 업데이트를 수행합니다. **[Try it](https://www.techonthenet.com/sql/update_try_sql.php)**
```SQL
UPDATE suppliers
SET city = 'Boise',
state = 'Idaho'
WHERE supplier_name = 'Microsoft';
```
이제 suppliers 테이블은 다음과 같이 표시됩니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 100         | Microsoft         | **Boise**        | **Idaho**  |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

---
**[튜토리얼로 돌아가기](UPDATE.md)**