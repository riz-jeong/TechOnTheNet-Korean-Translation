# SQL : 기본 키

이 SQL 튜토리얼에서는 SQL에서 **기본 키를 만들고 삭제**하는 방법을 구문과 예제를 통해 설명합니다.

## SQL에서 기본 키란 무엇인가요?
SQL에서 기본 키는 레코드를 고유하게 정의하는 단일 필드 또는 필드 조합입니다. 기본 키의 일부인 어떤 필드도 NULL 값을 포함할 수 없습니다. 테이블에는 기본 키가 하나만 있을 수 있습니다.

SQL에서 기본 키를 생성하려면 [CREATE TABLE 문](CREATE_TABLE.md) 또는 [ALTER TABLE 문](ALTER_TABLE.md)을 사용합니다.

---
## 기본 키 생성(CREATE TABLE 문)

### 구문
기본 키는 SQL에서 CREATE TABLE 문을 실행할 때 만들 수 있습니다.
```SQL
CREATE TABLE table_name
(
  column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],
  ...

  CONSTRAINT constraint_name PRIMARY KEY (pk_col1, pk_col2, ... pk_col_n)
);
```

혹은

```SQL
CREATE TABLE table_name
(
  column1 datatype CONSTRAINT constraint_name PRIMARY KEY,
  column2 datatype [ NULL | NOT NULL ],
  ...
);
```
#### **table_name**
- 생성하려는 테이블의 이름입니다.
#### **column1, column2**
- 테이블에 생성하려는 열입니다.
#### **constraint_name**
- 기본 키의 이름입니다.
#### **pk_col1, pk_col2, ... pk_col_n**
- 기본 키를 구성하는 열입니다.

### 예제
SQL에서 CREATE TABLE 문을 사용하여 기본 키를 만드는 방법의 예를 살펴보겠습니다. 기본 키가 하나의 열로만 구성된 매우 간단한 예제부터 시작하겠습니다.

예를 들어
```SQL
CREATE TABLE suppliers
( supplier_id int NOT NULL,
  supplier_name char(50) NOT NULL,
  contact_name char(50),
  CONSTRAINT suppliers_pk PRIMARY KEY (supplier_id)
);
```
이 예제에서는 suppliers 테이블에 suppliers_pk라는 기본 키를 만들었습니다. 이 키는 supplier_id 열이라는 하나의 열로만 구성됩니다.

대체 구문을 사용하여 다음과 같이 동일한 기본 키를 만들 수도 있습니다.
```SQL
CREATE TABLE suppliers
( supplier_id int CONSTRAINT suppliers_pk PRIMARY KEY,
  supplier_name char(50) NOT NULL,
  contact_name char(50)
);
```
이 두 구문은 하나의 필드만 있는 기본 키를 만들 때 모두 유효합니다.

2개 이상의 열로 구성된 기본 키를 생성하는 경우 기본 키가 CREATE TABLE 문의 끝에 정의되는 첫 번째 구문만 사용하도록 제한됩니다.

예를 들어
```SQL
CREATE TABLE contacts
( last_name VARCHAR(30) NOT NULL,
  first_name VARCHAR(25) NOT NULL,
  birthday DATE,
  CONSTRAINT contacts_pk PRIMARY KEY (last_name, first_name)
);
```
이 예제에서는 last_name 및 first_name 열의 조합으로 구성된 contacts_pk라는 기본 키를 만듭니다. 따라서 last_name과 first_name의 각 조합은 contacts 테이블에서 고유해야 합니다.

---
## 기본 키 생성(ALTER TABLE 문)
테이블이 이미 존재하고 나중에 기본 키를 추가하려는 경우 ALTER TABLE 문을 사용하여 기본 키를 만들 수 있습니다.

### 구문
SQL에서 ALTER TABLE 문을 사용하여 기본 키를 만드는 구문은 다음과 같습니다.
```SQL
ALTER TABLE table_name
  ADD CONSTRAINT constraint_name
    PRIMARY KEY (column1, column2, ... column_n);
```
#### **table_name**
- 수정할 테이블의 이름입니다. 기본 키를 추가하려는 테이블입니다.
#### **constraint_name**
- 기본 키의 이름입니다.
#### **column1, column2, ... column_n**
- 기본 키를 구성하는 열입니다.

### 예제
SQL에서 ALTER TABLE 문을 사용하여 기본 키를 만드는 방법의 예제를 살펴보겠습니다. 데이터베이스에 이미 suppliers 테이블이 생성되어 있다고 가정해 보겠습니다. 다음 ALTER TABLE 문을 사용하여 suppliers 테이블에 기본 키를 추가할 수 있습니다.
```SQL
ALTER TABLE suppliers
  ADD CONSTRAINT suppliers_pk 
    PRIMARY KEY (supplier_id);
```
이 예제에서는 기존 suppliers 테이블에 suppliers_pk라는 기본 키를 만들었습니다. supplier_id 열로 구성됩니다.

아래 예제에서와 같이 둘 이상의 필드가 있는 기본 키를 만들 수도 있습니다:
```SQL
ALTER TABLE suppliers
  ADD CONSTRAINT suppliers_pk
    PRIMARY KEY (supplier_id, supplier_name);
```
이 예제에서는 supplier_id 및 supplier_name 열의 조합으로 구성된 suppliers_pk라는 기본 키를 생성합니다.

---
## 기본 키 삭제
SQL에서는 ALTER TABLE 문을 사용하여 기본 키를 삭제할 수 있습니다.

### 구문
SQL에서 기본 키를 삭제하는 구문은 다음과 같습니다.
```SQL
ALTER TABLE table_name
  DROP PRIMARY KEY;
```
#### **table_name**
- 수정할 테이블의 이름입니다. 삭제하려는 기본 키가 있는 테이블입니다.

### 예제
SQL에서 ALTER TABLE 문을 사용하여 기본 키를 삭제하는 방법의 예를 살펴보겠습니다.
```SQL
ALTER TABLE suppliers
  DROP PRIMARY KEY;
```
이 예제에서는 suppliers 테이블에 기본 키를 삭제했습니다. 테이블에는 기본 키가 하나만 있을 수 있으므로 기본 키의 이름을 지정할 필요가 없습니다.

---
**[< 이전](CREATE_TABLE_AS.md) / [다음 : ALTER TABLE >](ALTER_TABLE.md)**