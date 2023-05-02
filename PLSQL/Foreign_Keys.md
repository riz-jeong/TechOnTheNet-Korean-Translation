# Oracle / PLSQL : 외래 키

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **외래 키**를 사용하는 방법을 설명합니다.

## Oracle에서 외래 키란 무엇인가요?
외래 키는 Oracle 데이터베이스 내에서 참조 무결성을 강화하는 방법입니다. 외래 키는 한 테이블의 값이 다른 테이블에도 나타나야 함을 의미합니다.

참조된 테이블을 부모 테이블이라고 하고 외래 키가 있는 테이블을 자식 테이블이라고 합니다. 자식 테이블의 외래 키는 일반적으로 부모 테이블의 [기본 키](Primary_Keys.md)를 참조합니다.

외래 키는 CREATE TABLE 문 또는 ALTER TABLE 문에서 정의할 수 있습니다.

---
## CREATE TABLE 문 사용

### 구문
CREATE TABLE 문을 사용하여 외래 키를 생성하는 구문은 다음과 같습니다.
```sql
CREATE TABLE table_name
(
  column1 datatype null/not null,
  column2 datatype null/not null,
  ...

  CONSTRAINT fk_column
    FOREIGN KEY (column1, column2, ... column_n)
    REFERENCES parent_table (column1, column2, ... column_n)
);
```

### 예제
```sql
CREATE TABLE supplier
( supplier_id numeric(10) not null,
  supplier_name varchar2(50) not null,
  contact_name varchar2(50),
  CONSTRAINT supplier_pk PRIMARY KEY (supplier_id)
);

CREATE TABLE products
( product_id numeric(10) not null,
  supplier_id numeric(10) not null,
  CONSTRAINT fk_supplier
    FOREIGN KEY (supplier_id)
    REFERENCES supplier(supplier_id)
);
```
이 예제에서는 supplier 테이블에 supplier_pk라는 기본 키를 만들었습니다. 이 기본 키는 supplier_id 필드라는 하나의 필드로만 구성됩니다. 그런 다음 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 외래 키를 products 테이블에 만들었습니다.

아래 예제에서와 같이 둘 이상의 필드가 있는 외래 키를 만들 수도 있습니다.
```sql
CREATE TABLE supplier
( supplier_id numeric(10) not null,
  supplier_name varchar2(50) not null,
  contact_name varchar2(50),
  CONSTRAINT supplier_pk PRIMARY KEY (supplier_id, supplier_name)
);

CREATE TABLE products
( product_id numeric(10) not null,
  supplier_id numeric(10) not null,
  supplier_name varchar2(50) not null,
  CONSTRAINT fk_supplier_comp
    FOREIGN KEY (supplier_id, supplier_name)
    REFERENCES supplier(supplier_id, supplier_name)
);
```
이 예제에서 fk_foreign_comp라는 외래 키는 supplier_id 및 supplier_name 필드라는 두 필드를 기반으로 supplier 테이블을 참조합니다.

---
## ALTER TABLE 문 사용

### 구문
ALTER TABLE 문에서 외래 키를 생성하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
   FOREIGN KEY (column1, column2, ... column_n)
   REFERENCES parent_table (column1, column2, ... column_n);
```

### 예제
```sql
ALTER TABLE products
ADD CONSTRAINT fk_supplier
  FOREIGN KEY (supplier_id)
  REFERENCES supplier(supplier_id);
```
이 예제에서는 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 외래 키를 만들었습니다.

아래 예제에서처럼 둘 이상의 필드를 사용하여 외래 키를 만들 수도 있습니다.
```sql
ALTER TABLE products
ADD CONSTRAINT fk_supplier
  FOREIGN KEY (supplier_id, supplier_name)
  REFERENCES supplier(supplier_id, supplier_name);
```

---
**[< 이전](LOCAL_TEMP.md) / [다음 : Foreign Keys (cascade delete) >](Foreign_Keys_Cascade.md)**