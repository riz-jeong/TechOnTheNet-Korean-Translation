# SQL: ALIASES

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **ALIASES** (열 또는 테이블의 임시 이름)를 사용하는 방법을 설명합니다.

## 설명
SQL ALIASES을 사용하여 열 또는 테이블의 임시 이름을 만들 수 있습니다.

- **열 ALIASES**는 결과 집합의 열 머리글을 읽기 쉽게 만드는 데 사용됩니다.
- **테이블 ALIASES**는 읽기 쉽도록 SQL을 줄이거나 자체 조인을 수행할 때 사용됩니다. (예: FROM 절에 동일한 테이블을 두 번 이상 나열하는 경우)

[![ALIASES](https://img.youtube.com/vi/ngPeJ06f4-A/0.jpg)](https://youtu.be/ngPeJ06f4-A)

## 구문
SQL에서 열에 ALIASES을 지정하는 구문은 다음과 같습니다.
```SQL
column_name [AS] alias_name
```
SQL에서 테이블에 ALIASES을 지정하는 구문은 다음과 같습니다.
```SQL
table_name [AS] alias_name
```
### 매개변수 및 인수
#### **column_name**
- 별칭을 지정하려는 열의 원래 이름입니다.
#### **table_name**
- 별칭을 지정하려는 테이블의 원래 이름입니다.
#### **alias_name**
- 할당할 임시 이름입니다.

## 참고
- alias_name에 공백이 포함되어 있으면 따옴표로 묶어야 합니다.
- 열 이름에 별칭을 지정할 때 공백을 사용할 수 있습니다. 그러나 일반적으로 테이블 이름에 별칭을 지정할 때 공백을 사용하는 것은 좋지 않습니다.
- alias_name은 SQL 문의 범위 내에서만 유효합니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/alias_ddl.php)**

---
## 예제 - 열 이름에 별칭을 지정하는 방법
일반적으로 별칭은 결과 집합의 열 이름을 더 읽기 쉽게 만드는 데 사용됩니다. 가장 일반적으로 쿼리에서 MIN, MAX, AVG, SUM 또는 COUNT와 같은 집계 함수를 사용할 때 열에 별칭을 지정합니다.

SQL에서 열 이름을 별칭으로 지정하는 방법에 대한 예를 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 employees라는 테이블이 있습니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1001            | Smith     | John       | 62000  | 500     |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1003            | Everest   | Brad       | 71000  | 501     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

열에 별칭을 지정하는 방법을 보여 드리겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/alias_try_sql.php)**
```SQL
SELECT dept_id, COUNT(*) AS total
FROM employees
GROUP BY dept_id;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| dept_id | total |
| :------ | :---- |
| 500     | 2     |
| 501     | 2     |

이 예제에서는 COUNT(*) 필드의 별칭을 total로 지정했습니다. 따라서 결과 집합이 반환될 때 두 번째 열의 제목으로 total이 표시됩니다. alias_name에 공백이 포함되지 않았으므로 alias_name을 따옴표로 묶을 필요가 없습니다.

이제 열 별칭에 공백을 포함하도록 쿼리를 다시 작성해 보겠습니다.
```SQL
SELECT dept_id, COUNT(*) AS "total employees"
FROM employees
GROUP BY dept_id;
```

| dept_id | total employees |
| :------ | :-------------- |
| 500     | 2               |
| 501     | 2               |

이 예제에서는 COUNT(*) 필드의 별칭을 "total employees"로 지정하여 결과 집합의 두 번째 열의 제목이 되도록 했습니다. 이 열 별칭에는 공백이 있으므로 SQL 문에서 "total employees"를 따옴표로 묶어야 합니다.

---
## 예제 - 테이블 이름 별칭을 지정하는 방법
테이블에 별칭을 붙이는 이유는 [FROM 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/FROM.md)에 동일한 테이블 이름을 두 번 이상 나열하려는 경우(예: 자체 조인)이거나 테이블 이름을 줄여 SQL 문을 더 짧고 읽기 쉽게 만들려는 경우입니다.

SQL에서 테이블 이름을 별칭으로 지정하는 방법의 예를 살펴보겠습니다.

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

그리고 다음 데이터가 포함된 categories라는 테이블이 있습니다.

| category_id | category_name       |
| :---------- | :------------------ |
| 25          | Deli                |
| 50          | Produce             |
| 75          | Bakery              |
| 100         | General Merchandise |
| 125         | Technology          |

이제 이 두 테이블을 조인하고 각 테이블 이름에 별칭을 지정해 보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/alias_try_sql.php)**
```SQL
SELECT p.product_name, c.category_name
FROM products AS p
INNER JOIN categories AS c
ON p.category_id = c.category_id
WHERE p.product_name <> 'Pear';
```
5개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| product_name | category_name |
| :----------- | :------------ |
| Banana       | Produce       |
| Orange       | Produce       |
| Apple        | Produce       |
| Bread        | Bakery        |
| Sliced Ham   | Deli          |

이 예제에서는 products 테이블에 대한 별칭과 카테고리 테이블에 대한 별칭을 만들었습니다. 이제 이 SQL 문에서 products 테이블을 p로, 카테고리 테이블을 c로 참조할 수 있습니다.

테이블 별칭을 만들 때 FROM 절에 나열된 모든 테이블에 대해 별칭을 만들 필요는 없습니다. 일부 또는 모든 테이블에 별칭을 만들도록 선택할 수 있습니다.

---
**[< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/NOT.md) / [다음 : NOT >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/JOINS.md)**