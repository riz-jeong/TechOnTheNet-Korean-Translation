# SQL : 비교 연산자

이 SQL 튜토리얼에서는 SQL에서 같음과 같지 않음을 테스트하는 데 사용되는 모든 비교 연산자와 고급 연산자를 살펴봅니다.

## 설명
비교 연산자는 WHERE 절에서 선택해야 할 레코드를 결정하는 데 사용됩니다.  
다음은 SQL에서 사용할 수 있는 비교 연산자 목록입니다.
| 비교 연산자 | 설명                                            |
| :---------- | :---------------------------------------------- |
| =           | 같음                                            |
| <>          | 같지 않음                                       |
| !=          | 같지 않음                                       |
| >           | 보다 큼                                         |
| >=          | 크거나 같음                                     |
| <           | 보다 작음                                       |
| <=          | 작거나 같음                                     |
| IN ( )      | 리스트의 값과 일치                              |
| NOT         | 부정 연산                                       |
| BETWEEN     | 범위 내(포함)                                   |
| IS NULL     | NULL 값                                         |
| IS NOT NULL | Non-NULL 값                                     |
| LIKE        | %와 _를 사용하여 패턴 일치                      |
| EXISTS      | 하위 쿼리가 하나 이상의 행을 반환하면 조건 충족 |

#
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!
### [DDL/DML 받기](https://www.techonthenet.com/sql/comparison_operators_ddl.php)

#
## 예제 - 동등 연산자
SQL에서는 = 연산자를 사용하여 쿼리에서 동일성 여부를 테스트할 수 있습니다.  
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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name = 'Microsoft';
```
1개의 레코드가 선택됩니다. 아래는 표시되는 결과입니다.

| supplier_id | supplier_name | city    | state      |
| :---------- | :------------ | :------ | :--------- |
| 100         | Microsoft     | Redmond | Washington |

이 예제에서 위의 SELECT 문은 suppliers 테이블에서 supplier_name이 Microsoft와 같은 모든 행을 반환합니다.

#
## 예제 - 부등 연산자
SQL에서는 쿼리에서 부등식을 테스트하는 두 가지 방법이 있습니다.  
<> 연산자 또는 != 연산자를 사용할 수 있습니다. 둘 다 동일한 결과를 반환합니다.  
이전 예제와 동일한 suppliers 테이블을 사용하겠습니다.
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
다음 SQL 문을 입력하여 <> 연산자를 사용하여 부등식을 테스트합니다. **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name <> 'Microsoft';
```
또는 다음 SQL 문을 입력하여 != 연산자를 사용합니다. **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name != 'Microsoft';
```
8개의 레코드가 선택됩니다. 아래는 SQL 문 중 하나에 표시되는 결과입니다.

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

이 예제에서 두 SELECT 문은 suppliers 테이블에서 supplier_name이 Microsoft와 같지 않은 모든 행을 반환합니다.

#
## 예제 - 보다 큼 연산자
SQL에서 > 연산자를 사용하여 보다 큼 연산식을 테스트할 수 있습니다.  
이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.
| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |
다음 SQL 문을 입력합니다.  **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id > 6000;
```
3개의 레코드가 선택됩니다. 아래는 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이 예제에서 SELECT 문은 customer_id가 6000보다 큰 customers 테이블의 모든 행을 반환합니다.  
6000과 같은 customer_id는 결과 집합에 포함되지 않습니다.

#
## 예제 - 크거나 같음 연산자
SQL에서는 >= 연산자를 사용하여 크거나 같음 연산식을 테스트할 수 있습니다.  
이전 예제와 동일한 customers 테이블을 사용하겠습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SQL 문을 입력합니다.  **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id >= 6000;
```
4개의 레코드가 선택됩니다. 아래는 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이 예제에서 SELECT 문은 customers 테이블에서 customer_id가 6000보다 크거나 같은 모든 행을 반환합니다.  
이 경우 6000과 같은 supplier_id가 결과 집합에 포함됩니다.

#
## 예제 - 보다 작음 연산자
SQL에서 < 연산자를 사용하여 보다 작음 연산식을 테스트할 수 있습니다.  
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

다음 SQL 문을 입력합니다.  **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_id < 5;
```
4개의 레코드가 선택됩니다. 아래는 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |

이 예제에서 SELECT 문은 products 테이블에서 product_id가 5보다 작은 모든 행을 반환합니다.  
5와 같은 product_id는 결과 집합에 포함되지 않습니다.

#
## 예제 - 작거나 같음 연산자
SQL에서는 <= 연산자를 사용하여 작거나 같음 연산식을 테스트할 수 있습니다.  
이전 예제와 동일한 products 테이블을 사용하겠습니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

다음 SQL 문을 입력합니다.  **[Try it](https://www.techonthenet.com/sql/comparison_operators_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_id <= 5;
```
5개의 레코드가 선택됩니다. 아래는 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |

이 예제에서 SELECT 문은 products 테이블에서 product_id가 5보다 작거나 같은 모든 행을 반환합니다.  
이 경우 5와 같은 product_id가 결과 집합에 포함됩니다.

#
## 예제 - 고급 연산자
고급 비교 연산자에 대해 자세히 알아보려면 각 연산자에 대해 개별적으로 설명하는 튜토리얼을 작성해 두었습니다.  이러한 주제는 나중에 다루거나 지금 바로 튜토리얼 중 하나로 이동할 수 있습니다.
- [IN ( )](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/IN.md)
- [NOT](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/NOT.md)
- [BETWEEN](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/BETWEEN.md)
- [IS NULL](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/IS_NULL.md)
- [IS NOT NULL](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/IS_NOT_NULL.md)
- [LIKE](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/LIKE.md)
- [EXISTS](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/EXISTS.md)