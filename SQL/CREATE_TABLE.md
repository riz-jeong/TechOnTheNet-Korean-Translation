# SQL : CREATE TABLE 문

이 SQL 튜토리얼에서는 구문, 예제 및 연습 문제를 통해 SQL **CREATE TABLE 문**을 사용하는 방법을 설명합니다.

## 설명
SQL CREATE TABLE 문을 사용하면 테이블을 생성하고 정의할 수 있습니다.

## 구문
SQL에서 CREATE TABLE 문의 구문은 다음과 같습니다.
```SQL
CREATE TABLE table_name
( 
  column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],
  ...
);
```
### 매개변수 및 인수
#### **table_name**
- 생성하려는 테이블의 이름입니다.
#### **column1, column2**
- 테이블에 생성하려는 열입니다. 각 열에는 데이터 유형이 있어야 합니다. 열은 NULL 또는 NOT NULL로 정의되어야 하며, 이 값을 비워두면 데이터베이스는 NULL을 기본값으로 간주합니다.

---
## 예제
SQL CREATE TABLE 예제를 살펴보겠습니다.
```SQL
CREATE TABLE suppliers
( supplier_id int NOT NULL,
  supplier_name char(50) NOT NULL,
  contact_name char(50)
);
```
이 SQL CREATE TABLE 예제에서는 열이 3개인 suppliers라는 테이블을 만듭니다.
- 첫 번째 열은 숫자 데이터 유형(최대 10자리 길이)으로 생성되며 null 값을 포함할 수 없는 supplier_id라고 합니다.
- 두 번째 열은 supplier_name이라고 하며 문자 데이터 유형(최대 50자 길이)으로 생성되며 역시 Null 값을 포함할 수 없습니다.
- 세 번째 열은 contact_name이라고 하며 문자 데이터 유형이지만 Null 값을 포함할 수 있습니다.

이제 이 SQL CREATE TABLE 문에서 유일한 문제는 테이블의 기본 키를 정의하지 않았다는 것입니다. 이 SQL CREATE TABLE 문을 수정하여 다음과 같이 supplier_id를 기본 키로 정의할 수 있습니다.
```SQL
CREATE TABLE suppliers
( supplier_id int NOT NULL,
  supplier_name char(50) NOT NULL,
  contact_name char(50),
  CONSTRAINT suppliers_pk PRIMARY KEY (supplier_id)
);
```

[기본 키에 대해 알아보세요.](Primary_Keys.md)

[외래 키에 대해 알아보세요.](Indexes.md)

---
## 연습 문제 #1
고객 ID, 이름 및 주소 정보를 저장하는 customers라는 SQL 테이블을 만듭니다.

### 연습 문제 풀이 #1
customers 테이블에 대한 SQL CREATE TABLE 문은 다음과 같습니다.
```SQL
CREATE TABLE customers
( customer_id int NOT NULL,
  customer_name char(50) NOT NULL,
  address char(50),
  city char(50),
  state char(25),
  zip_code char(10)
);
```

---
## 연습 문제 #2
고객 ID, 이름 및 주소 정보를 저장하는 customers라는 SQL 테이블을 만듭니다.

하지만 이번에는 고객 ID가 테이블의 [기본 키](Primary_Keys.md)가 되어야 합니다.

### 연습 문제 풀이 #2
customers 테이블에 대한 SQL CREATE TABLE 문은 다음과 같습니다.
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

---
## 연습 문제 #3
아래의 departments 테이블을 기반으로 직원 번호, 직원 이름, 부서 및 급여 정보를 저장하는 employees라는 SQL 테이블을 만듭니다. employees 테이블의 [기본 키](Primary_Keys.md)는 직원 번호여야 합니다. employees 테이블에 department_id 필드를 기반으로 departments 테이블을 참조하는 [외래 키](Foreign_Keys.md)를 만듭니다.
```SQL
CREATE TABLE departments
( department_id int NOT NULL,
  department_name char(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (department_id)
);
```

### 연습 문제 풀이 #3
employees 테이블에 대한 SQL CREATE TABLE 문은 다음과 같습니다.
```SQL
CREATE TABLE employees
( employee_number int NOT NULL,
  employee_name char(50) NOT NULL,
  department_id int,
  salary int,
  CONSTRAINT employees_pk PRIMARY KEY (employee_number),
  CONSTRAINT fk_departments
    FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
);
```

---
**[< 이전](Data_Types.md.md) / [다음 : CREATE TABLE AS >](CREATE_TABLE_AS.md)**