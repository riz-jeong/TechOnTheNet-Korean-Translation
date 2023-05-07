# Oracle / PLSQL : Null on Delete 설정된 외래 키

이 Oracle 튜토리얼에서는 Oracle에서 Null on Delete로 설정된 외래 키를 사용하는 방법을 구문과 예제를 통해 설명합니다.

## Oracle에서 Null on Delete로 설정된 외래 키란 무엇인가요?
Null on Delete로 설정이 있는 외래 키는 상위 테이블의 레코드가 삭제되면 하위 테이블의 해당 레코드에 외래 키 필드가 NULL로 설정됨을 의미합니다. 하위 테이블의 레코드는 삭제되지 않습니다.

Null on Delete로 설정이 있는 외래 키는 CREATE TABLE 문 또는 ALTER TABLE 문에서 정의할 수 있습니다.

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
     ON DELETE SET NULL
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
  supplier_id numeric(10),
  CONSTRAINT fk_supplier
    FOREIGN KEY (supplier_id)
    REFERENCES supplier(supplier_id)
    ON DELETE SET NULL
);
```
이 예제에서는 supplier 테이블에 supplier_pk라는 기본 키를 만들었습니다. 이 기본 키는 supplier_id 필드 하나로만 구성됩니다. 그런 다음 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 외래 키를 products 테이블에 만들었습니다.

삭제 시 null로 설정되어 있으므로 supplier 테이블의 레코드가 삭제되면 products 테이블의 모든 해당 레코드에 supplier_id 값이 null로 설정됩니다.

아래 예제에서와 같이 둘 이상의 필드를 사용하여 Null on Delete로 설정하는 외래 키를 만들 수도 있습니다.
```sql
CREATE TABLE supplier
( supplier_id numeric(10) not null,
  supplier_name varchar2(50) not null,
  contact_name varchar2(50),
  CONSTRAINT supplier_pk PRIMARY KEY (supplier_id, supplier_name)
);

CREATE TABLE products
( product_id numeric(10) not null,
  supplier_id numeric(10),
  supplier_name varchar2(50),
  CONSTRAINT fk_supplier_comp
    FOREIGN KEY (supplier_id, supplier_name)
    REFERENCES supplier(supplier_id, supplier_name)
    ON DELETE SET NULL
);
```
이 예제에서 fk_foreign_comp라는 외래 키는 supplier_id 및 supplier_name 필드라는 두 필드를 기반으로 supplier 테이블을 참조합니다.

supplier 테이블의 레코드가 삭제되면 supplier 테이블의 supplier_id 및 supplier_name 필드를 기준으로 fk_foreign_comp라는 외래 키가 삭제되면 products 테이블의 모든 해당 레코드가 supplier_id 및 supplier_name 필드를 null로 설정하게 됩니다.

---
## ALTER TABLE 문 사용

### 구문
ALTER TABLE 문에서 외래 키를 생성하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
   FOREIGN KEY (column1, column2, ... column_n)
   REFERENCES parent_table (column1, column2, ... column_n)
   ON DELETE SET NULL;
```

### 예제
```sql
ALTER TABLE products
ADD CONSTRAINT fk_supplier
  FOREIGN KEY (supplier_id)
  REFERENCES supplier(supplier_id)
  ON DELETE SET NULL;
```
이 예제에서는 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 Null on Delete로 설정된 외래 키를 만들었습니다.

아래 예제에서와 같이 둘 이상의 필드를 사용하여 Null on Delete로 설정된 외래 키를 만들 수도 있습니다.
```sql
ALTER TABLE products
ADD CONSTRAINT fk_supplier
  FOREIGN KEY (supplier_id, supplier_name)
  REFERENCES supplier(supplier_id, supplier_name)
  ON DELETE SET NULL;
```

---
**[< 이전](Foreign_Keys_Cascade.md) / [다음 : Drop Foreign Key >](Foreign_Keys_Drop.md)**