# SQL : AND 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **AND 조건**을 사용하는 방법을 설명합니다.

## 설명
SQL AND 조건(AND 연산자라고도 함)은 SELECT, INSERT, UPDATE 또는 DELETE 문에서 두 개 이상의 조건을 테스트하는 데 사용됩니다. 레코드를 선택하려면 모든 조건이 충족되어야 합니다.

## 구문
SQL에서 AND 조건의 구문은 다음과 같습니다.
```SQL
WHERE condition1
AND condition2
...
AND condition_n;
```
### 매개변수 및 인수
#### **condition1, condition2, ... condition_n**
- 각 레코드에 대해 테스트할 여러 조건. 결과 집합에 포함되려면 모든 조건이 충족되어야 합니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/and_ddl.php)**

---
## 예제 - SELECT 문과 함께 "AND" 조건 사용
[SELECT 문](SQL/SELECT.md)에서 AND 조건을 사용하여 레코드를 선택하기 위해 충족해야 하는 두 가지 조건을 테스트하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이제 AND 조건을 사용하는 방법을 보여드리겠습니다. 다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/and_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE favorite_website = 'techonthenet.com'
AND customer_id > 6000
ORDER BY last_name;
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website |
| :---------- | :-------- | :--------- | :--------------- |
| 9000        | Johnson   | Derek      | techonthenet.com |

이 예제에서는 favorite_website이 techonthenet.com이고 customer_id가 6000보다 큰 모든 고객을 반환합니다. SQL SELECT 문에 *가 사용되었으므로 customers 테이블의 모든 필드가 결과 집합에 나타납니다.

---
## 예제 - UPDATE 문과 함께 "AND" 조건 사용
이제 [UPDATE 문](SQL/UPDATE.md)에서 AND 조건을 사용하는 방법의 예를 살펴보겠습니다. 레코드가 업데이트되기 전에 여러 조건이 충족되는지 테스트합니다.

이 예제에서는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다.

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

다음 UPDATE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/and_try_sql.php)**
```SQL
UPDATE suppliers
SET supplier_name = 'TBD'
WHERE city = 'Redwood City'
AND supplier_id <> 900;
```
레코드 1개가 업데이트됩니다. suppliers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM suppliers;
```
아래가 표시되는 결과입니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 100         | Microsoft         | Redmond          | Washington |
| 200         | Google            | Mountain View    | California |
| 300         | TBD               | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

이 예제에서는 suppliers 테이블의 모든 supplier_name 값을 city가 Redwood City이고 supplier_id가 900이 아닌 TBD로 업데이트합니다. 보시다시피 세 번째 행의 supplier_name이 업데이트되었습니다.

---
## 예제 - DELETE 문과 함께 "AND" 조건 사용
다음으로 [DELETE 문](DELETE.md)에서 AND 조건을 사용하여 레코드가 삭제되기 전에 두 가지 조건이 충족되는지 테스트하는 방법을 살펴보겠습니다.

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

다음 DELETE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/and_try_sql.php)**
```SQL
DELETE FROM products
WHERE category_id = 50
AND product_name <> 'Pear';
```
3개의 레코드가 삭제됩니다. products 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM products;
```
아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

이 예제에서는 category_id가 50이고 product_name이 Pear가 아닌 모든 레코드를 products 테이블에서 삭제합니다.

---
**[< 이전](ORDER_BY.md) / [다음 : OR >](OR.md)**