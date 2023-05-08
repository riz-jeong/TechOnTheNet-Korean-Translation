# Oracle / PLSQL : 외래 키 활성화

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **외래 키를 활성화**하는 방법을 설명합니다.

## 설명
Oracle에서 비활성화된 외래 키가 있을 수 있습니다. 외래 키는 ALTER TABLE 문을 사용하여 활성화할 수 있습니다.

## 구문
Oracle/PLSQL에서 외래 키를 활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ENABLE CONSTRAINT constraint_name;
```

---
## 예제
다음과 같이 외래 키를 생성한 경우.
```sql
CREATE TABLE supplier
( supplier_id numeric(10) not null,
  supplier_name varchar2(50) NOT NULL,
  CONTACT_NAME VARCHAR2(50),
  CONSTRAINT supplier_pk PRIMARY KEY (supplier_id)
);

CREATE TABLE products
( product_id numeric(10) not null,
  supplier_id numeric(10) NOT NULL,
  CONSTRAINT fk_supplier
    FOREIGN KEY (supplier_id)
    REFERENCES supplier(supplier_id)
);
```
이 예제에서는 supplier 테이블에 supplier_pk라는 기본 키를 만들었습니다. 이 기본 키는 supplier_id 필드 하나로만 구성됩니다. 그런 다음 supplier_id 필드를 기반으로 supplier 테이블을 참조하는 fk_supplier라는 외래 키를 products 테이블에 만들었습니다.

외래 키가 비활성화되어 있는데 이를 활성화하려면 다음 명령을 실행하면 됩니다.
```sql
ALTER TABLE products
ENABLE CONSTRAINT fk_supplier;
```

---
**[< 이전](Foreign_Keys_Disable.md) / [다음 : Enable Foreign key >](Foreign_Keys_Enable.md)**