# SQL : UPDATE 문

이 SQL 튜토리얼에서는 구문, 예제 및 [연습 문제](UPDATE_Exercises.md)를 통해 SQL **UPDATE 문**을 사용하는 방법을 설명합니다.

## 설명
SQL UPDATE 문은 테이블의 기존 레코드를 업데이트하는 데 사용됩니다.

[![UPDATE](https://img.youtube.com/vi/B6WCH3X9oyE/0.jpg)](https://youtu.be/B6WCH3X9oyE)

## 구문
SQL에서 테이블을 업데이트할 때 UPDATE 문의 구문은 다음과 같습니다.
```SQL
UPDATE table
SET column1 = expression1,
    column2 = expression2,
    ...
[WHERE conditions];
```
또는

다른 테이블의 데이터로 테이블을 업데이트할 때 SQL UPDATE 문의 구문은 다음과 같습니다.
```SQL
UPDATE table1
SET column1 = (SELECT expression1
               FROM table2
               WHERE conditions)
[WHERE conditions];
```
또는

여러 테이블을 업데이트할 때 SQL UPDATE 문의 구문(Oracle에서는 허용되지 않음)은 다음과 같습니다.
```SQL
UPDATE table1, table2, ...
SET column1 = expression1,
    column2 = expression2,
    ...
WHERE table1.column = table2.column
[AND conditions];
```

### 매개변수 및 인수
#### column1, column2
- 업데이트하려는 열입니다.
#### expression1, expression2
- 이것이 column1, column2에 할당할 새 값입니다. 따라서 column1에는 expression1의 값이 할당되고 column2에는 expression2의 값이 할당되는 식으로 할당됩니다.
#### WHERE conditions(WHERE 조건)
- 선택 사항입니다. 업데이트를 실행하기 위해 충족해야 하는 조건입니다. 조건을 제공하지 않으면 테이블의 모든 레코드가 업데이트됩니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/update_ddl.php)**

---
## 예제 - 단일 열 업데이트
SQL UPDATE 문을 사용하여 테이블의 단일 열을 업데이트하는 방법을 보여주는 예제를 살펴보겠습니다.

이 UPDATE 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이제 customers 테이블의 한 열을 업데이트하여 UPDATE 문이 어떻게 작동하는지 살펴보겠습니다. 다음 UPDATE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/update_try_sql.php)**
```SQL
UPDATE customers
SET first_name = 'Judy'
WHERE customer_id = 8000;
```
레코드 1개가 업데이트됩니다. customers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM customers;
```
다음은 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | **Judy**   | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이 UPDATE 예제에서는 customer_id가 8000인 customers 테이블에서 first_name 필드가 'Judy'로 설정되어 있습니다.

---
## 예제 - 여러 열 업데이트
테이블에서 둘 이상의 열을 업데이트하는 방법을 보여주는 UPDATE 예제를 살펴보겠습니다.

>팁: UPDATE 문에서 여러 열을 업데이트하는 경우 SET 절에서 열/값 쌍을 쉼표로 구분해야 합니다.

이 UPDATE 예제에는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다.

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

이제 UPDATE 문을 사용하여 한 번에 둘 이상의 열 값을 업데이트하는 방법을 보여드리겠습니다. 다음 UPDATE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/update_try_sql.php)**
```SQL
UPDATE suppliers
SET supplier_id = 150,
    supplier_name = 'Apple',
    city = 'Cupertino'
WHERE supplier_name = 'Google';
```
레코드 1개가 업데이트됩니다. suppliers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM suppliers;
```
다음은 표시되는 결과입니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 100         | Microsoft         | Redmond          | Washington |
| **150**     | **Apple**         | **Cupertino**    | California |
| 300         | Oracle            | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

이 UPDATE 예제에서는 supplier_name이 'Google'인 행의 supplier_id를 150으로, supplier_name을 'Apple'로, city를 'Cupertino'로 업데이트합니다.

---
## 예제 - 다른 테이블의 데이터로 테이블 업데이트
다른 테이블의 데이터로 테이블을 업데이트하는 방법을 보여주는 UPDATE 예제를 살펴보겠습니다.

이 UPDATE 예제에는 다음과 같은 데이터가 있는 products라는 테이블이 있습니다.

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

이제 summary_data 테이블을 products 테이블의 값으로 업데이트해 보겠습니다. 다음 UPDATE 문을 입력합니다.
```SQL
UPDATE summary_data
SET current_category = (SELECT category_id
   FROM products
   WHERE products.product_id = summary_data.product_id)
WHERE EXISTS (SELECT category_id
   FROM products
   WHERE products.product_id = summary_data.product_id);
```
5개의 레코드가 업데이트됩니다. summary_data 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM summary_data;
```
다음은 표시되는 결과입니다.

| product_id | current_category |
| :--------- | :--------------- |
| 1          | **50**           |
| 2          | **50**           |
| 3          | **50**           |
| 4          | **50**           |
| 5          | **75**           |
| 8          | 10               |

이 예제에서는 summary_data 테이블의 current_category 필드를 product_id 값이 일치하는 products 테이블의 category_id로 업데이트합니다. summary_data 테이블의 처음 5개 레코드가 업데이트되었습니다.

>팁: 레코드를 업데이트하기 전에 products 테이블과 summary_data 테이블 모두에 일치하는 product_id가 있는지 확인하기 위해 UPDATE 문에 WHERE 절에 [EXISTS 조건](EXISTS.md)이 포함되어 있음을 알 수 있습니다.

EXISTS 조건을 포함하지 않았다면 UPDATE 쿼리는 summary_data 테이블의 6번째 행에 있는 current_category 필드를 NULL로 업데이트했을 것입니다. (products 테이블에 product_id=8인 레코드가 없기 때문입니다)

---
## 연습 문제
SQL UPDATE 문을 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습을 통해 UPDATE 문을 사용하는 기술을 시험해 볼 수 있습니다. 풀어야 하는 문제가 주어집니다. 각 연습이 끝나면 정답을 확인할 수 있도록 해답이 제공됩니다. 한번 도전해 보세요!

**[연습 문제로 이동](UPDATE_Exercises.md)**

---
**[< 이전](INSERT.md) / [다음 : DELETE >](DELETE.md)**