# Oracle / PLSQL : ALTER TABLE 문

이 Oracle 자습서에서는 Oracle **ALTER TABLE 문**을 사용하여 열 추가, 열 수정, 열 삭제, 열 이름 바꾸기 또는 테이블 이름 바꾸기를 수행하는 방법을 설명합니다. (구문, 예제 및 연습 문제 포함)

## 설명
Oracle ALTER TABLE 문은 테이블의 열을 추가, 수정 또는 삭제하는 데 사용됩니다. Oracle ALTER TABLE 문은 테이블 이름을 변경하는 데에도 사용됩니다.

---
## 테이블에 열 추가

### 구문
테이블에 열을 추가하려면 Oracle ALTER TABLE 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
  ADD column_name column_definition;
```

### 예제
ALTER TABLE 문을 사용하여 Oracle 테이블에 열을 추가하는 방법을 보여주는 예제를 살펴 보겠습니다.
```sql
ALTER TABLE customers
  ADD customer_name varchar2(45);
```
이 Oracle ALTER TABLE 예제는 customers 테이블에 데이터 형식이 varchar2(45)인 customer_name이라는 열을 추가합니다.

좀 더 복잡한 예제에서는 ALTER TABLE 문을 사용하여 기본값이 있는 새 열을 추가할 수 있습니다.
```sql
ALTER TABLE customers
  ADD city varchar2(40) DEFAULT 'Seattle';
```
이 예제에서는 데이터 형식이 varchar2(40), 기본값이 'Seattle'인 city라는 열이 customers 테이블에 추가되었습니다.

---
## 표에 여러 열 추가

### 구문
기존 테이블에 여러 열을 추가하려면 Oracle ALTER TABLE 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
  ADD (column_1 column_definition,
       column_2 column_definition,
       ...
       column_n column_definition);
```

### 예제
ALTER TABLE 문을 사용하여 Oracle 테이블에 여러 열을 추가하는 방법을 보여주는 예제를 살펴 보겠습니다.
```sql
ALTER TABLE customers
  ADD (customer_name varchar2(45),
       city varchar2(40) DEFAULT 'Seattle');
```
이 Oracle ALTER TABLE 예제에서는 customers 테이블에 customer_name을 varchar2(45) 필드로, city를 기본값이 'Seattle'인 varchar2(40) 필드로 하는 두 열을 추가합니다.

---
## 테이블의 열 수정

### 구문
기존 테이블의 열을 수정하려면 Oracle ALTER TABLE 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
  MODIFY column_name column_type;
```

### 예제
ALTER TABLE 문을 사용하여 Oracle 테이블의 열을 수정하는 방법을 보여주는 예제를 살펴보겠습니다.
```sql
ALTER TABLE customers
  MODIFY customer_name varchar2(100) NOT NULL;
```
이 Oracle ALTER TABLE 예제에서는 customer_name이라는 열을 데이터 형식이 varchar2(100)이 되도록 수정하고 해당 열이 null 값을 허용하지 않도록 강제합니다.

더 복잡한 예제에서는 ALTER TABLE 문을 사용하여 기본값을 추가하고 열 정의를 수정할 수 있습니다.
```sql
ALTER TABLE customers
  MODIFY city varchar2(75) DEFAULT 'Seattle' NOT NULL;
```
이 예제에서 ALTER TABLE 문은 city라는 열을 데이터 형식이 varchar2(75)로 수정하고, 기본값을 'Seattle'로 설정하며, null 값을 허용하지 않도록 열을 설정합니다.

---
## 테이블의 여러 열 수정

### 구문
기존 테이블에서 여러 열을 수정하려면 Oracle ALTER TABLE 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
  MODIFY (column_1 column_type,
          column_2 column_type,
          ...
          column_n column_type);
```

### 예제
ALTER TABLE 문을 사용하여 Oracle 테이블의 여러 열을 수정하는 방법을 보여주는 예제를 살펴 보겠습니다.
```sql
ALTER TABLE customers
  MODIFY (customer_name varchar2(100) NOT NULL,
          city varchar2(75) DEFAULT 'Seattle' NOT NULL);
```
이 Oracle ALTER TABLE 예제에서는 customer_name 및 city 열을 모두 수정합니다. customer_name 열은 varchar2(100) 데이터 형식으로 설정되며 null 값을 허용하지 않습니다. city 열은 varchar2(75) 데이터 형식으로 설정되고 기본값은 'Seattle'로 설정되며 이 열은 null 값을 허용하지 않습니다.

---
## 표에 열 놓기

### 구문
기존 테이블에서 열을 삭제하려면 Oracle ALTER TABLE 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
  DROP COLUMN column_name;
```

### 예제
ALTER TABLE 문을 사용하여 Oracle 테이블에서 열을 삭제하는 방법을 보여주는 예제를 살펴 보겠습니다.
```sql
ALTER TABLE customers
  DROP COLUMN customer_name;
```
이 Oracle ALTER TABLE 예제는 customers라는 테이블에서 customer_name이라는 열을 삭제합니다.

---
## 테이블의 열 이름 바꾸기 (Oracle 9i 릴리스 2의 신규 기능)

### 구문
Oracle 9i 릴리스 2부터 열 이름을 변경할 수 있습니다.

기존 테이블에서 열 이름을 바꾸려면 Oracle ALTER TABLE 구문을 사용합니다.
```sql
ALTER TABLE table_name
  RENAME COLUMN old_name TO new_name;
```

### 예제
ALTER TABLE 문을 사용하여 Oracle 테이블의 열 이름을 바꾸는 방법을 보여주는 예제를 살펴보겠습니다.
```sql
ALTER TABLE customers
  RENAME COLUMN customer_name TO cname;
```
이 Oracle ALTER TABLE 예제에서는 customer_name이라는 열의 이름을 cname으로 바꿉니다.

---
## 테이블 이름 바꾸기

### 구문
테이블 이름을 바꾸려면 Oracle ALTER TABLE 구문을 사용합니다.
```sql
ALTER TABLE table_name
  RENAME TO new_table_name;
```

### 예제
ALTER TABLE 문을 사용하여 Oracle에서 테이블 이름을 변경하는 방법을 보여주는 예제를 살펴보겠습니다.
```sql
ALTER TABLE customers
  RENAME TO contacts;
```
이 Oracle ALTER TABLE 예제는 customers 테이블의 이름을 contacts로 변경합니다.

---
## 연습 문제 #1
아래 departments 테이블을 기준으로 departments 테이블의 이름을 depts로 바꿉니다.
```sql
CREATE TABLE departments
( department_id number(10) NOT NULL,
  department_name varchar2(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (department_id)
);
```

### 연습 문제 풀이 #1
다음 Oracle ALTER TABLE 문은 departments 테이블의 이름을 depts로 변경합니다.
```sql
ALTER TABLE departments
  RENAME TO depts;
```

---
## 연습 문제 #2
아래 employees 테이블을 기반으로 number(6) 데이터 형식인 bonus라는 열을 추가합니다.
```sql
CREATE TABLE employees
( employee_number number(10) NOT NULL,
  employee_name varchar2(50) NOT NULL,
  department_id number(10),
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);
```

### 연습 문제 풀이 #2
다음 Oracle ALTER TABLE 문은 employees 테이블에 보너스 열을 추가합니다.
```sql
ALTER TABLE employees
  ADD bonus number(6);
```

---
## 연습 문제 #3
아래 customers 테이블을 기반으로 두 개의 열을 추가합니다. 하나는 varchar2(50) 데이터 형식인 contact_name이라는 열이고 다른 하나는 날짜 데이터 형식인 last_contacted라는 열입니다.
```sql
CREATE TABLE customers
( customer_id number(10) NOT NULL,
  customer_name varchar2(50) NOT NULL,
  address varchar2(50),
  city varchar2(50),
  state varchar2(25),
  zip_code varchar2(10),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);
```

### 연습 문제 풀이 #3
다음 Oracle ALTER TABLE 문은 customers 테이블에 contact_name 및 last_contacted 열을 추가합니다.
```sql
ALTER TABLE customers
  ADD (contact_name varchar2(50),
       last_contacted date);
```

---
## 연습 문제 #4
아래 employees 테이블을 기반으로 employee_name 열을 varchar2(75) 데이터 형식으로 변경합니다.
```sql
CREATE TABLE employees
( employee_number number(10) NOT NULL,
  employee_name varchar2(50) NOT NULL,
  department_id number(10),
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);
```

### 연습 문제 풀이 #4
다음 Oracle ALTER TABLE 문은 employee_name 열의 데이터 형식을 varchar2(75)로 변경합니다.
```sql
ALTER TABLE employees
  MODIFY employee_name varchar2(75);
```

---
## 연습 문제 #5
아래 customers 테이블을 기반으로 customer_name 열을 null 값 허용 안 함으로 변경하고 state 열을 varchar2(2) 데이터 형식으로 변경합니다.
```sql
CREATE TABLE customers
( customer_id number(10) NOT NULL,
  customer_name varchar2(50),
  address varchar2(50),
  city varchar2(50),
  state varchar2(25),
  zip_code varchar2(10),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);
```

### 연습 문제 풀이 #5
다음 Oracle ALTER TABLE 문은 customers 테이블에서 customer_name 및 state 열을 적절하게 수정합니다.
```sql
ALTER TABLE customers
  MODIFY (customer_name varchar2(50) NOT NULL,
          state varchar2(2));
```

---
## 연습 문제 #6
아래 employees 테이블을 기준으로 salary 열을 삭제합니다.
```sql
CREATE TABLE employees
( employee_number number(10) NOT NULL,
  employee_name varchar2(50) NOT NULL,
  department_id number(10),
  salary number(6),
  CONSTRAINT employees_pk PRIMARY KEY (employee_number)
);
```

### 연습 문제 풀이 #6
다음 Oracle ALTER TABLE 문은 employees 테이블에서 salary 열을 삭제합니다.
```sql
ALTER TABLE employees
  DROP COLUMN salary;
```

---
## 연습 문제 #7
아래 departments 테이블에 따라 department_name 열의 이름을 dept_name으로 바꿉니다.
```sql
CREATE TABLE departments
( department_id number(10) NOT NULL,
  department_name varchar2(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (department_id)
);
```

### 연습 문제 풀이 #7
다음 Oracle ALTER TABLE 문은 departments 테이블에서 department_name 열의 이름을 dept_name으로 변경합니다.
```sql
ALTER TABLE departments
  RENAME COLUMN department_name TO dept_name;
```

---
**[< 이전](Primary_Keys.md) / [다음 : DROP TABLE >](DROP_TABLE.md)**