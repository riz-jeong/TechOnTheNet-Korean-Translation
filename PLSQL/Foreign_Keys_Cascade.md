# Oracle / PLSQL : Cascade Delete를 사용한 외래 키

이 Oracle 튜토리얼에서는 Oracle에서 **Cascade Delete를 사용한 외래 키**를 사용하는 방법을 구문과 예제를 통해 설명합니다.

## Oracle에서 Cascade Delete를 사용한 외래 키란 무엇인가요?
Cascade Delete가 있는 외래 키는 부모 테이블의 레코드가 삭제되면 자식 테이블의 해당 레코드가 자동으로 삭제되는 것을 의미합니다. 이를 Oracle에서는 Cascade Delete라고 합니다.

Cascade Delete를 사용한 외래 키는 CREATE TABLE 문 또는 ALTER TABLE 문에서 정의할 수 있습니다.

---
## CREATE TABLE 문 사용

### 구문
Oracle/PLSQL에서 CREATE TABLE 문을 사용하여 Cascade Delete를 사용한 외래 키를 생성하는 구문은 다음과 같습니다.
```sql
CREATE TABLE table_name
(
  column1 datatype null/not null,
  column2 datatype null/not null,
  ...

  CONSTRAINT fk_column
     FOREIGN KEY (column1, column2, ... column_n)
     REFERENCES parent_table (column1, column2, ... column_n)
     ON DELETE CASCADE
);
```

### 예제
Oracle/PLSQL에서 CREATE TABLE 문을 사용하여 Cascade Delete를 사용하여 외래 키를 생성하는 예제를 살펴보겠습니다.
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
    ON DELETE CASCADE
);
```
이 예제에서는 supplier 테이블에 supplier_pk라는 기본 키를 만들었습니다. 이 기본 키는 supplier_id 필드 하나만으로 구성됩니다. 그런 다음 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 외래 키를 products 테이블에 만들었습니다.

Cascade Delete로 인해 supplier 테이블의 레코드가 삭제되면 products 테이블에서 동일한 supplier_id 값을 가진 모든 레코드도 삭제됩니다.

아래 예제에서와 같이 둘 이상의 필드가 있는 외래 키(Cascade Delete 사용)를 만들 수도 있습니다.
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
    ON DELETE CASCADE
);
```
이 예제에서 fk_foreign_comp라는 외래 키는 supplier 테이블을 두 개의 필드, 즉 supplier_id 및 supplier_name 필드를 기반으로 참조합니다.

fk_foreign_comp라는 외래 키에 대한 Cascade Delete는 supplier 테이블의 레코드가 삭제될 때 supplier_id 및 supplier_name을 기준으로 products 테이블의 모든 해당 레코드가 Cascade Delete되도록 합니다.

---
## ALTER TABLE 문 사용

### 구문
Oracle/PLSQL의 ALTER TABLE 문에서 Cascade Delete를 사용하여 외래 키를 생성하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
   FOREIGN KEY (column1, column2, ... column_n)
   REFERENCES parent_table (column1, column2, ... column_n)
   ON DELETE CASCADE;
```

### 예제
Oracle/PLSQL에서 ALTER TABLE 문을 사용하여 Cascade Delete를 사용하여 외래 키를 생성하는 예제를 살펴보겠습니다.
```sql
ALTER TABLE products
ADD CONSTRAINT fk_supplier
  FOREIGN KEY (supplier_id)
  REFERENCES supplier(supplier_id)
  ON DELETE CASCADE;
```
이 예제에서는 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 외래 키(Cascade Delete 사용)를 만들었습니다.

아래 예제에서와 같이 둘 이상의 필드를 사용하여 외래 키(Cascade Delete 사용)를 만들 수도 있습니다.
```sql
ALTER TABLE products
ADD CONSTRAINT fk_supplier
  FOREIGN KEY (supplier_id, supplier_name)
  REFERENCES supplier(supplier_id, supplier_name)
  ON DELETE CASCADE;
```

---
**[< 이전](Foreign_Keys.md) / [다음 : Foreign Keys (set null delete) >](Foreign_Keys_Null.md)**