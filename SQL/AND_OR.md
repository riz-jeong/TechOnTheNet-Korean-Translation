# SQL: AND 및 OR 조건 결합

이 SQL 튜토리얼에서는 단일 쿼리에서 **AND 조건**과 **OR 조건**을 함께 사용하는 방법을 구문과 예제를 통해 설명합니다.

## 설명
SQL [AND 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/AND.md)과 [OR 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/OR.md)을 결합하여 SELECT, INSERT, UPDATE 또는 DELETE 문에서 여러 조건을 테스트할 수 있습니다.

이러한 조건을 결합할 때는 괄호를 사용하여 데이터베이스가 각 조건을 평가할 순서를 알 수 있도록 하는 것이 중요합니다. (마치 수학 시간에 연산 순서를 배울 때와 같습니다!)

[![AND & OR](https://img.youtube.com/vi/l3Ky5btytSY/0.jpg)](https://youtu.be/l3Ky5btytSY)

## 구문
SQL에서 AND 조건과 OR 조건을 함께 사용하는 구문은 다음과 같습니다.
```SQL
WHERE condition1
AND condition2
...
OR condition_n;
```
### 매개변수 및 인수
#### **condition1, condition2, ... condition_n**
- 레코드가 선택될지 여부를 결정하기 위해 평가되는 조건입니다.

## 참고
- SQL AND 및 OR 조건을 사용하면 여러 조건을 테스트할 수 있습니다.
- 괄호 안의 연산 순서를 잊지 마세요!

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!
### [DDL/DML 받기](https://www.techonthenet.com/sql/and_or_ddl.php)

---
## 예제 - SELECT 문과 함께 "AND" 및 "OR" 조건 사용
이제 [SELECT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT.md)에서 AND 조건과 OR 조건을 함께 사용하는 방법의 예를 살펴보겠습니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/and_or_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE (state = 'California' AND supplier_id <> 900)
OR (supplier_id = 100);
```

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 100         | Microsoft         | Redmond          | Washington |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 700         | Dole Food Company | Westlake Village | California |

이 예제에서는 state가 California이지만 supplier_id가 900이 아닌 모든 공급업체가 반환됩니다. 이 쿼리는 또한 supplier_id가 100인 모든 공급업체를 반환합니다. 괄호는 AND 및 OR 조건이 평가되는 순서를 결정합니다. 수학 시간에 연산 순서에서 배운 것과 같습니다!

---
## 예제 - UPDATE 문과 함께 "AND" 및 "OR" 조건 사용
다음으로 [UPDATE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/UPDATE.md)에서 AND 및 OR 조건을 사용하는 방법을 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이제 AND 및 OR 조건을 사용하여 테이블의 레코드를 업데이트하는 방법을 보여드리겠습니다. 다음 UPDATE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/and_or_try_sql.php)**
```SQL
UPDATE customers
SET favorite_website = 'techonthenet.com'
WHERE customer_id = 6000
OR (customer_id > 7000 AND last_name <> 'Johnson');
```

```SQL
SELECT * FROM customers;
```
아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website     |
| :---------- | :-------- | :--------- | :------------------- |
| 4000        | Jackson   | Joe        | techonthenet.com     |
| 5000        | Smith     | Jane       | digminecraft.com     |
| 6000        | Ferguson  | Samantha   | **techonthenet.com** |
| 7000        | Reynolds  | Allen      | checkyourmath.com    |
| 8000        | Anderson  | Paige      | **techonthenet.com** |
| 9000        | Johnson   | Derek      | techonthenet.com     |

이 예제에서는 customers 테이블의 모든 favorite_website 값을 customer_id가 6000이고 customer_id가 7000보다 크며 last_name이 'Johnson'이 아닌 레코드가 있는 'techonthenet.com'으로 업데이트합니다. 보시다시피 세 번째 행과 다섯 번째 행의 favorite_website 값이 업데이트되었습니다.

---
## 예제 - DELETE 문과 함께 "AND" 및 "OR" 조건 사용
다음으로 [DELETE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/DELETE.md)을 사용하여 AND 및 OR 조건을 결합하여 레코드를 삭제하는 방법을 살펴보겠습니다.

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

다음 DELETE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/and_or_try_sql.php)**
```SQL
DELETE FROM products
WHERE category_id = 25
OR (product_id < 4 AND product_name <> 'Banana');
```
3개의 레코드가 삭제됩니다. products 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM products;
```
아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 2          | Banana       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 7          | Kleenex      | NULL        |

이 예제에서는 category_id가 25인 제품 테이블에서 모든 레코드를 삭제합니다. 또한 product_id가 4보다 작고 product_name이 'Banana'와 같지 않은 모든 레코드가 제품 테이블에서 삭제됩니다.

---
### [< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/OR.md) / [다음 : DISTINCT >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/DISTINCT.md)