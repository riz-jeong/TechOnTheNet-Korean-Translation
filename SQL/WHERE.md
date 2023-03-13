# SQL : WHERE 절

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **WHERE 절**을 사용하는 방법을 설명합니다.

## 설명
SQL WHERE 절은 결과를 필터링하고 SELECT, INSERT, UPDATE 또는 DELETE 문에서 조건을 적용하는 데 사용됩니다.

## 구문
SQL에서 WHERE 절의 구문은 다음과 같습니다.
```SQL
WHERE conditions;
```
### 매개변수 및 인수
#### **conditions(조건)**
- 레코드를 선택하기 위해 충족해야 하는 조건입니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/where_ddl.php)**

---
## 예제 - WHERE 절의 하나의 조건
SQL WHERE 절의 구문을 설명하기 어렵기 때문에 WHERE 절을 사용하여 조건 1개를 적용하는 예제부터 시작하겠습니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/where_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE state = 'California';
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 700         | Dole Food Company | Westlake Village | California |
| 900         | Electronic Arts   | Redwood City     | California |

이 예제에서는 SQL WHERE 절을 사용하여 suppliers 테이블에서 결과를 필터링했습니다. 위의 SQL 문은 suppliers 테이블에서 state가 California인 모든 행을 반환합니다.  
선택에 *가 사용되었으므로 suppliers 테이블의 모든 필드가 결과 집합에 나타납니다.

---
## 예제 - WHERE 절의 두 가지 조건(AND 조건)
WHERE 절에서 AND 조건을 사용하여 레코드를 선택하기 위해 충족해야 하는 조건을 하나 이상 지정할 수 있습니다. 이 작업을 수행하는 방법을 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/where_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE favorite_website = 'techonthenet.com'
AND customer_id > 6000;
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website |
| :---------- | :-------- | :--------- | :--------------- |
| 9000        | Johnson   | Derek      | techonthenet.com |

이 예제에서는 WHERE 절을 사용하여 여러 조건을 정의합니다.  
이 경우 이 SQL 문은 AND 조건을 사용하여 favorite_website이 techonthenet.com이고 customer_id가 6000보다 큰 모든 고객을 반환합니다.

---
## 예제 - WHERE 절의 두 가지 조건(OR 조건)
WHERE 절의 OR 조건을 사용하여 조건 중 하나라도 충족되면 레코드가 반환되는 여러 조건을 테스트할 수 있습니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/where_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_name = 'Pear'
OR product_name = 'Apple';
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 4          | Apple        | 50          |

이 예제에서는 WHERE 절을 사용하여 여러 조건을 정의하지만 AND 조건을 사용하는 대신 OR 조건을 사용합니다.  
이 경우 이 SQL 문은 제품 테이블에서 product_name이 Pear 또는 Apple인 모든 레코드를 반환합니다.

---
## 예제 - AND 및 OR 조건 결합
AND 조건과 OR 조건을 결합하여 더 복잡한 조건을 테스트할 수도 있습니다.

이 예제에서 products 테이블을 다시 사용해 보겠습니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/where_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE (product_id > 3 AND category_id = 75)
OR (product_name = 'Pear');
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 5          | Bread        | 75          |

이 예제에서는 product_id가 3보다 크고 category_id가 75인 모든 제품과 product_name이 Pear인 모든 제품을 반환합니다.  
괄호는 AND 및 OR 조건이 평가되는 순서를 결정합니다. 수학 시간에 배운 연산 순서와 같습니다!

---
**[< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/Comparison_Operators.md) / [다음 : ORDER BY >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/ORDER_BY.md)**