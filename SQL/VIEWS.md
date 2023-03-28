# SQL : 뷰

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL 뷰를 만들고, 업데이트하고, 삭제하는 방법을 설명합니다.

## 설명
SQL 뷰는 본질적으로 물리적으로 존재하지 않는 가상 테이블입니다. 오히려 하나 이상의 테이블을 조인하는 SQL 문에 의해 생성됩니다.

---
## SQL 뷰 만들기

### 구문
SQL에서 CREATE VIEW 문의 구문은 다음과 같습니다.
```SQL
CREATE VIEW view_name AS
  SELECT columns
  FROM tables
  [WHERE conditions];
```
#### **view_name**
- 생성하려는 SQL 뷰의 이름입니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드가 뷰에 포함되기 위해 충족되어야 하는 조건입니다.

### 예제
다음은 SQL CREATE VIEW를 사용하는 방법의 예입니다.
```SQL
CREATE VIEW sup_orders AS
  SELECT suppliers.supplier_id, orders.quantity, orders.price
  FROM suppliers
  INNER JOIN orders
  ON suppliers.supplier_id = orders.supplier_id
  WHERE suppliers.supplier_name = 'IBM';
```
이 SQL CREATE VIEW 예제는 select 문의 결과 집합을 기반으로 가상 테이블을 생성합니다. 이제 다음과 같이 SQL 뷰를 쿼리할 수 있습니다.
```SQL
SELECT *
FROM sup_orders;
```

---
## SQL 뷰 업데이트
SQL CREATE 또는 REPLACE VIEW 문을 사용하여 삭제하지 않고 SQL 뷰의 정의를 수정할 수 있습니다.

### 구문
SQL CREATE OR REPLACE VIEW 문의 구문은 다음과 같습니다.
```SQL
CREATE OR REPLACE VIEW view_name AS
  SELECT columns
  FROM table
  [WHERE conditions];
```

### 예제
다음은 SQL CREATE OR REPLACE VIEW 문을 사용하는 방법의 예입니다.
```SQL
CREATE or REPLACE VIEW sup_orders AS
  SELECT suppliers.supplier_id, orders.quantity, orders.price
  FROM suppliers
  INNER JOIN orders
  ON suppliers.supplier_id = orders.supplier_id
  WHERE suppliers.supplier_name = 'Microsoft';
```
이 SQL CREATE OR REPLACE VIEW 예제는 sup_orders라는 SQL 뷰의 정의를 삭제하지 않고 업데이트합니다. SQL 뷰가 아직 존재하지 않는 경우, SQL 뷰가 처음으로 생성될 뿐입니다.

---
## SQL 뷰 삭제
SQL 뷰가 생성되면 SQL DROP VIEW 문을 사용하여 뷰를 삭제할 수 있습니다.

### 구문
SQL DROP VIEW 문의 구문은 다음과 같습니다.
```SQL
DROP VIEW view_name;
```
#### **view_name**
- 삭제하려는 뷰의 이름입니다.

### 예제
다음은 SQL DROP VIEW 문을 사용하는 방법의 예입니다.
```SQL
DROP VIEW sup_orders;
```
이 SQL DROP VIEW 예제는 sup_orders라는 SQL 뷰를 삭제합니다.

---
## 자주 묻는 질문
- 질문 : SQL 뷰에서 데이터를 업데이트할 수 있나요?

- 답변 : SQL의 뷰는 하나 이상의 테이블을 조인하여 만들어집니다. 뷰에서 레코드를 업데이트하면 SQL 뷰를 구성하는 기초 테이블의 레코드가 업데이트됩니다.

    따라서 기본 SQL 테이블에 대한 적절한 권한이 있는 경우 SQL 뷰에서 데이터를 업데이트할 수 있습니다.

---

- 질문 : 테이블이 데이터베이스에서 삭제된 경우 SQL 뷰가 존재하나요?

- 답변 : 예, Oracle에서는 SQL 뷰의 기반이 되는 테이블 중 하나가 데이터베이스에서 삭제된 후에도 SQL 뷰는 계속 존재합니다. 그러나 테이블이 삭제된 후 SQL 뷰를 쿼리하려고 하면 SQL 뷰에 오류가 있음을 나타내는 메시지가 표시됩니다.

    삭제한 테이블을 다시 생성하면 SQL VIEW가 다시 정상적으로 작동합니다.

---
**[< 이전](DROP_TABLE.md) / [다음 : GLOBAL TEMP >](GLOBAL_TEMP.md)**