# SQL : IN 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **IN 조건**을 사용하는 방법을 설명합니다.

## 설명
SQL IN 조건(IN 연산자라고도 함)을 사용하면 표현식이 값 목록의 어떤 값과 일치하는지 쉽게 테스트할 수 있습니다. 이 조건은 SELECT, INSERT, UPDATE 또는 DELETE 문에서 여러 개의 [OR 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/OR.md)의 필요성을 줄이는 데 사용됩니다.

## 구문
SQL에서 IN 조건의 구문은 다음과 같습니다.
```SQL
expression IN (value1, value2, .... value_n);
```
또는
```SQL
expression IN (subquery);
```
### 매개변수 및 인수
#### **expression(표현식)**
- 테스트할 값입니다.
#### **value1, value2 ..., value_n**
- 표현식에 대해 테스트할 값입니다. 이러한 값 중 하나라도 표현식과 일치하면 IN 조건이 true로 평가됩니다.
#### **subquery(하위 쿼리)**
- 결과 집합이 표현식에 대해 테스트되는 [SELECT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT.md)입니다. 이러한 값 중 표현식과 일치하는 값이 하나라도 있으면 IN 조건은 참으로 평가됩니다.

#
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!
### [DDL/DML 받기](https://www.techonthenet.com/sql/in_ddl.php)

#
## 예제 - 문자 값과 함께 IN 조건 사용
IN 조건은 SQL의 모든 데이터 유형에 사용할 수 있습니다. 문자(문자열) 값에 IN 조건을 사용하는 방법을 살펴보겠습니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/in_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name IN ('Microsoft', 'Oracle', 'Flowers Foods');
```
3개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name | city         | state      |
| :---------- | :------------ | :----------- | :--------- |
| 100         | Microsoft     | Redmond      | Washington |
| 300         | Oracle        | Redwood City | California |
| 800         | Flowers Foods | Thomasville  | Georgia    |

이 예제에서는 supplier_name이 Microsoft, Oracle, Flowers Foods 중 하나인 suppliers 테이블의 모든 행을 반환합니다. 선택에 *가 사용되었으므로 suppliers 테이블의 모든 필드가 결과 집합에 나타납니다.

이는 다음 SQL 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/in_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name = 'Microsoft'
OR supplier_name = 'Oracle'
OR supplier_name = 'Flowers Foods';
```
보시다시피 IN 조건을 사용하면 여러 개의 OR 조건을 사용하는 것보다 더 읽기 쉽고 효율적으로 사용할 수 있습니다.

#
## 예제 - 숫자 값과 함께 IN 조건 사용
다음으로 숫자 값과 함께 IN 조건을 사용하는 방법을 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/in_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id IN (5000, 7000, 8000, 9000);
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이 예제에서는 customer_id가 5000, 7000, 8000, 9000 중 하나인 customers 테이블의 모든 레코드를 반환합니다.

이는 다음 SQL 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/in_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id = 5000
OR customer_id = 7000
OR customer_id = 8000
OR customer_id = 9000;
```

#
## 예제 - NOT 연산자와 함께 IN 조건 사용
마지막으로 NOT 연산자와 함께 IN 조건을 사용하는 방법을 살펴보겠습니다. NOT 연산자는 조건을 부정하는 데 사용됩니다. IN 조건과 함께 NOT 연산자를 사용하면 NOT IN 조건이 생성됩니다. 이렇게 하면 표현식이 목록에 없는지 테스트합니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/in_try_sql.php)**
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

이는 다음 SQL 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/in_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_name <> 'Pear'
AND product_name <> 'Banana'
AND product_name <> 'Bread';
```
보시다시피, IN 조건이 부정되기 때문에 동일한 SQL 문은 OR 조건 대신 AND 조건을 사용하여 작성됩니다.

#
### [< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/DISTINCT.md) / [다음 : NULL >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/IS_NULL.md)