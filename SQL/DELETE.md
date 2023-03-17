# SQL : DELETE 문

이 SQL 튜토리얼에서는 구문, 예제 및 [연습 문제](DELETE_Exercises.md)를 통해 SQL **DELETE 문**을 사용하는 방법을 설명합니다.

## 설명
SQL DELETE 문은 테이블에서 하나 이상의 레코드를 삭제하는 데 사용됩니다.

[![DELETE](https://img.youtube.com/vi/VKlNt3pkLaw/0.jpg)](https://youtu.be/VKlNt3pkLaw)

## 구문
SQL에서 DELETE 문의 구문은 다음과 같습니다.
```SQL
DELETE FROM table
[WHERE conditions];
```

### 매개변수 및 인수
#### table
- 레코드를 삭제하려는 테이블입니다.
#### WHERE conditions(WHERE 조건)
- 선택 사항입니다. 레코드를 삭제하기 위해 충족해야 하는 조건입니다. 조건을 제공하지 않으면 테이블의 모든 레코드가 삭제됩니다.

### 참고
- 테이블에서 전체 행을 삭제하는 것이므로 DELETE 문에 필드를 나열할 필요가 없습니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/delete_ddl.php)**

---
## 예제 - 조건이 하나 있는 DELETE 문
WHERE 절에 조건이 없는 DELETE 문을 실행하면 테이블의 모든 레코드가 삭제됩니다. 따라서 대부분의 경우 DELETE 문에 하나 이상의 조건이 있는 WHERE 절을 포함하게 됩니다.

WHERE 절에 조건이 하나 있는 DELETE 쿼리의 간단한 예부터 시작해 보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다:

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

다음 DELETE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/delete_try_sql.php)**
```SQL
DELETE FROM suppliers
WHERE supplier_name = 'Microsoft';
```
레코드 1개가 삭제됩니다. suppliers 테이블에서 데이터를 다시 선택합니다:
```SQL
SELECT * FROM suppliers;
```
다음은 표시되는 결과입니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

이 예제에서는 suppliers 테이블에서 supplier_name이 'Microsoft'인 모든 레코드를 삭제합니다.

삭제할 행 수를 확인하는 것이 좋습니다. 삭제를 수행하기 전에 다음 [SELECT 문](SELECT.md)을 실행하여 삭제할 행 수를 확인할 수 있습니다. **[Try it](https://www.techonthenet.com/sql/delete_try_sql.php)**
```SQL
SELECT COUNT(*)
FROM suppliers
WHERE supplier_name = 'Microsoft';
```
이 쿼리는 DELETE 문을 실행할 때 삭제될 레코드 수를 반환합니다.

| COUNT(*) |
| :------- |
| 1        |

---
## 예제 - 조건이 두 개 이상인 DELETE 문
SQL의 DELETE 문에는 AND 조건 또는 OR 조건을 사용하여 두 개 이상의 조건을 포함할 수 있습니다. AND 조건을 사용하면 모든 조건이 충족되는 경우 레코드를 삭제할 수 있습니다. OR 조건은 조건 중 하나라도 충족되면 레코드를 삭제합니다.

AND 조건을 사용하여 두 개의 조건이 있는 DELETE 문을 사용하는 예제를 살펴보겠습니다.

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

다음 DELETE 문을 입력합니다: **[Try it](https://www.techonthenet.com/sql/update_try_sql.php)**
```SQL
DELETE FROM products
WHERE category_id = 50
AND product_name <> 'Pear';
```
3개의 레코드가 삭제됩니다. products 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM products;
```
다음은 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

이 예제에서는 category_id가 50이고 product_name이 Pear가 아닌 모든 레코드를 제품 테이블에서 삭제합니다.

삭제할 행 수를 확인하려면 삭제를 수행하기 전에 다음 SELECT 문을 실행하면 됩니다. **[Try it](https://www.techonthenet.com/sql/delete_try_sql.php)**
```SQL
SELECT COUNT(*)
FROM products
WHERE category_id = 50
AND product_name <> 'Pear';
```
이 쿼리는 DELETE 문을 실행할 때 삭제될 레코드 수를 반환합니다.

| COUNT(*) |
| :------- |
| 3        |

---
## 예제 - DELETE 문과 함께 EXISTS 사용
더 복잡한 삭제 작업을 수행할 수도 있습니다.

다른 테이블의 값을 기반으로 한 테이블의 레코드를 삭제하고 싶을 수 있습니다. 삭제를 수행할 때 FROM 절에 둘 이상의 테이블을 나열할 수 없으므로 [EXISTS 절](EXISTS.md)을 사용할 수 있습니다.

이 예에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

그리고 다음 데이터가 포함된 orders라는 테이블이 있습니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

이제 summary_data 테이블을 products 테이블의 값으로 업데이트해 보겠습니다. 다음 UPDATE 문을 입력합니다.
```SQL
DELETE FROM orders
WHERE EXISTS
  (SELECT *
   FROM customers
   WHERE customers.customer_id = orders.customer_id
   AND customers.last_name = 'Jackson');
```
1개의 레코드가 업데이트됩니다. orders 테이블에서 데이터를 다시 선택합니다.
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

이 예제에서는 customers 테이블에 last_name이 'Jackson'이고 두 테이블 모두에 일치하는 customer_id 값이 있는 레코드가 있는 orders 테이블에서 모든 레코드를 삭제합니다. 이 예제에서는 order_id = 4에 대한 레코드가 삭제되었습니다.

삭제할 행 수를 확인하려면 삭제를 수행하기 전에 다음 SQL SELECT 문을 실행하면 됩니다.
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
## 자주 묻는 질문
- 질문 : TableA의 field1 및 field2의 데이터가 TableB의 fieldx 및 fieldz의 데이터와 일치하지 않는 모든 레코드를 삭제하려면 SQL DELETE 문을 어떻게 작성해야 하나요?

- 답변 : SQL DELETE 문에 다음과 같이 시도해 볼 수 있습니다.
```SQL
DELETE FROM TableA
WHERE NOT EXISTS
  (SELECT *
   FROM TableB
   WHERE TableA.field1 = TableB.fieldx
   AND TableA.field2 = TableB.fieldz);
```

---
## 연습 문제
SQL DELETE 문을 사용하여 자신의 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이러한 연습을 통해 DELETE 문을 사용하는 기술을 시험해 볼 수 있습니다. 풀어야 하는 문제가 주어집니다. 각 연습이 끝나면 정답을 확인할 수 있도록 솔루션을 제공합니다. 한번 도전해 보세요!

**[연습 문제로 이동](DELETE_Exercises.md)**

---
**[< 이전](UPDATE.md) / [다음 : TRUNCATE >](TRUNCATE.md)**