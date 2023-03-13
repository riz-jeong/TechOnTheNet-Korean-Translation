# SQL : IS NOT NULL 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **IS NOT NULL 조건**을 사용하는 방법을 설명합니다.

## 설명
IS NOT NULL 조건은 SQL에서 NULL이 아닌 값을 테스트하는 데 사용됩니다. NULL이 아닌 값이 발견되면 TRUE를 반환하고, 그렇지 않으면 FALSE를 반환합니다. 이 조건은 SELECT, INSERT, UPDATE 또는 DELETE 문에서 사용할 수 있습니다.

## 구문
SQL에서 IS NOT NULL 조건의 구문은 다음과 같습니다.
```SQL
expression IS NOT NULL
```
### 매개변수 및 인수
#### **expression(표현식)**
- NOT NULL 값을 테스트할 표현식입니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/is_not_null_ddl.php)**

---
## 예제 - SELECT 문과 함께 IS NOT NULL 사용
NULL이 아닌 값을 테스트할 때 SQL에서 사용하는 것이 권장되는 [비교 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/Comparison_Operators.md)는 IS NOT NULL입니다. 먼저 [SELECT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT.md)에서 IS NOT NULL 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 products라는 테이블이 있습니다:

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/is_not_null_sql.php)**
```SQL
SELECT *
FROM products
WHERE category_id IS NOT NULL;
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

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
## 예제 - UPDATE 문과 함께 IS NOT NULL 사용
다음으로 [UPDATE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/UPDATE.md)에서 IS NOT NULL 조건을 사용하는 방법의 예를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 UPDATE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/is_not_null_sql.php)**
```SQL
UPDATE customers
SET favorite_website = 'techonthenet.com'
WHERE favorite_website IS NOT NULL;
```
레코드 5개가 업데이트됩니다. customers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM customers;
```
아래가 표시되는 결과입니다.


| customer_id | last_name | first_name | favorite_website     |
| :---------- | :-------- | :--------- | :------------------- |
| 4000        | Jackson   | Joe        | **techonthenet.com** |
| 5000        | Smith     | Jane       | **techonthenet.com** |
| 6000        | Ferguson  | Samantha   | **techonthenet.com** |
| 7000        | Reynolds  | Allen      | **techonthenet.com** |
| 8000        | Anderson  | Paige      | NULL                 |
| 9000        | Johnson   | Derek      | **techonthenet.com** |

이 예제에서는 customers 테이블의 모든 favorite_website 값을 'techonthenet.com'으로 업데이트하며, favorite_website에 NULL 값이 포함되어 있습니다. 보시다시피, favorite_website은 1행만 제외하고 모두 업데이트되었습니다.

---
## 예제 - DELETE 문과 함께 IS NOT NULL 사용
다음으로 [DELETE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/DELETE.md)에서 IS NOT NULL 조건을 사용하는 방법에 대한 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 orders라는 테이블이 있습니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

다음 DELETE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/is_not_null_sql.php)**
```SQL
DELETE FROM orders
WHERE customer_id IS NOT NULL;
```
레코드 4개가 삭제됩니다. orders 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM orders;
```
아래가 표시되는 결과입니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 5        | NULL        | 2016/05/01 |

이 예제에서는 customer_id에 NULL 값이 포함되지 않은 모든 레코드를 orders 테이블에서 삭제합니다.

---
**[< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/IS_NULL.md) / [다음 : LIKE >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/LIKE.md)**