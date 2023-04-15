# SQL : JOINS

이 SQL 자습서에서는 구문, 일러스트 및 예제를 통해 SQL **JOINS**를 사용하는 방법을 설명합니다.

## 설명
SQL JOIN은 여러 테이블에서 데이터를 검색하는 데 사용됩니다. SQL 조인은 SQL 문에 두 개 이상의 테이블이 나열될 때마다 수행됩니다.

SQL 조인에는 4가지 유형이 있습니다:

- SQL INNER JOIN(단순 조인이라고도 함)
- SQL LEFT OUTER JOIN(LEFT JOIN이라고도 함)
- SQL RIGHT OUTER JOIN(RIGHT JOIN이라고도 함)
- SQL FULL OUTER JOIN(FULL JOIN이라고도 함)

이제 SQL JOIN 구문에 대해 논의하고, SQL JOIN의 시각적 그림을 살펴보고, 몇 가지 예제를 살펴보겠습니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/joins_ddl.php)**

---
## SQL INNER JOIN(단순 조인)
이미 SQL INNER JOIN을 사용하는 SQL 문을 작성했을 가능성이 높습니다. 가장 일반적인 유형의 SQL 조인입니다. SQL INNER JOIN은 조인 조건이 충족되는 여러 테이블의 모든 행을 반환합니다.

### 구문
SQL에서 INNER JOIN의 구문은 다음과 같습니다.
```SQL
SELECT columns
FROM table1 
INNER JOIN table2
ON table1.column = table2.column;
```

### 일러스트
이 다이어그램에서 SQL INNER JOIN은 음영 처리된 영역을 반환합니다.

![INNER JOIN](Visual-Illustration/inner_join.gif)

SQL INNER JOIN은 table1과 table2가 교차하는 레코드를 반환합니다.

### 예제
쿼리에서 INNER JOIN을 사용하는 방법의 예를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

그리고 다음 데이터가 있는 orders라는 테이블이 있습니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT customers.customer_id, orders.order_id, orders.order_date
FROM customers 
INNER JOIN orders
ON customers.customer_id = orders.customer_id
ORDER BY customers.customer_id;
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | order_id | order_date |
| :---------- | :------- | :--------- |
| 4000        | 4        | 2016/04/20 |
| 5000        | 2        | 2016/04/18 |
| 7000        | 1        | 2016/04/18 |
| 8000        | 3        | 2016/04/19 |

이 예제에서는 customers 테이블과 orders 테이블 모두에 일치하는 customer_id 값이 있는 customers 및 orders 테이블의 모든 행을 반환합니다.

customers 테이블에서 customer_id가 6000 및 9000인 행은 두 테이블에 모두 존재하지 않으므로 생략됩니다. orders 테이블에서 order_id가 5인 행은 customers 테이블에 NULL의 customer_id가 존재하지 않으므로 생략됩니다.

#### 옛 구문
마지막으로, 위의 INNER JOIN 예제는 이전 암시적 구문을 사용하여 다음과 같이 다시 작성할 수 있다는 점을 언급할 필요가 있습니다. (하지만 여전히 INNER JOIN 키워드 구문을 사용하는 것이 좋습니다) **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT customers.customer_id, orders.order_id, orders.order_date
FROM customers, orders
WHERE customers.customer_id = orders.customer_id
ORDER BY customers.customer_id;
```

---
## SQL LEFT OUTER JOIN
또 다른 조인 유형은 LEFT OUTER JOIN이라고 합니다. 이 조인 유형은 ON 조건에 지정된 왼쪽 테이블의 모든 행과 조인된 필드가 동일한 다른 테이블의 행만 반환합니다. (조인 조건이 충족됨)

### 구문
SQL에서 LEFT OUTER JOIN의 구문은 다음과 같습니다.
```SQL
SELECT columns
FROM table1
LEFT [OUTER] JOIN table2
ON table1.column = table2.column;
```
일부 데이터베이스에서는 OUTER 키워드가 생략되고 단순히 LEFT JOIN으로 작성됩니다.

### 일러스트
이 다이어그램에서 SQL LEFT OUTER JOIN은 음영 처리된 영역을 반환합니다.

![LEFT OUTER JOIN](Visual-Illustration/left_outer_join.gif)

SQL LEFT OUTER JOIN은 table1의 모든 레코드와 table2의 레코드 중 table1과 교차하는 레코드만 반환합니다.

### 예제
이제 SELECT 문에서 LEFT OUTER JOIN을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이전 예와 동일한 customers 테이블을 사용합니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

그리고 다음 데이터가 포함된 orders 테이블입니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT customers.customer_id, orders.order_id, orders.order_date
FROM customers 
LEFT OUTER JOIN orders
ON customers.customer_id = orders.customer_id
ORDER BY customers.customer_id;
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | order_id | order_date |
| :---------- | :------- | :--------- |
| 4000        | 4        | 2016/04/20 |
| 5000        | 2        | 2016/04/18 |
| 6000        | NULL     | NULL       |
| 7000        | 1        | 2016/04/18 |
| 8000        | 3        | 2016/04/19 |
| 9000        | NULL     | NULL       |

이 LEFT OUTER JOIN 예제는 customers 테이블의 모든 행과 조인된 필드가 동일한 orders 테이블의 행만 반환합니다.

customers 테이블의 customer_id 값이 orders 테이블에 존재하지 않는 경우 orders 테이블의 모든 필드가 결과 집합에 NULL로 표시됩니다. 보시다시피, customer_id가 6000 및 9000인 행은 LEFT OUTER JOIN을 통해 포함되지만 order_id 및 order_date 필드는 NULL로 표시됩니다.

---
## SQL RIGHT OUTER JOIN
또 다른 조인 유형은 SQL RIGHT OUTER JOIN이라고 합니다. 이 유형의 조인은 ON 조건에 지정된 오른쪽 테이블의 모든 행과 조인된 필드가 동일한 다른 테이블의 행만 반환합니다. (조인 조건이 충족됨)

### 구문
SQL에서 RIGHT OUTER JOIN의 구문은 다음과 같습니다.
```SQL
SELECT columns
FROM table1
RIGHT [OUTER] JOIN table2
ON table1.column = table2.column;
```
일부 데이터베이스에서는 OUTER 키워드가 생략되고 단순히 RIGHT JOIN으로 작성됩니다.

### 일러스트
이 다이어그램에서 SQL 오른쪽 외부 조인은 음영 처리된 영역을 반환합니다.

![RIGHT OUTER JOIN](Visual-Illustration/right_outer_join.gif)

SQL RIGHT OUTER JOIN은 table2의 모든 레코드와 table1의 레코드 중 table2와 교차하는 레코드만 반환합니다.

### 예제
이제 SELECT 문에서 RIGHT OUTER JOIN을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이전 예제와 동일한 customers 테이블을 사용합니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

그리고 다음 데이터가 포함된 orders 테이블입니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT customers.customer_id, orders.order_id, orders.order_date
FROM customers 
RIGHT OUTER JOIN orders
ON customers.customer_id = orders.customer_id
ORDER BY customers.customer_id;
```
5개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | order_id | order_date |
| :---------- | :------- | :--------- |
| NULL        | 5        | 2016/05/01 |
| 4000        | 4        | 2016/04/20 |
| 5000        | 2        | 2016/04/18 |
| 7000        | 1        | 2016/04/18 |
| 8000        | 3        | 2016/04/19 |

이 RIGHT OUTER JOIN 예제는 orders 테이블의 모든 행과 조인된 필드가 동일한 customers 테이블의 행만 반환합니다.

orders 테이블의 customer_id 값이 customers 테이블에 존재하지 않는 경우 customers 테이블의 모든 필드가 결과 집합에 NULL로 표시됩니다. 보시다시피, order_id가 5인 행은 RIGHT OUTER JOIN을 통해 포함되지만 customer_id 필드는 NULL로 표시됩니다.

---
## SQL FULL OUTER JOIN
또 다른 조인 유형은 SQL FULL OUTER JOIN이라고 합니다. 이 유형의 조인은 왼쪽 테이블과 오른쪽 테이블의 모든 행을 반환하며, 조인 조건이 충족되지 않는 위치에는 NULL 값이 있습니다.

### 구문
SQL FULL OUTER JOIN의 구문은 다음과 같습니다.
```SQL
SELECT columns
FROM table1
FULL [OUTER] JOIN table2
ON table1.column = table2.column;
```
일부 데이터베이스에서는 OUTER 키워드가 생략되고 단순히 FULL JOIN으로 작성됩니다.

### 일러스트
이 다이어그램에서 SQL FULL OUTER JOIN은 음영 처리된 영역을 반환합니다.

![FULL OUTER JOIN](Visual-Illustration/full_outer_join.gif)

SQL FULL OUTER JOIN은 table1과 table2의 양쪽 모든 레코드를 반환합니다.

### 예제
SELECT 문에서 FULL OUTER JOIN을 사용하는 방법을 보여주는 예제를 살펴보겠습니다.

이전 예와 동일한 customers 테이블을 사용합니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

그리고 다음 데이터가 포함된 orders 테이블입니다.

| order_id | customer_id | order_date |
| :------- | :---------- | :--------- |
| 1        | 7000        | 2016/04/18 |
| 2        | 5000        | 2016/04/18 |
| 3        | 8000        | 2016/04/19 |
| 4        | 4000        | 2016/04/20 |
| 5        | NULL        | 2016/05/01 |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/joins_try_sql.php)**
```SQL
SELECT customers.customer_id, orders.order_id, orders.order_date
FROM customers 
FULL OUTER JOIN orders
ON customers.customer_id = orders.customer_id
ORDER BY customers.customer_id;
```
7개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | order_id | order_date |
| :---------- | :------- | :--------- |
| NULL        | 5        | 2016/05/01 |
| 4000        | 4        | 2016/04/20 |
| 5000        | 2        | 2016/04/18 |
| 6000        | NULL     | NULL       |
| 7000        | 1        | 2016/04/18 |
| 8000        | 3        | 2016/04/19 |
| 9000        | NULL     | NULL       |

이 FULL OUTER JOIN 예제는 orders 테이블의 모든 행과 customers 테이블의 모든 행을 반환합니다. 조인 조건이 충족되지 않을 때마다 결과 집합의 해당 필드에 NULL 값이 확장됩니다. 즉, customers 테이블의 customer_id 값이 orders 테이블에 존재하지 않는 경우 orders 테이블의 모든 필드가 결과 집합에 NULL로 표시됩니다. 또한 orders 테이블의 customer_id 값이 customers 테이블에 존재하지 않는 경우 customers 테이블의 모든 필드가 결과 집합에서 NULL로 표시됩니다.

보시다시피, customer_id가 6000 및 9000인 행은 포함되지만 해당 레코드의 order_id 및 order_date 필드에는 NULL 값이 포함됩니다. order_id가 5인 행도 포함되지만 해당 레코드의 customer_id 필드에는 NULL 값이 있습니다.

---
**[< 이전](ALIASES.md) / [다음 : BETWEEN >](BETWEEN.md)**