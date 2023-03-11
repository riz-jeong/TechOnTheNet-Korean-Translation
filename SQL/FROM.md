# SQL : FROM 절

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **FROM 절**을 사용하는 방법을 설명합니다.

## 설명
SQL FROM 절은 SQL 문에 필요한 테이블과 모든 조인을 나열하는 데 사용됩니다.

## 구문
SQL에서 FROM 절의 구문은 다음과 같습니다.
```SQL
FROM table1
[ { INNER JOIN
  | LEFT [OUTER] JOIN
  | RIGHT [OUTER] JOIN
  | FULL [OUTER] JOIN } table2
ON table1.column1 = table2.column1 ]
```
### 매개변수 및 인수
#### **table1 and table2**
- 다음은 SQL 문에 사용된 테이블입니다. 두 테이블은 table1.column1 = table2.column1을 기준으로 조인됩니다.

## 참고
- SQL 문에서 FROM 절을 사용하는 경우 FROM 절에 나열된 테이블이 하나 이상 있어야 합니다.
- SQL FROM 절에 두 개 이상의 테이블이 나열되어 있는 경우 일반적으로 이러한 테이블은 INNER 또는 OUTER 조인을 사용하여 조인됩니다.

#
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!
### [DDL/DML 받기](https://www.techonthenet.com/sql/from_ddl.php)

#
## 예제 - FROM 절에 나열된 테이블 하나
먼저 SQL 문에서 하나의 테이블만 나열하는 FROM 절을 사용하는 방법부터 살펴보겠습니다.

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

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/from_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_id < 400
ORDER BY city DESC;
```
3개의 레코드가 선택됩니다. 아래는 표시되는 결과입니다.

| supplier_id | supplier_name | city          | state      |
| :---------- | :------------ | :------------ | :--------- |
| 300         | Oracle        | Redwood City  | California |
| 100         | Microsoft     | Redmond       | Washington |
| 200         | Google        | Mountain View | California |

이 예제에서는 FROM 절을 사용하여 suppliers라는 테이블을 나열했습니다.  
이 쿼리에서는 테이블을 하나만 나열했기 때문에 조인이 수행되지 않습니다.

#
## 예제 - FROM 절의 두 테이블(INNER JOIN)
FROM 절을 사용하여 두 테이블을 함께 [INNER JOIN](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/INNER_JOIN.md)하는 방법을 살펴보겠습니다.  
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

그리고 다음과 같은 데이터가 있는 categories 테이블입니다.

| category_id | category_name       |
| :---------- | :------------------ |
| 25          | Deli                |
| 50          | Produce             |
| 75          | Bakery              |
| 100         | General Merchandise |
| 125         | Technology          |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/from_try_sql.php)**
```SQL
SELECT products.product_name, categories.category_name
FROM products 
INNER JOIN categories
ON products.category_id = categories.category_id
WHERE product_name <> 'Pear';
```
5개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_name | category_name |
| :----------- | :------------ |
| Banana       | Produce       |
| Orange       | Produce       |
| Apple        | Produce       |
| Bread        | Bakery        |
| Sliced Ham   | Deli          |

이 예제에서는 FROM 절을 사용하여 두 테이블(products 및 categories)을 조인합니다.  
이 경우 FROM 절을 사용하여 두 테이블의 category_id 열을 기준으로 products 테이블과 categories 테이블 간에 INNER JOIN을 지정합니다.

#
## 예제 - FROM 절의 두 테이블(OUTER JOIN)
[OUTER JOIN](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/OUTER_JOIN.md)을 사용하여 두 테이블을 조인할 때 FROM 절을 사용하는 방법을 살펴보겠습니다.  
이 경우 LEFT OUTER JOIN을 살펴보겠습니다.

위의 INNER JOIN 예제에서와 동일한 제품 및 카테고리 테이블을 사용하되 이번에는 LEFT OUTER JOIN을 사용하여 테이블을 조인해 보겠습니다.  
다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/from_try_sql.php)**
```SQL
SELECT products.product_name, categories.category_name
FROM products 
LEFT OUTER JOIN categories
ON products.category_id = categories.category_id
WHERE product_name <> 'Pear';
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_name | category_name |
| :----------- | :------------ |
| Banana       | Produce       |
| Orange       | Produce       |
| Apple        | Produce       |
| Bread        | Bakery        |
| Sliced Ham   | Deli          |
| Kleenex      | NULL          |

이 예제에서는 FROM 절을 사용하여 두 테이블의 category_id를 기준으로 products 및 categories 테이블을 좌측 외부 조인합니다.

이제 product_name이 'Kleenex'인 마지막 레코드가 범주 이름에 대한 NULL 값과 함께 결과 집합에 나타납니다.  
이 레코드는 INNER 조인을 수행했을 때 결과에 나타나지 않았습니다.

#
### [< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT.md) / [다음 : Comparison Operators >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/Comparison_Operators.md)