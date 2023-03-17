# SQL : DELETE 문 연습 문제

SQL DELETE 문을 사용하여 실력을 테스트하고 싶다면 몇 가지 연습 문제를 풀어보세요.

이 연습 문제를 통해 DELETE 문 사용 실력을 테스트할 수 있습니다.  
각 연습이 끝나면 정답을 확인할 수 있도록 풀이가 제공됩니다.

시작하세요!

**[튜토리얼로 돌아가기](DELETE.md)**

---
## 연습 문제 #1
employees 테이블을 기준으로 salary가 $60,000보다 큰 모든 직원 기록을 삭제합니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  salary int,
  dept_id int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1001, 'Smith', 'John', 62000, 500);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1002, 'Anderson', 'Jane', 57500, 500);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1003, 'Everest', 'Brad', 71000, 501);

INSERT INTO employees
(employee_number, last_name, first_name, salary, dept_id)
VALUES
(1004, 'Horvath', 'Jack', 42000, 501);
```

### 연습 문제 #1 풀이
다음 DELETE 문은 employees 테이블에서 이러한 레코드를 삭제합니다. **[Try it](https://www.techonthenet.com/sql/delete_try_sql.php)**
```SQL
DELETE FROM employees
WHERE salary > 60000;
```
2개의 레코드가 삭제되고 이제 employees 테이블은 다음과 같이 표시됩니다.

| employee_number | last_name | first_name | salary | dept_id |
| :-------------- | :-------- | :--------- | :----- | :------ |
| 1002            | Anderson  | Jane       | 57500  | 500     |
| 1004            | Horvath   | Jack       | 42000  | 501     |

---
## 연습 문제 #2
suppliers 테이블을 기준으로 state가 'California'이고 supplier_name이 Google이 아닌 공급업체 레코드를 삭제합니다.
```SQL
CREATE TABLE suppliers
( supplier_id int NOT NULL,
  supplier_name char(50) NOT NULL,
  city char(50),
  state char(50),
  CONSTRAINT suppliers_pk PRIMARY KEY (supplier_id)
);

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(100, 'Microsoft', 'Redmond', 'Washington');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(200, 'Google', 'Mountain View', 'California');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(300, 'Oracle', 'Redwood City', 'California');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(400, 'Kimberly-Clark', 'Irving', 'Texas');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(500, 'Tyson Foods', 'Springdale', 'Arkansas');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(600, 'SC Johnson', 'Racine', 'Wisconsin');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(700, 'Dole Food Company', 'Westlake Village', 'California');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(800, 'Flowers Foods', 'Thomasville', 'Georgia');

INSERT INTO suppliers
(supplier_id, supplier_name, city, state)
VALUES
(900, 'Electronic Arts', 'Redwood City', 'California');
```

### 연습 문제 #2 풀이
다음 SQL DELETE 문은 suppliers 테이블에서 이러한 레코드를 삭제합니다. **[Try it](https://www.techonthenet.com/sql/delete_try_sql.php)**
```SQL
DELETE FROM suppliers
WHERE state = 'California'
AND supplier_name <> 'Google';
```
3개의 레코드가 삭제되고 suppliers 테이블은 이제 다음과 같이 표시됩니다.

| supplier_id | supplier_name  | city          | state      |
| :---------- | :------------- | :------------ | :--------- |
| 100         | Microsoft      | Redmond       | Washington |
| 200         | Google         | Mountain View | California |
| 400         | Kimberly-Clark | Irving        | Texas      |
| 500         | Tyson Foods    | Springdale    | Arkansas   |
| 600         | SC Johnson     | Racine        | Wisconsin  |
| 800         | Flowers Foods  | Thomasville   | Georgia    |

---
**[튜토리얼로 돌아가기](DELETE.md)**