# SQL : ORDER BY 절

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **ORDER BY 절**을 사용하는 방법을 설명합니다.

## 설명
SQL ORDER BY 절은 SELECT 문에 대한 결과 집합의 레코드를 정렬하는 데 사용됩니다.

## 구문
SQL에서 ORDER BY 절의 구문은 다음과 같습니다.
```SQL
SELECT expressions
FROM tables
[WHERE conditions]
ORDER BY expression [ ASC | DESC ];
```
### 매개변수 및 인수
#### **expressions(표현식)**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.
#### **ASC**
- 선택 사항입니다. ASC는 결과 집합을 표현식별로 오름차순으로 정렬합니다. 기본 동작입니다.
#### **DESC**
- 선택 사항입니다. DESC는 결과 집합을 표현식별로 내림차순으로 정렬합니다.

## 참고
- ORDER BY 절에 ASC 또는 DESC 수정자가 제공되지 않으면 결과가 표현식별로 오름차순으로 정렬됩니다. 이는 ORDER BY expression ASC와 동일합니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/order_by_ddl.php)**

---
## 예제 - 오름차순으로 결과 정렬
결과를 오름차순으로 정렬하려면 ASC 속성을 지정하면 됩니다. ORDER BY 절의 필드 뒤에 값(ASC 또는 DESC)을 지정하지 않으면 기본적으로 정렬 순서가 오름차순으로 지정됩니다. 이에 대해 자세히 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/order_by_try_sql.php)**
```SQL
SELECT *
FROM customers
ORDER BY last_name;
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 8000        | Anderson  | Paige      | NULL              |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 9000        | Johnson   | Derek      | techonthenet.com  |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 5000        | Smith     | Jane       | digminecraft.com  |

이 예제는 고객의 모든 레코드를 last_name 필드를 기준으로 오름차순으로 정렬하여 반환하며, 다음 SQL ORDER BY 절과 동일합니다. **[Try it](https://www.techonthenet.com/sql/order_by_try_sql.php)**
```SQL
SELECT *
FROM customers
ORDER BY last_name ASC;
```
대부분의 프로그래머는 오름차순으로 정렬할 경우 ASC 속성을 생략합니다.

---
## 예제 - 내림차순으로 결과 정렬
결과 집합을 내림차순으로 정렬할 때는 ORDER BY 절에 DESC 속성을 사용합니다. 자세히 살펴보겠습니다.

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

다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/order_by_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_id > 400
ORDER BY supplier_id DESC;
```
5개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 900         | Electronic Arts   | Redwood City     | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 700         | Dole Food Company | Westlake Village | California |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 500         | Tyson Foods       | Springdale       | Arkansas   |

이 예제에서는 supplier_id 필드를 기준으로 결과 집합을 내림차순으로 정렬합니다.

---
## 예제 - 상대적 위치에 따른 결과 정렬
결과 집합의 첫 번째 필드가 1, 두 번째 필드가 2, 세 번째 필드가 3인 결과 집합의 상대적 위치별로 정렬하려면 SQL ORDER BY 절을 사용할 수도 있습니다.

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

다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/order_by_try_sql.php)**
```SQL
SELECT product_id, product_name
FROM products
WHERE product_name <> 'Bread'
ORDER BY 1 DESC;
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_id | product_name |
| :--------- | :----------- |
| 7          | Kleenex      |
| 6          | Sliced Ham   |
| 4          | Apple        |
| 3          | Orange       |
| 2          | Banana       |
| 1          | Pear         |

이 예제에서는 product_id 필드가 결과 집합에서 1번 위치에 있으므로 product_id 필드를 기준으로 결과를 내림차순으로 정렬하며, 이는 다음 SQL ORDER BY 절과 동일합니다. **[Try it](https://www.techonthenet.com/sql/order_by_try_sql.php)**
```SQL
SELECT product_id, product_name
FROM products
WHERE product_name <> 'Bread'
ORDER BY product_id DESC;
```

---
## 예제 - ASC 및 DESC 속성 모두 사용
SQL ORDER BY 절을 사용하여 결과 집합을 정렬하는 경우, 단일 [SELECT 문](SELECT.md)에서 ASC 및 DESC 속성을 사용할 수 있습니다.

이 예제에서는 이전 예제와 동일한 products 테이블을 사용하겠습니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/order_by_try_sql.php)**
```SQL
SELECT *
FROM products
WHERE product_id <> 7
ORDER BY category_id DESC, product_name ASC;
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 5          | Bread        | 75          |
| 4          | Apple        | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 1          | Pear         | 50          |
| 6          | Sliced Ham   | 25          |

이 예제에서는 category_id 필드를 기준으로 내림차순으로 정렬된 레코드를 반환하고, product_name을 기준으로 오름차순으로 정렬된 2차 정렬을 수행합니다.

---
**[< 이전](WHERE.md) / [다음 : AND >](AND.md)**