# Oracle / PLSQL : VIEW

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **VIEW를 만들고, 업데이트하고, 삭제**하는 방법을 설명합니다.

## Oracle에서 VIEW란 무엇인가요?
Oracle VIEW는 본질적으로 물리적으로 존재하지 않는 가상 테이블입니다. 그보다는 하나 이상의 테이블을 [조인](JOINS.md)하는 쿼리에 의해 생성됩니다.

---
## 뷰 만들기
### 구문
Oracle/PLSQL의 CREATE VIEW 문 구문은 다음과 같습니다.
```sql
CREATE VIEW view_name AS
  SELECT columns
  FROM tables
  [WHERE conditions];
```
#### **view_name**
- 생성하려는 Oracle VIEW의 이름입니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드가 뷰에 포함되기 위해 충족되어야 하는 조건입니다.

### 예제
다음은 Oracle CREATE VIEW를 사용하는 방법의 예입니다.
```sql
CREATE VIEW sup_orders AS
  SELECT suppliers.supplier_id, orders.quantity, orders.price
  FROM suppliers
  INNER JOIN orders
  ON suppliers.supplier_id = orders.supplier_id
  WHERE suppliers.supplier_name = 'Microsoft';
```
이 Oracle CREATE VIEW 예제는 SELECT 문의 결과 집합을 기반으로 가상 테이블을 생성합니다. 이제 다음과 같이 Oracle VIEW를 쿼리할 수 있습니다.
```sql
SELECT *
FROM sup_orders;
```

---
## 뷰 업데이트
Oracle CREATE 또는 REPLACE VIEW 문을 사용하여 삭제하지 않고 Oracle VIEW의 정의를 수정할 수 있습니다.

### 구문
Oracle/PLSQL에서 CREATE OR REPLACE VIEW 문의 구문은 다음과 같습니다.
```sql
CREATE OR REPLACE VIEW view_name AS
  SELECT columns
  FROM table
  WHERE conditions;
```
#### **view_name**
- 만들거나 바꾸려는 Oracle VIEW의 이름입니다.

### 예제
다음은 Oracle CREATE OR REPLACE VIEW 문을 사용하는 예입니다.
```sql
CREATE or REPLACE VIEW sup_orders AS
  SELECT suppliers.supplier_id, orders.quantity, orders.price
  FROM suppliers
  INNER JOIN orders
  ON suppliers.supplier_id = orders.supplier_id
  WHERE suppliers.supplier_name = 'Apple';
```
이 Oracle CREATE OR REPLACE VIEW 예제는 sup_orders라는 Oracle VIEW의 정의를 삭제하지 않고 업데이트합니다. Oracle VIEW가 아직 존재하지 않는 경우, 이 뷰는 단지 처음 생성될 뿐입니다.

---
## 뷰 삭제
Oracle VIEW가 생성되면 Oracle DROP VIEW 문을 사용하여 삭제할 수 있습니다.

### 구문
Oracle/PLSQL의 DROP VIEW 문 구문은 다음과 같습니다.
```sql
DROP VIEW view_name;
```
#### **view_name**
- 삭제하려는 뷰의 이름입니다.

### 예제
다음은 Oracle DROP VIEW 문을 사용하는 예제입니다.
```sql
DROP VIEW sup_orders;
```
이 Oracle DROP VIEW 예제는 sup_orders라는 Oracle VIEW를 삭제합니다.

---
## 자주 묻는 질문
- 질문 : Oracle VIEW에서 데이터를 업데이트할 수 있나요?

- 답변 : Oracle의 뷰는 하나 이상의 테이블을 조인하여 생성됩니다. 뷰에서 레코드를 업데이트하면 뷰를 구성하는 기초 테이블의 레코드가 업데이트됩니다.

    따라서 네, 기본 Oracle 테이블에 대한 적절한 권한이 있는 경우 Oracle VIEW에서 데이터를 업데이트할 수 있습니다.

---

- 질문 : 테이블이 데이터베이스에서 삭제된 경우에도 Oracle 뷰가 존재합니까?

- 답변 : 네, Oracle에서는 Oracle 뷰의 기반이 되는 테이블 중 하나가 데이터베이스에서 삭제된 후에도 뷰가 계속 존재합니다. 그러나 테이블이 삭제된 후 Oracle VIEW를 쿼리하려고 하면 Oracle VIEW에 오류가 있음을 나타내는 메시지가 표시됩니다.

    테이블(삭제한 테이블)을 다시 생성하면 Oracle VIEW가 다시 정상적으로 작동합니다.

---
**[< 이전](DROP_TABLE.md) / [다음 : GLOBAL TEMP >](GLOBAL_TEMP.md)**