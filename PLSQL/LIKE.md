# Oracle / PLSQL : LIKE 조건

이 Oracle 튜토리얼에서는 구문, 예제 및 연습 문제를 통해 Oracle **LIKE 조건**(패턴 일치를 수행하기 위해)을 사용하는 방법을 설명합니다.

## 설명
Oracle LIKE 조건을 사용하면 와일드카드를 SELECT, INSERT, UPDATE 또는 DELETE 문의 WHERE 절에 사용할 수 있습니다. 이를 통해 패턴 일치를 수행할 수 있습니다.

## 구문
Oracle/PLSQL에서 LIKE 조건의 구문은 다음과 같습니다.
```SQL
expression LIKE pattern [ ESCAPE 'escape_character' ]
```
### 매개변수 및 인수
#### **expression(표현식)**
- 열 또는 필드와 같은 문자 표현식입니다.
#### **pattern**
- 패턴 일치를 포함하는 문자 표현식입니다. 선택할 수 있는 패턴은 다음과 같습니다.

| 와일드카드 | 설명                                                    |
| :--------- | :------------------------------------------------------ |
| %          | 모든 길이의 문자열(0 길이 포함)을 일치시킬 수 있습니다. |
| _          | 단일 문자로 일치시킬 수 있습니다.                       |

#### escape_character
- 선택 사항입니다. 와일드카드 문자의 리터럴 인스턴스(예: % 또는 _)를 테스트할 수 있습니다.

## 참고
- Oracle [REGEXP_LIKE 조건](REGEXP_LIKE.md)도 참조하세요.

---
## 예제 - % 와일드카드 사용(퍼센트 기호 와일드카드)
첫 번째로 살펴볼 Oracle LIKE 예제는 % 와일드카드(퍼센트 기호 와일드카드)를 사용하는 것입니다.

Oracle LIKE 조건에서 % 와일드카드가 어떻게 작동하는지 설명하겠습니다. last_name이 'Ap'로 시작하는 모든 고객을 찾고자 합니다.
```SQL
SELECT last_name
FROM customers
WHERE last_name LIKE 'Ap%';
```
동일한 문자열 내에서 % 와일드카드를 여러 번 사용할 수도 있습니다.
```SQL
SELECT last_name
FROM customers
WHERE last_name LIKE '%er%';
```
이 Oracle LIKE 조건 예제에서는 last_name에 'er' 문자가 포함된 모든 고객을 찾고 있습니다.

---
## 예제 - _ 와일드카드 사용(밑줄 와일드카드)
Oracle LIKE 조건에서 _ 와일드카드(밑줄 와일드카드)가 어떻게 작동하는지 설명해 보겠습니다. 와일드카드는 한 문자만 찾는다는 점을 기억하세요.
```SQL
SELECT supplier_name
FROM suppliers
WHERE supplier_name LIKE 'Sm_th';
```
이 Oracle LIKE 조건 예제는 supplier_name이 5자이고 처음 두 문자가 'Sm'이고 마지막 두 문자가 'th'인 모든 공급업체를 반환합니다. 예를 들어, 공급업체 이름이 'Smith', 'Smyth', 'Smath', 'Smeth' 등인 공급업체를 반환할 수 있습니다.

다음은 또 다른 예제입니다.
```SQL
SELECT *
FROM suppliers
WHERE account_number LIKE '92314_';
```
계정 번호를 찾고 있지만 6자리 중 5자리만 알고 있을 수 있습니다. 위의 예제에서는 잠재적으로 10개의 레코드를 다시 검색할 수 있습니다. (누락된 값은 0에서 9까지의 모든 값일 수 있음) 
계좌 번호가 다음과 같은 공급업체를 반환할 수 있습니다.

923140, 923141, 923142, 923143, 923144, 923145, 923146, 923147, 923148, 923149

---
## 예제 - NOT 연산자 사용
다음으로 와일드카드와 함께 Oracle [NOT 연산자](NOT.md)를 사용하는 방법을 살펴보겠습니다.

NOT 연산자와 함께 % 와일드카드를 사용해 보겠습니다. Oracle LIKE 조건을 사용하여 이름이 'T'로 시작하지 않는 공급업체를 찾을 수도 있습니다.
```SQL
SELECT supplier_name
FROM suppliers
WHERE supplier_name NOT LIKE 'W%';
```
Oracle LIKE 조건 앞에 NOT 연산자를 배치하면 supplier_name이 'W'로 시작하지 않는 모든 공급업체를 검색할 수 있습니다.

---
## 예제 - 이스케이프 문자 사용
패턴 일치 시 '이스케이프 문자'를 사용하는 방법을 이해하는 것이 중요합니다. 이 예제에서는 Oracle에서 이스케이프 문자를 구체적으로 다룹니다.

Oracle LIKE 조건에서 % 또는 _ 문자를 검색하고 싶다고 가정해 보겠습니다. 이스케이프 문자를 사용하여 이 작업을 수행할 수 있습니다.

이스케이프 문자는 단일 문자(길이 1)로만 정의할 수 있다는 점에 유의하세요.
```SQL
SELECT *
FROM suppliers
WHERE supplier_name LIKE 'Water!%' ESCAPE '!';
```
이 Oracle LIKE 조건 예제에서는 이스케이프 문자로 ! 문자를 식별합니다. 이 문은 이름이 Water%인 모든 공급업체를 반환합니다.

다음은 Oracle LIKE 조건에서 이스케이프 문자를 사용하는 더 복잡한 예제입니다.
```SQL
SELECT *
FROM suppliers
WHERE supplier_name LIKE 'H%!%' ESCAPE '!';
```
이 Oracle LIKE 조건 예제는 이름이 H로 시작하고 %로 끝나는 모든 공급업체를 반환합니다. 예를 들어 'Hello%'와 같은 값이 반환됩니다.

이스케이프 문자와 _ 문자를 Oracle LIKE 조건에 함께 사용할 수도 있습니다.
```SQL
SELECT *
FROM suppliers
WHERE supplier_name LIKE 'H%!_' ESCAPE '!';
```
이 Oracle LIKE 조건 예제는 이름이 H로 시작하고 _로 끝나는 모든 공급업체를 반환합니다. 예를 들어 'Hello_'와 같은 값이 반환됩니다.

---
## 자주 묻는 질문
- 질문 : Oracle [UPPER 함수](UPPER.md)를 Oracle LIKE 조건과 통합하려면 어떻게 해야 하나요? 'test'라는 단어가 포함된 모든 레코드에 대해 자유 텍스트 필드에 대해 쿼리하려고 합니다. 문제는 다음과 같은 방법으로 입력할 수 있다는 것입니다. TEST, Test, or test

- 답변 : 이 질문에 답하기 위해 한 가지 예를 살펴보겠습니다.

TEST, Test 또는 test 값을 포함하는 supplier_name이라는 필드가 있는 suppliers 테이블이 있다고 가정해 보겠습니다.

TEST, Test 또는 test로 저장되었는지 여부에 관계없이 "test"라는 단어가 포함된 모든 레코드를 찾으려면 다음 SELECT 문 중 하나를 실행하면 됩니다.
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
이러한 SELECT 문은 Oracle [UPPER 함수](UPPER.md)와 LIKE 조건의 조합을 사용하여 supplier_name 필드에 "test"라는 단어가 포함된 모든 레코드를 반환합니다. (TEST, Test 또는 test로 저장되었는지 여부와 관계없이)

---
## 연습 문제 #1
다음 데이터로 채워진 employees 테이블을 기반으로 employee_name이 문자 'h'로 끝나는 모든 레코드를 찾습니다.
```SQL
CREATE TABLE employees
( employee_number number(10) not null,
  employee_name varchar2(50) not null,
  salary number(6),
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1001, 'John Smith', 62000);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1002, 'Jane Anderson', 57500);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1003, 'Brad Everest', 71000);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1004, 'Jack Horvath', 42000);
```

### 연습 문제 풀이 #1
다음 SELECT 문은 Oracle LIKE 조건을 사용하여 employee_name이 문자 "h"로 끝나는 레코드를 반환합니다.
```SQL
SELECT *
FROM employees
WHERE employee_name LIKE '%h';
```
그러면 다음과 같은 결과 집합이 반환됩니다.

| EMPLOYEE_NUMBER | EMPLOYEE_NAME | SALARY |
| :-------------- | :------------ | :----- |
| 1001            | John Smith    | 62000  |
| 1004            | Jack Horvath  | 42000  |

---
## 연습 문제 #2
다음 데이터로 채워진 employees 테이블을 기반으로 employee_name에 문자 's'가 포함된 모든 레코드를 찾습니다.
```SQL
CREATE TABLE employees
( employee_number number(10) not null,
  employee_name varchar2(50) not null,
  salary number(6),
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1001, 'John Smith', 62000);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1002, 'Jane Anderson', 57500);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1003, 'Brad Everest', 71000);

INSERT INTO employees (employee_number, employee_name, salary)
VALUES (1004, 'Jack Horvath', 42000);
```

### 연습 문제 풀이 #2
다음 Oracle SELECT 문은 Oracle LIKE 조건을 사용하여 employee_name에 문자 "s"가 포함된 레코드를 반환합니다.
```SQL
SELECT *
FROM employees
WHERE employee_name LIKE '%s%';
```
그러면 다음과 같은 결과 집합이 반환됩니다.

| EMPLOYEE_NUMBER | EMPLOYEE_NAME | SALARY |
| :-------------- | :------------ | :----- |
| 1002            | Jane Anderson | 57500  |
| 1003            | Brad Everest  | 71000  |

---
## 연습 문제 #3
다음 데이터로 채워진 suppliers 테이블을 기반으로 supplier_id가 4자리이고 "500"으로 시작하는 모든 레코드를 찾습니다.
```SQL
INSERT INTO suppliers(supplier_id, supplier_name, city)
VALUES ('5008', 'Microsoft', 'New York');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES ('5009', 'IBM', 'Chicago');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES ('5010', 'Red Hat', 'Detroit');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES ('5011', 'NVIDIA', 'New York');
```

### 연습 문제 풀이 #3
다음 Oracle SELECT 문은 Oracle LIKE 조건을 사용하여 supplier_id가 4자리이고 "500"으로 시작하는 레코드를 반환합니다.
```SQL
SELECT *
FROM suppliers
WHERE supplier_id LIKE '500_';
```
그러면 다음과 같은 결과 집합이 반환됩니다.

| SUPPLIER_ID | SUPPLIER_NAME | CITY     |
| :---------- | :------------ | :------- |
| 5008        | Microsoft     | New York |
| 5009        | IBM           | Chicago  |

---
**[< 이전](IS_NOT_NULL.md) / [다음 : REGEXP_LIKE >](REGEXP_LIKE.md)**