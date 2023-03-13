# SQL : SELECT 문

이 SQL 튜토리얼에서는 구문, 예제 및 [연습 문제](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT_Exercises.md)를 통해 SQL **SELECT 문**을 사용하는 방법을 설명합니다.

## 설명
SQL SELECT 문은 SQL 데이터베이스의 하나 이상의 테이블에서 레코드를 검색하는 데 사용됩니다. 검색된 레코드를 결과 집합이라고 합니다.

[![SELECT](https://img.youtube.com/vi/gbHXhXmACgI/0.jpg)](https://youtu.be/gbHXhXmACgI)

## 구문
SQL에서 SELECT 문의 구문은 다음과 같습니다.
```SQL
SELECT expressions
FROM tables
[WHERE conditions]
[ORDER BY expressions [ ASC | DESC ]];
```
### 매개변수 및 인수
#### **expressions(표현식)**
- 검색하려는 열 또는 계산입니다. 모든 열을 선택하려면 *를 사용합니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다. 조건을 제공하지 않으면 모든 레코드가 선택됩니다.
#### **ORDER BY expression(ORDER BY 표현식)**
- 선택 사항입니다. 결과 집합의 레코드를 정렬하는 데 사용되는 표현식입니다. 둘 이상의 표현식을 제공하는 경우 값을 쉼표(,)로 구분해야 합니다.
#### **ASC**
- 선택 사항입니다. ASC는 결과 집합을 표현식별로 오름차순으로 정렬합니다. 기본 동작입니다.
#### **DESC**
- 선택 사항입니다. DESC는 결과 집합을 표현식별로 내림차순으로 정렬합니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/select_ddl.php)**

---
## 예제 - 테이블에서 모든 필드 선택
SQL SELECT 문을 사용하여 테이블에서 모든 필드를 선택하는 방법을 보여주는 예제를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| ----------- | --------- | ---------- | ----------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이제 고객 테이블에서 모든 열을 선택하여 SELECT 문이 어떻게 작동하는지 살펴보겠습니다.  
다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE favorite_website = 'techonthenet.com'
ORDER BY last_name ASC;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website |
| ----------- | --------- | ---------- | ---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com |
| 9000        | Johnson   | Derek      | techonthenet.com |

이 예제에서는 *를 사용하여 favorite_website가 'techonthenet.com'인 customers 테이블의 모든 필드를 표시했습니다.  
결과 집합은 last_name을 기준으로 오름차순으로 정렬됩니다.

---
## 예제 - 테이블에서 개별 필드 선택
테이블의 모든 필드가 아니라 테이블에서 개별 필드를 선택하려면 SQL SELECT 문을 사용할 수도 있습니다.

이 예제에서는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다.

| supplier_id | supplier_name     | city             | state      |
| ----------- | ----------------- | ---------------- | ---------- |
| 100         | Microsoft         | Redmond          | Washington |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

이제 customers 테이블에서 모든 열을 선택하여 SELECT 문이 어떻게 작동하는지 살펴보겠습니다.  
다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT supplier_name, city
FROM suppliers
WHERE supplier_id > 500
ORDER BY supplier_name ASC, city DESC;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_name     | city             |
| ----------------- | ---------------- |
| Dole Food Company | Westlake Village |
| Electronic Arts   | Redwood City     |
| Flowers Foods     | Thomasville      |
| SC Johnson        | Racine           |

이 예제에서는 supplier_id 값이 500보다 큰 suppliers 테이블에서 supplier_name 및 city 필드만 반환합니다.  
결과는 supplier_name을 오름차순으로 정렬한 다음 city를 내림차순으로 정렬합니다.

---
## 예제 - 여러 테이블에서 개별 필드 선택
SQL SELECT 문을 사용하여 여러 테이블에서 필드를 검색할 수도 있습니다.

이 예제에서는 다음과 같은 데이터가 있는 orders라는 테이블이 있습니다.

| order_id | customer_id | order_date |
| -------- | ----------- | ---------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

그리고 다음 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| ----------- | --------- | ---------- | ----------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이제 주문 테이블과 고객 테이블에서 열을 선택해 보겠습니다.  
다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT orders.order_id, customers.last_name
FROM orders
INNER JOIN customers
ON orders.customer_id = customers.customer_id
WHERE orders.order_id <> 1
ORDER BY orders.order_id;
```
3개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| order_id | last_name |
| -------- | --------- |
| 2        | Smith     |
| 3        | Anderson  |
| 4        | Jackson   |

이 SELECT 예제에서는 두 테이블을 조인하여 orders 테이블의 order_id와 customers 테이블의 last_name을 표시하는 결과 집합을 제공합니다.  
SELECT 문에서 열을 사용할 때마다 열이 어느 테이블에 속하는지 모호할 경우를 대비하여 열 앞에 테이블 이름(예: orders.order_id)을 붙입니다.

orders 테이블의 모든 필드를 선택한 다음 customers 테이블의 last_name 필드를 선택하려는 경우  
다음 SELECT 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/select_try_sql.php)**
```SQL
SELECT orders.*, customers.last_name
FROM orders
INNER JOIN customers
ON orders.customer_id = customers.customer_id
WHERE orders.order_id <> 1
ORDER BY orders.order_id;
```
3개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| order_id | customer_id | order_date | last_name |
| -------- | ----------- | ---------- | --------- |
| 2        | 5000        | 2016/04/18 | Smith     |
| 3        | 8000        | 2016/04/19 | Anderson  |
| 4        | 4000        | 2016/04/20 | Jackson   |

이 예제에서는 orders.*를 사용하여 orders 테이블에서 모든 필드를 선택한 다음 customers 테이블에서 last_name 필드를 선택한다는 것을 나타냅니다.

---
## 연습 문제
SQL SELECT 문을 사용하여 자신의 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습을 통해 SELECT 문을 사용하는 실력을 시험해 볼 수 있습니다.  
각 연습이 끝나면 정답을 확인할 수 있도록 솔루션을 제공합니다. 한 번 도전해 보세요!

**[연습 문제로 이동](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/SELECT_Exercises.md)**

---
**[< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/README.md) / [다음 : FROM >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/FROM.md)**