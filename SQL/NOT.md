# SQL : NOT 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **NOT 조건**을 사용하는 방법을 설명합니다.

## 설명
SQL NOT 조건(NOT 연산자라고도 함)은 SELECT, INSERT, UPDATE, DELETE 문의 WHERE 절에서 조건을 부정하는 데 사용됩니다.

## 구문
SQL에서 NOT 조건의 구문은 다음과 같습니다.
```SQL
NOT condition
```
### 매개변수 및 예제
#### **condition(조건)**
- 이것이 부정할 조건입니다. 레코드가 결과 집합에 포함되려면 조건의 반대가 충족되어야 합니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/not_ddl.php)**

---
## 예제 - IN 조건에 NOT 사용
먼저 IN 조건에 NOT 연산자를 사용하는 방법부터 살펴보겠습니다. [IN 조건](IN.md)과 함께 NOT 연산자를 사용하면 NOT IN 조건이 생성됩니다. 이렇게 하면 표현식이 목록에 없는지 테스트합니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/not_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_name NOT IN ('Pear', 'Banana', 'Bread');
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

이 예제에서는 products 테이블에서 product_name이 Pear, Banana, Bread가 아닌 모든 행을 반환합니다. 때로는 원하는 값과 반대로 원하지 않는 값을 나열하는 것이 더 효율적일 수 있습니다.

이는 다음 SQL 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/not_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_name <> 'Pear'
AND product_name <> 'Banana'
AND product_name <> 'Bread';
```

---
## 예제 - IS NULL 조건에 NOT 사용
NOT 연산자를 [IS NULL 조건](IS_NULL.md)과 결합하면 NULL이 아닌 값을 테스트할 수 있는 IS NOT NULL 조건이 만들어집니다. 이 연산자는 NULL이 아닌 값을 테스트할 때 SQL에서 사용하도록 권장되는 [비교 연산자](Comparison_Operators.md)입니다. 쿼리에서 IS NOT NULL 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이전 예제와 동일한 products 테이블을 사용합니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/not_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE category_id IS NOT NULL;
```

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |

이 예제에서는 customer_id에 NULL 값이 포함되지 않은 products 테이블의 모든 레코드를 반환합니다.

---
## 예제 - LIKE 조건과 함께 NOT 사용
다음으로 [LIKE 조건](LIKE.md)과 함께 NOT 연산자를 사용하는 방법의 예를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 100         | Microsoft         | Redmond          | Washington |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

suppliers 테이블에서 supplier_name에 문자 'o'가 포함되지 **않은** 모든 레코드를 찾아보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/not_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name NOT LIKE '%o%';
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name  | city   | state |
| :---------- | :------------- | :----- | :---- |
| 400         | Kimberly-Clark | Irving | Texas |

이 예제에서는 suppliers 테이블에 supplier_name에 문자 'o'가 포함되지 않은 레코드가 하나만 있습니다.

---
## 예제 - BETWEEN 조건과 함께 NOT 사용
NOT 연산자를 [BETWEEN 조건](BETWEEN.md)과 결합하여 NOT BETWEEN 조건을 만들 수도 있습니다. 쿼리에서 NOT BETWEEN 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SQL 문을 입력합니다.
```SQL
SELECT *
FROM customers
WHERE customer_id NOT BETWEEN 5000 AND 8000;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website |
| :---------- | :-------- | :--------- | :--------------- |
| 4000        | Jackson   | Joe        | techonthenet.com |
| 9000        | Johnson   | Derek      | techonthenet.com |

이렇게 하면 customer_id가 5000에서 8000 사이가 아닌 모든 행이 반환됩니다. 이는 다음 SELECT 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/not_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id < 5000
OR customer_id > 8000;
```

---
## 예제 - EXISTS 조건과 함께 NOT 사용
마지막으로 NOT 조건을 [EXISTS 조건](EXISTS.md)과 결합하여 NOT EXISTS 조건을 만들 수 있습니다. SQL에서 NOT EXISTS 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

그리고 다음 데이터가 있는 orders라는 테이블이 있습니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/not_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE NOT EXISTS
  (SELECT * 
   FROM orders
   WHERE customers.customer_id = orders.customer_id);
```

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이 예제에서는 orders 테이블에 지정된 customer_id에 대한 레코드가 없는 customers 테이블의 모든 레코드를 반환합니다.

---
**[< 이전](LIKE.md) / [다음 : ALIASES >](ALIASES.md)**