# SQL : OR 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **OR 조건**을 사용하는 방법을 설명합니다.

## 설명
SQL OR 조건은 SELECT, INSERT, UPDATE 또는 DELETE 문에서 여러 조건을 테스트하는 데 사용됩니다. 레코드가 선택되려면 조건 중 하나라도 충족되어야 합니다.

## 구문
SQL에서 OR 조건의 구문은 다음과 같습니다.
```SQL
WHERE condition1
OR condition2
...
OR condition_n;
```
### 매개변수 및 인수
#### **condition1, condition2, ... condition_n**
- 각 레코드에 대해 테스트할 여러 조건. 하나 이상의 조건을 충족하면 결과 집합에 포함할 수 있습니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!
### [DDL/DML 받기](https://www.techonthenet.com/sql/or_ddl.php)

---
## 예제 - SELECT 문과 함께 "OR" 조건 사용
[SELECT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT.md)에서 OR 조건을 사용하여 레코드를 선택하려면 어떤 조건이 충족되어야 하는 여러 조건을 테스트하는 방법을 보여주는 예제를 살펴 보겠습니다.

이 예제에는 다음과 같은 데이터가 포함된 suppliers라는 테이블이 있습니다.

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

이제 OR 조건을 사용하여 두 가지 조건을 테스트하는 방법을 보여 드리겠습니다. 다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/or_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE city = 'Mountain View'
OR supplier_id = 100
ORDER BY supplier_name;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name | city          | state      |
| :---------- | :------------ | :------------ | :--------- |
| 200         | Google        | Mountain View | California |
| 100         | Microsoft     | Redmond       | Washington |

이 예제에서는 Mountain View 시에 있거나 supplier_id가 100인 모든 공급업체가 반환됩니다. [SELECT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT.md)에 *가 사용되었으므로 suppliers 테이블의 모든 필드가 결과 집합에 나타납니다.

---
## 예제 - UPDATE 문과 함께 "OR" 조건 사용
OR 조건은 SQL [UPDATE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/UPDATE.md)에서 여러 조건을 테스트하는 데 사용할 수 있습니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 UPDATE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/or_try_sql.php)**
```SQL
UPDATE customers
SET favorite_website = 'techonthenet.com'
WHERE customer_id = 5000
OR last_name = 'Reynolds'
OR first_name = 'Paige';
```
3개의 레코드가 업데이트됩니다. customers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM customers;
```
아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website     |
| :---------- | :-------- | :--------- | :------------------- |
| 4000        | Jackson   | Joe        | techonthenet.com     |
| 5000        | Smith     | Jane       | **techonthenet.com** |
| 6000        | Ferguson  | Samantha   | bigactivities.com    |
| 7000        | Reynolds  | Allen      | **techonthenet.com** |
| 8000        | Anderson  | Paige      | **techonthenet.com** |
| 9000        | Johnson   | Derek      | techonthenet.com     |

이 예제에서는 customers 테이블의 모든 favorite_website 값을 customer_id가 5000이거나 last_name이 Reynolds이거나 first_name이 Paige인 techonthenet.com으로 업데이트합니다. 보시다시피 두 번째, 네 번째 및 다섯 번째 행의 favorite_website 필드가 업데이트됩니다.

---
## 예제 - UPDATE 문과 함께 "OR" 조건 사용
다음으로 [DELETE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/DELETE.md)에서 OR 조건을 사용하여 레코드가 삭제되기 전에 조건이 충족되는지 테스트하는 방법을 살펴보겠습니다.

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

다음 DELETE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/or_try_sql.php)**
```SQL
DELETE FROM products
WHERE product_name = 'Pear'
OR product_name = 'Apple'
OR category_id = 25;
```
3개의 레코드가 삭제됩니다. products 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM products;
```
아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 5          | Bread        | 75          |
| 7          | Kleenex      | NULL        |

이 조건 예제는 products 테이블에서 product_name이 Pear, product_name이 Apple 또는 category_id = 25인 모든 레코드를 삭제합니다.

---
### [< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/AND.md) / [다음 : AND & OR >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/AND_OR.md)