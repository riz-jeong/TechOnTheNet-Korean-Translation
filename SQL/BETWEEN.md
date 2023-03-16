# SQL : BETWEEN 조건

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **BETWEEN 조건**을 사용하는 방법을 설명합니다.

## 설명
SQL BETWEEN 조건을 사용하면 표현식이 값 범위(포함) 내에 있는지 쉽게 테스트할 수 있습니다. SELECT, INSERT, UPDATE 또는 DELETE 문에서 사용할 수 있습니다.

[![BETWEEN](https://img.youtube.com/vi/oiOvdZudb_I/0.jpg)](https://youtu.be/oiOvdZudb_I)

## 구문
SQL에서 BETWEEN 조건의 구문은 다음과 같습니다.
```SQL
expression BETWEEN value1 AND value2;
```
### 매개변수 및 인수
#### **expression(표현식)**
- 열 또는 계산입니다.
#### **value1 and value2**
- 이러한 값은 표현식이 비교되는 포괄적인 범위를 만듭니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/between_ddl.php)**

---
## 예제 - 숫자 값과 함께 BETWEEN 조건 사용
숫자 범위 내에서 값을 검색하기 위해 BETWEEN 조건을 사용하는 방법을 예로 들어 보겠습니다.

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

다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_id BETWEEN 300 AND 600;
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name  | city         | state      |
| :---------- | :------------- | :----------- | :--------- |
| 300         | Oracle         | Redwood City | California |
| 400         | Kimberly-Clark | Irving       | Texas      |
| 500         | Tyson Foods    | Springdale   | Arkansas   |
| 600         | SC Johnson     | Racine       | Wisconsin  |

이 예제에서는 supplier_id가 300에서 600(포함) 사이인 suppliers 테이블의 모든 행을 반환합니다. 이는 다음 SELECT 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_id >= 300
AND supplier_id <= 600;
```

---
## 예제 - 날짜 값과 함께 BETWEEN 조건 사용
SQL에서 날짜는 다소 까다로울 수 있으며, 날짜에 BETWEEN 조건을 사용하는 방법은 실행 중인 데이터베이스(예: Oracle, SQL Server, MySQL 등)에 따라 다릅니다. 각 주요 데이터베이스 기술에 대한 예제를 보여드리겠습니다. 그럼 시작해 보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 orders라는 테이블이 있습니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

실행 중인 데이터베이스에 따라 다음 SQL 문 중 하나를 입력합니다.

SQL Server, PostgreSQL 및 SQLite의 경우 **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT *
FROM orders
WHERE order_date BETWEEN '2016/04/19' AND '2016/05/01';
```
Oracle의 경우(TO_DATE 함수 사용)
```SQL
SELECT *
FROM orders
WHERE order_date BETWEEN TO_DATE ('2016/04/19', 'yyyy/mm/dd')
AND TO_DATE ('2016/05/01', 'yyyy/mm/dd');
```
MySQL 및 MariaDB의 경우(CAST 함수 사용).
```SQL
SELECT *
FROM orders
WHERE order_date BETWEEN CAST('2016/04/19' AS DATE) AND CAST('2016/05/01' AS DATE);
```
3개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

이 예제에서는 주문 날짜가 2016년 4월 19일부터 2016년 5월 1일(포함) 사이인 주문 테이블의 모든 레코드를 반환합니다.

---
## 예제 - BETWEEN 조건에 NOT 연산자 사용
BETWEEN 조건은 [NOT 연산자](NOT.md)와 함께 사용하여 NOT BETWEEN 조건을 만들 수 있습니다. 쿼리에서 NOT BETWEEN 조건을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id NOT BETWEEN 5000 AND 8000;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website |
| :---------- | :-------- | :--------- | :--------------- |
| 4000        | Jackson   | Joe        | techonthenet.com |
| 9000        | Johnson   | Derek      | techonthenet.com |

이렇게 하면 customer_id가 5000에서 8000 사이가 **아닌** 모든 행이 반환됩니다. 이는 다음 SELECT 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE customer_id < 5000
OR customer_id > 8000;
```

---
**[< 이전](JOINS.md) / [다음 : INSERT >](INSERT.md)**