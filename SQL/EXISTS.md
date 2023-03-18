# SQL : EXISTS 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **EXISTS 조건**을 사용하는 방법을 설명합니다.

## 설명
SQL EXISTS 조건은 하위 쿼리와 함께 사용되며 하위 쿼리가 하나 이상의 행을 반환하면 조건이 충족된 것으로 간주됩니다. 이 조건은 SELECT, INSERT, UPDATE, DELETE 문에서 사용할 수 있습니다.

## 구문
SQL에서 EXISTS 조건의 구문은 다음과 같습니다.
```SQL
WHERE EXISTS ( subquery );
```
### 매개변수 및 인수
#### subquery(하위 쿼리)
- 하위 쿼리는 SELECT 문입니다. 하위 쿼리가 결과 집합에서 하나 이상의 레코드를 반환하는 경우 EXISTS 절이 true로 평가되고 EXISTS 조건이 충족됩니다. 하위 쿼리가 레코드를 반환하지 않으면 EXISTS 절이 false로 평가되고 EXISTS 조건이 충족되지 않습니다.

## 참고
- EXISTS 조건을 사용하는 SQL 문은 외부 쿼리 테이블의 모든 행에 대해 하위 쿼리가 다시 실행되므로 매우 비효율적입니다. 대부분의 쿼리를 작성하는 더 효율적인 방법에는 EXISTS 조건을 사용하지 않는 방법이 있습니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/exists_ddl.php)**

---
## 예제 - SELECT 문과 함께 EXISTS 조건 사용
먼저 [SELECT 문](SELECT.md)과 함께 EXISTS 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 포함된 customers 테이블이 있습니다.

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

이제 customers 테이블에서 orders 테이블에 동일한 customer_id를 가진 레코드가 하나 이상 있는 모든 레코드를 찾아보겠습니다. 다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/exists_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE EXISTS 
  (SELECT *
   FROM orders
   WHERE customers.customer_id = orders.customer_id);
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |

이 예제에서는 orders 테이블에 customer_id 값이 나타나는 고객에 4개의 레코드가 있습니다.

---
## 예제 - UPDATE 문과 함께 EXISTS 조건 사용
[UPDATE 문](UPDATE.md)에서 EXISTS 조건을 사용하는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 products라는 테이블이 있습니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

그리고 다음 데이터가 포함된 summary_data라는 테이블이 있습니다.

| product_id | current_category |
| :--------- | :--------------- |
| 1          | 10               |
| 2          | 10               |
| 3          | 10               |
| 4          | 10               |
| 5          | 10               |
| 8          | 10               |

이제 summary_data 테이블을 products 테이블의 값으로 업데이트해 보겠습니다. 다음 SQL 문을 입력합니다.
```SQL
UPDATE summary_data
SET current_category = (SELECT category_id
   FROM products
   WHERE products.product_id = summary_data.product_id)
WHERE EXISTS (SELECT category_id
   FROM products
   WHERE products.product_id = summary_data.product_id)
```
5개의 레코드가 업데이트됩니다. summary_data 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM summary_data;
```

| product_id | current_category |
| :--------- | :--------------- |
| 1          | **50**           |
| 2          | **50**           |
| 3          | **50**           |
| 4          | **50**           |
| 5          | **75**           |
| 8          | 10               |

이 예제에서는 summary_data 테이블의 current_category 필드를 product_id 값이 일치하는 products 테이블의 category_id로 업데이트합니다. summary_data 테이블의 처음 5개 레코드가 업데이트되었습니다.

>팁: EXISTS 조건을 포함하지 않았다면 UPDATE 쿼리는 summary_data 테이블의 6번째 행에서 current_category 필드를 NULL로 업데이트했을 것입니다. (products 테이블에 product_id=8인 레코드가 없으므로)

---
## 예제 - DELETE 문과 함께 EXISTS 조건 사용
[DELETE 문](DELETE.md)에서 EXISTS 조건을 사용하는 예제를 살펴보겠습니다.

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

다음 DELETE 문을 입력합니다.
```SQL
DELETE FROM orders
WHERE EXISTS
  (SELECT *
   FROM customers
   WHERE customers.customer_id = orders.customer_id
   AND customers.last_name = 'Jackson');
```
레코드 1개가 삭제됩니다. orders 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM orders;
```
다음은 표시되는 결과입니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 5        | NULL        | 2016/05/01 |

이 예제에서는 customers 테이블에 성이 'Jackson'이고 두 테이블 모두에 일치하는 customer_id 값이 있는 레코드가 있는 orders 테이블에서 모든 레코드를 삭제합니다. 이 예제에서는 order_id=4에 대한 레코드가 삭제되었습니다.

삭제할 행 수를 확인하려면 삭제를 수행하기 전에 다음 SELECT 문을 실행하면 됩니다.
```SQL
SELECT COUNT(*) FROM orders
WHERE EXISTS
  (SELECT *
   FROM customers
   WHERE customers.customer_id = orders.customer_id
   AND customers.last_name = 'Jackson');
```
DELETE 문을 실행할 때 삭제될 레코드 수를 반환합니다.

| COUNT(*) |
| :------- |
| 1        |

---
## 예제 - EXISTS 조건과 함께 NOT 사용
마지막으로 [NOT 조건](NOT.md)을 EXISTS 조건과 결합하여 NOT EXISTS 조건을 만들 수 있습니다. SQL에서 NOT EXISTS 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/exists_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE NOT EXISTS
  (SELECT * 
   FROM orders
   WHERE customers.customer_id = orders.customer_id);
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이 예제에서는 customers 테이블의 모든 레코드를 반환하지만, orders 테이블에 지정된 customer_id에 대한 레코드가 없는 경우 해당 레코드를 반환합니다.

---
**[< 이전](TRUNCATE.md) / [다음 : GROUP BY >](GROUP_BY.md)**