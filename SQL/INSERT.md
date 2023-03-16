# SQL : INSERT 문

이 SQL 튜토리얼에서는 구문, 예제 및 [연습 문제](INSERT_Exercises.md)를 통해 SQL INSERT 문을 사용하는 방법을 설명합니다.

## 설명
SQL INSERT 문은 테이블에 하나 이상의 레코드를 삽입하는 데 사용됩니다. INSERT 문에는 하나의 레코드를 삽입하는지 여러 레코드를 삽입하는지에 따라 두 가지 구문이 있습니다.

[![INSERT](https://img.youtube.com/vi/UrbItNGZU48/0.jpg)](https://youtu.be/UrbItNGZU48)

## 구문
SQL에서 단일 레코드를 삽입할 때 INSERT 문의 구문은 다음과 같습니다.
```SQL
INSERT INTO table
(column1, column2, ... )
VALUES
(expression1, expression2, ... );
```
또는 SQL에서 여러 레코드를 삽입할 때 INSERT 문의 구문은 다음과 같습니다.
```SQL
INSERT INTO table
(column1, column2, ... )
SELECT expression1, expression2, ...
FROM source_tables
[WHERE conditions];
```

### 매개변수 및 인수
#### **table(테이블)**
- 레코드를 삽입할 테이블입니다.
#### **column1, column2**
- 값을 삽입할 테이블의 열입니다.
#### **expression1, expression2**
- 테이블의 열에 할당할 값입니다. 따라서 column1에는 expression1의 값을 할당하고 column2에는 expression2의 값을 할당하는 식으로 할당할 수 있습니다.
#### **source_tables**
- 다른 테이블에서 레코드를 삽입할 때 사용됩니다. 삽입을 수행할 때 소스 테이블입니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 다른 테이블에서 레코드를 삽입할 때 사용합니다. 삽입할 레코드가 충족되어야 하는 조건입니다.

## 참고
- SQL INSERT 문을 사용하여 테이블에 레코드를 삽입할 때는 모든 NOT NULL 열에 대해 값을 제공해야 합니다. 열이 NULL 값을 허용하는 경우에만 INSERT 문에서 열을 생략할 수 있습니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/insert_ddl.php)**

---
## 예제 - INSERT 문을 사용하여 하나의 레코드 삽입하기
INSERT 문을 사용하는 가장 간단한 방법은 VALUES 키워드를 사용하여 테이블에 하나의 레코드를 삽입하는 것입니다. SQL에서 이 작업을 수행하는 방법에 대한 예를 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 포함된 categories라는 테이블이 있습니다.

| category_id | category_name       |
| :---------- | :------------------ |
| 25          | Deli                |
| 50          | Produce             |
| 75          | Bakery              |
| 100         | General Merchandise |
| 125         | Technology          |

새 카테고리 레코드를 삽입해 보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/insert_try_sql.php)**
```SQL
INSERT INTO categories
(category_id, category_name)
VALUES
(150, 'Miscellaneous');
```
레코드 1개가 삽입됩니다. categories 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM categories;
```
다음은 표시되는 결과입니다.

| category_id | category_name       |
| :---------- | :------------------ |
| 25          | Deli                |
| 50          | Produce             |
| 75          | Bakery              |
| 100         | General Merchandise |
| 125         | Technology          |
| **150**     | **Miscellaneous**   |

이 예제에서는 categories 테이블에 레코드 하나를 삽입합니다. 이 새 레코드의 category_id는 150이고 category_name은 'Miscellaneous'입니다.

이 예제에서는 categories 테이블의 모든 열에 대한 값을 제공하므로 열 이름을 생략하고 대신 다음과 같이 INSERT 문을 작성할 수 있습니다. **[Try it](https://www.techonthenet.com/sql/insert_try_sql.php)**
```SQL
INSERT INTO categories
VALUES
(150, 'Miscellaneous');
```
그러나 이 작업은 두 가지 이유로 위험합니다. 첫째, categories 테이블에 추가 열이 추가되면 INSERT 문에 오류가 발생합니다. 둘째, 테이블에서 열의 순서가 변경되면 데이터가 잘못된 열에 삽입됩니다. 따라서 일반적으로 INSERT 문에 열 이름을 나열하는 것이 좋습니다.

---
## 예제 - INSERT 문을 사용하여 여러 레코드 삽입하기
INSERT 문 안에 SELECT 문을 배치하면 여러 개의 삽입을 빠르게 수행할 수 있습니다. 이를 수행하는 방법에 대한 예를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 employees라는 테이블이 있습니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

그리고 다음 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

이제 customers 테이블에 일부 직원 정보를 삽입해 보겠습니다. **[Try it](https://www.techonthenet.com/sql/insert_try_sql.php)**
```SQL
INSERT INTO customers
(customer_id, last_name, first_name)
SELECT employee_number AS customer_id, last_name, first_name
FROM employees
WHERE employee_number < 1003;
```

> 팁: 이 유형의 INSERT를 사용하는 일부 데이터베이스에서는 삽입하려는 테이블의 열 이름과 일치하도록 SELECT의 열 이름에 [별칭](ALIASES.md)을 지정해야 합니다. 위의 예에서 볼 수 있듯이 SELECT 문의 첫 번째 열을 customer_id로 별칭을 지정했습니다.

2개의 레코드가 삽입됩니다. customers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM customers;
```
다음은 표시되는 결과입니다.

| customer_id | last_name    | first_name | favorite_website  |
| :---------- | :----------- | :--------- | :---------------- |
| 4000        | Jackson      | Joe        | techonthenet.com  |
| 5000        | Smith        | Jane       | digminecraft.com  |
| 6000        | Ferguson     | Samantha   | bigactivities.com |
| 7000        | Reynolds     | Allen      | checkyourmath.com |
| 8000        | Anderson     | Paige      | NULL              |
| 9000        | Johnson      | Derek      | techonthenet.com  |
| **1001**    | **Smith**    | **John**   | **NULL**          |
| **1002**    | **Anderson** | **Jane**   | **NULL**          |

이 예제에서는 employees 테이블의 데이터를 사용하여 customers 테이블의 마지막 2개 레코드가 삽입되었습니다.

이러한 유형의 삽입에서는 삽입되는 행 수를 확인해야 할 수 있습니다. 삽입을 수행하기 전에 SELECT 문에서 COUNT(*)를 실행하여 삽입할 행 수를 확인할 수 있습니다. 예를 들면 다음과 같습니다. **[Try it](https://www.techonthenet.com/sql/insert_try_sql.php)**
```SQL
SELECT COUNT(*)
FROM employees
WHERE employee_number < 1003;
```
INSERT 문을 실행할 때 삽입될 레코드 수를 반환합니다.

| COUNT(*) |
| :------- |
| 2        |

---
## 자주 묻는 질문
- 질문 : 클라이언트가 있는 데이터베이스를 설정하고 있습니다. 데이터베이스에 정보를 삽입할 때 SQL INSERT 문을 사용한다는 것을 알고 있는데 동일한 클라이언트 정보를 다시 입력하지 않으려면 어떻게 해야 하나요?

- 답변: SQL [EXISTS 조건](EXISTS.md)을 사용하여 중복 정보를 삽입하지 않도록 할 수 있습니다.

예를 들어, 기본 키가 client_id인 clients라는 테이블이 있는 경우 다음 SQL INSERT 문을 사용할 수 있습니다.
```SQL
INSERT INTO clients
(client_id, client_name, client_type)
SELECT supplier_id AS client_id, supplier_name AS client_name, 'advertising' AS client_type
FROM suppliers
WHERE NOT EXISTS (SELECT *
                  FROM clients
                  WHERE clients.client_id = suppliers.supplier_id);
```
이 SQL INSERT 문은 하위 선택이 있는 여러 레코드를 삽입합니다.

단일 레코드를 삽입하려는 경우 다음 SQL INSERT 문을 사용할 수 있습니다:
```SQL
INSERT INTO clients
(client_id, client_name, client_type)
SELECT 10345, 'IBM', 'advertising'
FROM dual
WHERE NOT EXISTS (SELECT *
                  FROM clients
                  WHERE clients.client_id = 10345);
```
이중 테이블을 사용하면 값이 현재 테이블에 저장되어 있지 않더라도 선택 문에 값을 입력할 수 있습니다.

---
## 연습 문제
SQL INSERT 문을 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습을 통해 INSERT 문으로 실력을 시험해 볼 수 있습니다. 풀어야 하는 문제가 주어집니다. 각 연습이 끝나면 정답을 확인할 수 있도록 솔루션을 제공합니다. 한번 도전해 보세요!
**[연습 문제로 이동](INSERT_Exercises.md)**

---
**[< 이전](BETWEEN.md) / [다음 : NOT >](UPDATE.md)**