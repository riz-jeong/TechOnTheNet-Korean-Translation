# Oracle / PLSQL : 기본 키

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **기본 키를 생성, 삭제, 비활성화 및 활성화**하는 방법을 설명합니다.

## Oracle에서 기본 키란 무엇인가요?
Oracle에서 **기본 키**는 레코드를 고유하게 정의하는 단일 필드 또는 필드 조합입니다. 기본 키의 일부인 필드 중 어느 것도 널 값을 포함할 수 없습니다. 테이블에는 기본 키가 하나만 있을 수 있습니다.

## 참고
- Oracle에서 기본 키는 32개 이상의 열을 포함할 수 없습니다.
- 기본 키는 CREATE TABLE 문 또는 ALTER TABLE 문에서 정의할 수 있습니다.

---
## 기본 키 만들기 - CREATE TABLE 문 사용
오라클에서 CREATE TABLE 문을 사용하여 기본 키를 생성할 수 있습니다.

### 구문
Oracle/PLSQL에서 CREATE TABLE 문을 사용하여 기본 키를 생성하는 구문은 다음과 같습니다.
```sql
CREATE TABLE table_name
(
  column1 datatype null/not null,
  column2 datatype null/not null,
  ...

  CONSTRAINT constraint_name PRIMARY KEY (column1, column2, ... column_n)
);
```

### 예제
Oracle에서 CREATE TABLE 문을 사용하여 기본 키를 만드는 방법의 예를 살펴보겠습니다.
```sql
CREATE TABLE suppliers
(
  supplier_id numeric(10) not null,
  supplier_name varchar2(50) NOT NULL,
  CONTACT_NAME VARCHAR2(50),
  CONSTRAINT supplier_pk PRIMARY KEY (supplier_id)
);
```
이 예제에서는 suppliers 테이블에 supplier_pk라는 기본 키를 만들었습니다. 이 키는 supplier_id 필드라는 하나의 필드로만 구성됩니다.

아래 예제에서와 같이 둘 이상의 필드로 기본 키를 만들 수도 있습니다.
```sql
CREATE TABLE suppliers
(
  supplier_id numeric(10) NOT NULL,
  supplier_name varchar2(50) NOT NULL,
  CONTACT_NAME VARCHAR2(50),
  CONSTRAINT supplier_pk PRIMARY KEY (supplier_id, supplier_name)
);
```

---
## 기본 키 생성 - ALTER TABLE 문 사용
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 생성할 수 있습니다.

### 구문
Oracle/PLSQL에서 ALTER TABLE 문을 사용하여 기본 키를 생성하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name PRIMARY KEY (column1, column2, ... column_n);
```

### 예제
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 생성하는 예제를 살펴보겠습니다.
```sql
ALTER TABLE suppliers
ADD CONSTRAINT supplier_pk PRIMARY KEY (supplier_id);
```
이 예제에서는 기존 suppliers 테이블에 supplier_pk라는 기본 키를 만들었습니다. 이 키는 supplier_id라는 필드로 구성됩니다.

아래 예제에서와 같이 둘 이상의 필드가 있는 기본 키를 만들 수도 있습니다.
```sql
ALTER TABLE suppliers
ADD CONSTRAINT supplier_pk PRIMARY KEY (supplier_id, supplier_name);
```

---
## 기본 키 삭제
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 삭제할 수 있습니다.

### 구문
Oracle/PLSQL에서 ALTER TABLE 문을 사용하여 기본 키를 삭제하는 구문은 다음과 같습니다:
```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

### 예제
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 삭제하는 방법의 예를 살펴보겠습니다.
```sql
ALTER TABLE suppliers
DROP CONSTRAINT supplier_pk;
```
이 예제에서는 suppliers 테이블에서 supplier_pk라는 기본 키를 삭제합니다.

---
## 기본 키 비활성화
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 비활성화할 수 있습니다.

### 구문
Oracle/PLSQL에서 ALTER TABLE 문을 사용하여 기본 키를 비활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
DISABLE CONSTRAINT constraint_name;
```

### 예제
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 비활성화하는 방법의 예를 살펴 보겠습니다.
```sql
ALTER TABLE suppliers
DISABLE CONSTRAINT supplier_pk;
```
이 예제에서는 suppliers 테이블의 기본 키인 supplier_pk를 비활성화합니다.

---
## 기본 키 활성화
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 활성화할 수 있습니다.

### 구문
Oracle/PLSQL에서 ALTER TABLE 문을 사용하여 기본 키를 활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ENABLE CONSTRAINT constraint_name;
```

### 예제
Oracle에서 ALTER TABLE 문을 사용하여 기본 키를 활성화하는 방법의 예를 살펴보겠습니다.
```sql
ALTER TABLE suppliers
ENABLE CONSTRAINT supplier_pk;
```
이 예제에서는 suppliers 테이블에서 supplier_pk라는 기본 키를 활성화합니다.

---
**[< 이전](CREATE_TABLE_AS.md) / [다음 : ALTER TABLE >](ALTER_TABLE.md)**