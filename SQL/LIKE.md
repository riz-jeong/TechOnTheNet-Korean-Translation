# SQL : LIKE 조건

이 SQL 튜토리얼에서는 구문, 예제 및 [연습 문제](LIKE_Exercises.md)를 통해서 SQL **LIKE 조건**(패턴 일치를 수행시키기 위해)을 사용하는 방법을 설명합니다.

## 설명
SQL LIKE 조건을 사용하면 와일드카드를 사용하여 쿼리에서 패턴 일치를 수행할 수 있습니다. LIKE 조건은 SELECT, INSERT, UPDATE, DELETE 문의 WHERE 절에 사용됩니다.

[![LIKE](https://img.youtube.com/vi/vEt7bDnXlnY/0.jpg)](https://youtu.be/vEt7bDnXlnY)

## 구문
SQL에서 LIKE 조건의 구문은 다음과 같습니다.
```SQL
expression LIKE pattern [ ESCAPE 'escape_character' ]
```
### 매개변수 및 인수
#### **expression(표현식)**
- 열 또는 필드와 같은 문자 표현식입니다.
#### **pattern(패턴)**
- 패턴 일치를 포함하는 문자 표현식입니다. 사용할 수 있는 와일드카드는 다음과 같습니다.

| 와일드카드 | 설명                                                   |
| :--------- | :----------------------------------------------------- |
| %          | 길이에 상관없이 모든 문자열(길이 0 포함)이 일치합니다. |
| _          | 단일 문자와 일치합니다.                                |

#### **ESCAPE 'escape_character'**
- 선택 사항입니다. 와일드카드 문자의 리터럴 인스턴스(예: % 또는 _)에서 패턴을 일치시킬 수 있습니다.

>팁: 문자 [데이터 형식](Data_Types.md)으로 패턴을 일치시키는 경우, 필드 길이를 채우기 위해 끝에 공백이 추가된다는 점을 기억하세요. 이로 인해 문자열 끝에서 패턴 일치에 LIKE 조건을 사용할 때 예기치 않은 결과가 발생할 수 있습니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/like_ddl.php)**

---
## 예제 - LIKE 조건에 % 와일드카드 사용
SQL LIKE 조건에서 % 와일드카드가 어떻게 작동하는지 설명하겠습니다. 와일드카드는 길이에 상관없이 모든 문자열(길이 0 포함)과 일치한다는 점을 기억하세요.

이 첫 번째 예제에서는 고객의 last_name이 'J'로 시작하는 customers 테이블의 모든 레코드를 찾고자 합니다.

이 예제에서는 다음과 같은 데이터가 있는 customers라는 테이블이 있습니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE last_name LIKE 'J%'
ORDER BY last_name;
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| customer_id | last_name | first_name | favorite_website |
| :---------- | :-------- | :--------- | :--------------- |
| 4000        | Jackson   | Joe        | techonthenet.com |
| 9000        | Johnson   | Derek      | techonthenet.com |

이 예제에서는 last_name이 'J'로 시작하는 customers 테이블의 레코드를 반환합니다. 보시다시피 last_name이 Jackson, Johnson인 레코드가 반환되었습니다.

LIKE 조건은 대소문자를 구분하지 않으므로 다음 SQL 문도 동일한 결과를 반환합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM customers
WHERE last_name LIKE 'j%'
ORDER BY last_name;
```

### LIKE 조건에 여러 개의 % 와일드카드 사용

와일드카드 %를 LIKE 조건과 함께 여러 번 사용할 수도 있습니다.

다음과 같은 customers 테이블을 사용합니다.

| customer_id | last_name | first_name | favorite_website  |
| :---------- | :-------- | :--------- | :---------------- |
| 4000        | Jackson   | Joe        | techonthenet.com  |
| 5000        | Smith     | Jane       | digminecraft.com  |
| 6000        | Ferguson  | Samantha   | bigactivities.com |
| 7000        | Reynolds  | Allen      | checkyourmath.com |
| 8000        | Anderson  | Paige      | NULL              |
| 9000        | Johnson   | Derek      | techonthenet.com  |

customers 테이블에서 last_name에 문자 'e'가 포함된 모든 last_name 값을 찾아 보겠습니다. 다음 SQL 문을 입력합니다.
```SQL
SELECT *
FROM customers
WHERE last_name LIKE 'j%'
ORDER BY last_name;
```
3개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| last_name |
| :-------- |
| Anderson  |
| Ferguson  |
| Reynolds  |

이 예제에서 Anderson, Ferguson, Reynolds가 last_name에 문자 'e'가 포함되어 있습니다.

---
## 예제 - LIKE 조건에 _ 와일드카드 사용
다음으로 _ 와일드카드(밑줄 와일드카드)가 LIKE 조건에서 어떻게 작동하는지 설명하겠습니다. _ 와일드카드는 % 와일드카드와 달리 정확히 하나의 문자를 찾는다는 점을 기억하세요.

다음과 같은 categories 테이블을 사용합니다.

| category_id | category_name       |
| :---------- | :------------------ |
| 25          | Deli                |
| 50          | Produce             |
| 75          | Bakery              |
| 100         | General Merchandise |
| 125         | Technology          |

categories 테이블에서 category_id가 2자리 길이이고 '5'로 끝나는 모든 레코드를 찾아보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM categories
WHERE category_id LIKE '_5';
```
2개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| category_id | category_name |
| :---------- | :------------ |
| 25          | Deli          |
| 75          | Bakery        |

이 예제에서는 category_id 값이 25와 75인 2개의 레코드가 패턴 일치합니다. category_id값 125는 _ 와일드카드가 단일 문자에만 일치하기 때문에 선택되지 않았습니다.

### LIKE 조건에 여러 개의 _ 와일드카드 사용

'5'로 끝나는 3자리 값에 대해 일치시키려면 _ 와일드카드를 두 번 사용해야 합니다. 다음과 같이 쿼리를 수정할 수 있습니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM categories
WHERE category_id LIKE '__5';
```
이제 category_id 값 125를 반환합니다.

| category_id | category_name |
| :---------- | :------------ |
| 125         | Technology    |

---
## 예제 - LIKE 조건에 NOT 연산자 사용
다음으로, LIKE 조건에 [NOT 연산자](NOT.md)를 사용하는 방법의 예를 살펴보겠습니다.

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

suppliers 테이블에서 supplier_name에 문자 'o'가 포함되지 않은 모든 레코드를 찾아보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/like_try_sql.php)**
```SQL
SELECT *
FROM suppliers
WHERE supplier_name NOT LIKE '%o%';
```
1개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| supplier_id | supplier_name  | city   | state |
| :---------- | :------------- | :----- | :---- |
| 400         | Kimberly-Clark | Irving | Texas |

이 예제에서는 suppliers 테이블에 supplier_name에 문자 'o'가 포함되지 않은 레코드가 하나만 있습니다.

---
## 예제 - LIKE 조건에 이스케이프 문자 사용
패턴 일치 시 '이스케이프 문자'를 사용하는 방법을 이해하는 것이 중요합니다. % 또는 _ 을 이스케이프 처리하고 대신 리터럴을 검색할 수 있습니다.

LIKE 조건에서 % 를 리터럴로 검색하고 싶다고 가정해 보겠습니다. 이스케이프 문자를 사용하여 이 작업을 수행할 수 있습니다. 이 예제에서는 LIKE 조건에서 이스케이프 문자로 ! 를 사용합니다.

>참고: 이스케이프 문자는 단일 문자로만 정의할 수 있습니다. ! 또는 # 과 같이 데이터에 자주 나타나지 않는 문자를 선택하는 것이 가장 좋습니다.

이 예제에서는 다음 데이터가 포함된 test라는 테이블을 사용합니다.

| test_id | test_value |
| :------ | :--------- |
| 1       | 10%        |
| 2       | 25%        |
| 3       | 100        |
| 4       | 99         |

test_value에 % 리터럴이 포함된 test 테이블의 모든 레코드를 반환할 수 있습니다. 다음 SQL 문을 입력합니다.
```SQL
SELECT *
FROM test
WHERE test_value LIKE '%!%%' escape '!';
```
아래가 표시되는 결과입니다.

| test_id | test_value |
| :------ | :--------- |
| 1       | 10%        |
| 2       | 25%        |

이 예제에서는 ! 문자를 이스케이프 문자로 식별합니다. LIKE 조건의 첫 번째 및 마지막 % 값은 일반 와일드카드로 처리됩니다. !%는 이스케이프된 %이므로 리터럴 % 값으로 취급됩니다.

위의 예제를 추가로 수정하여 1로 시작하고 % 리터럴을 포함하는 test_value만 반환할 수 있습니다. 다음 SQL 문을 입력합니다.
```SQL
SELECT *
FROM test
WHERE test_value LIKE '1%!%%' escape '!';
```
아래가 표시되는 결과입니다.

| test_id | test_value |
| :------ | :--------- |
| 1       | 10%        |

이 예제에서는 이번에는 하나의 레코드만 반환합니다. 1로 시작하고 % 리터럴을 포함하는 test_value가 하나만 있기 때문입니다.

---
## 자주 묻는 질문
- 질문 : [Oracle UPPER 함수](https://www.techonthenet.com/oracle/functions/upper.php)를 SQL LIKE 조건과 통합하려면 어떻게 해야 하나요? "test"라는 단어가 포함 된 모든 레코드에 대해 자유 텍스트 필드에 대해 쿼리하려고합니다. 문제는 다음과 같은 방법으로 입력 할 수 있다는 것입니다: TEST, Test, test.

- 답변: 이 질문에 답하기 위해 예를 들어 보겠습니다.
TEST, Test 또는 test 값을 포함하는 supplier_name이라는 필드가 있는 suppliers 테이블이 있다고 가정해 보겠습니다.

TEST, Test 또는 test로 저장되었는지 여부에 관계없이 "test"라는 단어가 포함된 모든 레코드를 찾으려면 다음 SQL SELECT 문 중 하나를 실행하면 됩니다.
```SQL
SELECT *
FROM suppliers
WHERE UPPER(supplier_name) LIKE ('TEST%');
```
혹은
```SQL
SELECT *
FROM suppliers
WHERE UPPER(supplier_name) LIKE UPPER('test%')
```
이러한 SQL SELECT 문은 [Oracle UPPER 함수](https://www.techonthenet.com/oracle/functions/upper.php)와 SQL LIKE 조건의 조합을 사용하여 supplier_name 필드에 해당 레코드가 TEST, Test 또는 test로 저장되었는지 여부와 관계없이 "test"라는 단어가 포함된 모든 레코드를 반환합니다.

---
## 연습 문제
SQL LIKE 조건을 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습을 통해 LIKE 조건으로 자신의 실력을 시험해 볼 수 있습니다. 풀어야 하는 문제가 주어집니다. 각 연습이 끝나면 정답을 확인할 수 있도록 솔루션을 제공합니다. 한번 도전해 보세요!

**[연습 문제로 이동](LIKE_Exercises.md)**

---
**[< 이전](IS_NOT_NULL.md) / [다음 : NOT >](NOT.md)**