# SQL : ALTER TABLE 문

이 SQL 튜토리얼에서는 명확하고 간결한 예제와 함께 SQL **ALTER TABLE 문**을 사용하여 열 추가, 열 수정, 열 삭제, 열 이름 바꾸기 또는 테이블 이름 바꾸기를 수행하는 방법을 설명합니다. 또한 직접 해볼 수 있는 몇 가지 연습 문제도 추가했습니다.

## 설명
SQL ALTER TABLE 문은 테이블의 열을 추가, 수정 또는 삭제하는 데 사용됩니다. SQL ALTER TABLE 문은 테이블 이름을 변경하는 데도 사용됩니다.

---
## 테이블에 열 추가

### 구문
테이블에 열을 추가하려면 SQL의 ALTER TABLE 구문을 사용합니다.
```SQL
ALTER TABLE table_name
  ADD column_name column_definition;
```

### 예제
열을 추가하는 SQL ALTER TABLE 예제를 살펴보겠습니다.

예를 들어
```SQL
ALTER TABLE supplier
  ADD supplier_name char(50);
```
이 SQL ALTER TABLE 예제에서는 supplier 테이블에 supplier_name이라는 열을 추가합니다.

---
## 테이블에 여러 열 추가

### 구문
기존 테이블에 여러 열을 추가하려면 SQL ALTER TABLE 구문을 사용합니다.
```SQL
ALTER TABLE table_name
  ADD (column_1 column_definition,
       column_2 column_definition,
       ...
       column_n column_definition);
```

### 예제
둘 이상의 열을 추가하는 SQL ALTER TABLE 예제를 살펴보겠습니다.

예를 들어
```SQL
ALTER TABLE supplier
  ADD (supplier_name char(50),
       city char(45));
```
이 SQL ALTER TABLE 예제에서는 supplier 테이블에 char(50) 필드인 supplier_name과 char(45) 필드인 city라는 두 열을 추가합니다.

---
## 테이블의 열 수정

### 구문
기존 테이블의 열을 수정하려면 SQL ALTER TABLE 구문을 사용합니다.

Oracle, MySQL, MariaDB의 경우
```SQL
ALTER TABLE table_name
  MODIFY column_name column_type;
```

SQL Server의 경우
```SQL
ALTER TABLE table_name
  ALTER COLUMN column_name column_type;
```

PostgreSQL의 경우
```SQL
ALTER TABLE table_name
  ALTER COLUMN column_name TYPE column_definition;
```

### 예제
ALTER TABLE 문을 사용하여 supplier_name이라는 열을 수정하는 방법의 예를 살펴보겠습니다. 대부분의 데이터베이스에는 약간 다른 구문이 있다는 점에 유의하세요.

Oracle의 경우
```SQL
ALTER TABLE supplier
  MODIFY supplier_name char(100) NOT NULL;
```

MySQL 및 MariaDB의 경우
```SQL
ALTER TABLE supplier
  MODIFY supplier_name VARCHAR(100) NOT NULL;
```

SQL Server의 경우
```SQL
ALTER TABLE supplier
  ALTER COLUMN supplier_name VARCHAR(100) NOT NULL;
```

PostgreSQL의 경우
```SQL
ALTER TABLE supplier
  ALTER COLUMN supplier_name TYPE CHAR(100),
  ALTER COLUMN supplier_name SET NOT NULL;
```

---
## 테이블에서 여러 열 수정

### 구문
기존 테이블의 여러 열을 수정하려면 SQL ALTER TABLE 구문을 사용합니다.

Oracle의 경우
```SQL
ALTER TABLE table_name
  MODIFY (column_1 column_type,
          column_2 column_type,
          ...
          column_n column_type);
```

MySQL 및 MariaDB의 경우
```SQL
ALTER TABLE table_name
  MODIFY column_1 column_definition
    [ FIRST | AFTER column_name ],
  MODIFY column_2 column_definition
    [ FIRST | AFTER column_name ],
  ...
;
```

PostgreSQL의 경우
```SQL
ALTER TABLE table_name
  ALTER COLUMN column_name TYPE column_definition,
  ALTER COLUMN column_name TYPE column_definition,
  ...
;
```

### 예제
ALTER TABLE 문을 사용하여 둘 이상의 열을 수정하는 예제를 살펴보겠습니다. 이 예제에서는 supplier_name 및 city라는 두 열을 수정합니다.

Oracle의 경우
```SQL
ALTER TABLE supplier
  MODIFY (supplier_name char(100) NOT NULL,
          city char(75));
```

MySQL 및 MariaDB의 경우
```SQL
ALTER TABLE supplier
  MODIFY supplier_name VARCHAR(100) NOT NULL,
  MODIFY city VARCHAR(75);
```

PostgreSQL의 경우
```SQL
ALTER TABLE supplier
  ALTER COLUMN supplier_name TYPE CHAR(100),
  ALTER COLUMN supplier_name SET NOT NULL,
  ALTER COLUMN city TYPE CHAR(75);
```

---
## 테이블에서 열 제거

### 구문
기존 테이블에서 열을 삭제하려면 SQL ALTER TABLE 구문을 사용합니다.
```SQL
ALTER TABLE table_name
  DROP COLUMN column_name;
```

### 예제
테이블에서 열을 삭제하는 예제를 살펴보겠습니다.

예를 들어
```SQL
ALTER TABLE supplier
  DROP COLUMN supplier_name;
```
이 SQL ALTER TABLE 예제는 supplier라는 테이블에서 supplier_name이라는 열을 삭제합니다.

---
## 테이블에서 열 이름 바꾸기

### 구문

기존 테이블의 열 이름을 바꾸려면 SQL ALTER TABLE 구문을 사용합니다.

Oracle 및 PostgreSQL의 경우
```SQL
ALTER TABLE table_name
  RENAME COLUMN old_name TO new_name;
```

SQL Server의 경우(sp_rename이라는 저장 프로시저를 사용하여)
```SQL
sp_rename 'table_name.old_column', 'new_name', 'COLUMN';
```

MySQL 및 MariaDB의 경우
```SQL
ALTER TABLE table_name
  CHANGE COLUMN old_name TO new_name;
```

### 예제
supplier 테이블의 열 이름을 supplier_name에서 sname으로 변경하는 예제를 살펴보겠습니다.

Oracle(9i Rel2 이상) 및 PostgreSQL의 경우
```SQL
ALTER TABLE supplier
  RENAME COLUMN supplier_name TO sname;
```

SQL Server의 경우(sp_rename이라는 저장 프로시저를 사용하여)
```SQL
sp_rename 'supplier.supplier_name', 'sname', 'COLUMN';
```

MySQL 및 MariaDB의 경우
```SQL
ALTER TABLE supplier
  CHANGE COLUMN supplier_name sname VARCHAR(100);
```

MySQL 및 MariaDB에서는 열 이름을 변경할 때 열의 데이터 유형을 지정해야 합니다.

---
## 테이블 이름 바꾸기

### 구문
테이블 이름을 바꾸려면 SQL ALTER TABLE 구문을 사용합니다.

Oracle, MySQL, MariaDB, PostgreSQL, SQLite의 경우
```SQL
ALTER TABLE table_name
  RENAME TO new_table_name;
```

SQL Server의 경우(sp_rename이라는 저장 프로시저 사용)
```SQL
sp_rename 'table_name', 'new_table_name';
```

### 예제
supplier라는 테이블의 이름을 새 이름인 vendor로 변경하는 예를 살펴보겠습니다.

Oracle, MySQL, MariaDB, PostgreSQL, SQLite의 경우
```SQL
ALTER TABLE supplier
  RENAME TO vendor;
```

SQL Server의 경우(sp_rename이라는 저장 프로시저 사용)
```SQL
sp_rename 'supplier', 'vendor';
```

---
## 연습 문제 #1
아래 departments 테이블을 기준으로 departments 테이블의 이름을 depts로 바꿉니다.
```SQL
CREATE TABLE departments
( department_id int NOT NULL,
  department_name char(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (department_id)
);
```

### 연습 문제 풀이 #1
다음 SQL ALTER TABLE 문은 departments 테이블의 이름을 depts로 변경합니다.
```SQL
ALTER TABLE departments
  RENAME TO depts;
```

---
## 연습 문제 #2
아래 employees 테이블을 기반으로 int 데이터 유형인 salary라는 열을 추가합니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  employee_name char(50) NOT NULL,
  department_id int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);
```

### 연습 문제 풀이 #2
다음 SQL ALTER TABLE 문은 employees 테이블에 salary 열을 추가합니다.
```SQL
ALTER TABLE employees
  ADD salary int;
```

---
## 연습 문제 #3
아래 customers 테이블을 기반으로 두 개의 열을 추가합니다. 하나는 char(50) 데이터 유형인 contact_name이라는 열이고 다른 하나는 날짜 데이터 유형인 last_contacted라는 열입니다.
```SQL
CREATE TABLE customers
( customer_id int NOT NULL,
  customer_name char(50) NOT NULL,
  address char(50),
  city char(50),
  state char(25),
  zip_code char(10),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);
```

### 연습 문제 풀이 #3
다음 SQL ALTER TABLE 문은 customers 테이블에 contact_name 및 last_contacted 열을 추가합니다:
```SQL
ALTER TABLE customers
  ADD (contact_name char(50),
       last_contacted date);
```

---
## 연습 문제 #4
아래 employees 테이블을 기반으로 employee_name 열을 char(75) 데이터 유형으로 변경합니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  employee_name char(50) NOT NULL,
  department_id int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);
```

### 연습 문제 풀이 #4
다음 SQL ALTER TABLE 문은 employee_name 열의 데이터 유형을 char(75)로 변경합니다.
```SQL
ALTER TABLE employees
  MODIFY employee_name char(75);
```

---
## 연습 문제 #5
아래 customers 테이블을 기반으로 customer_name 열을 null 값 허용 안 함으로 변경하고 state 열을 char(2) 데이터 유형으로 변경합니다.
```SQL
CREATE TABLE customers
( customer_id int NOT NULL,
  customer_name char(50),
  address char(50),
  city char(50),
  state char(25),
  zip_code char(10),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);
```

### 연습 문제 풀이 #5
다음 SQL ALTER TABLE 문은 customers 테이블에서 customer_name 및 state 열을 적절하게 수정합니다.
```SQL
ALTER TABLE customers
  MODIFY (customer_name char(50) NOT NULL,
          state char(2));
```

---
## 연습 문제 #6
아래 employees 표를 기준으로 salary 열을 삭제합니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  employee_name char(50) NOT NULL,
  department_id int,
  salary int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);
```

### 연습 문제 풀이 #6
다음 SQL ALTER TABLE 문은 employees 테이블에서 salary 열을 삭제합니다:
```SQL
ALTER TABLE employees
  DROP COLUMN salary;
```

---
## 연습 문제 #7
아래 departments 표에 따라 department_name 열의 이름을 dept_name으로 바꿉니다.
```SQL
CREATE TABLE departments
( department_id int NOT NULL,
  department_name char(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (department_id)
);
```

### 연습 문제 풀이 #7
다음 SQL ALTER TABLE 문은 departments 테이블에서 department_name 열의 이름을 dept_name으로 변경합니다.
```SQL
ALTER TABLE departments
  RENAME COLUMN department_name to dept_name;
```

---
**[< 이전](Primary_Keys.md) / [다음 : DROP TABLE >](DROP_TABLE.md)**