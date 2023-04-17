# Oracle / PLSQL : INSERT ALL 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **INSERT ALL 문**을 사용하는 방법을 설명합니다.

## 설명
Oracle INSERT ALL 문은 단일 INSERT 문으로 여러 행을 추가하는 데 사용됩니다. 하나의 SQL 명령만 사용하여 하나의 테이블 또는 여러 테이블에 행을 삽입할 수 있습니다.

## 구문
Oracle/PLSQL에서 INSERT ALL 문의 구문은 다음과 같습니다.
```SQL
INSERT ALL
  INTO mytable (column1, column2, column_n) VALUES (expr1, expr2, expr_n)
  INTO mytable (column1, column2, column_n) VALUES (expr1, expr2, expr_n)
  INTO mytable (column1, column2, column_n) VALUES (expr1, expr2, expr_n)
SELECT * FROM dual;
```
### 매개변수 및 인수
#### **mytable
- 레코드를 삽입할 테이블입니다.
#### **column1, column2, column_n**
- 값을 삽입할 테이블의 열입니다.
#### **EXPR1, EXPR2, ... EXPR_N**
- 테이블의 열에 할당할 값입니다.

---
## 예제 - 하나의 테이블에 삽입
INSERT INTO 문을 사용하여 여러 레코드를 하나의 테이블에 삽입할 수 있습니다.

예를 들어 suppliers 테이블에 3개의 행을 삽입하려는 경우 다음 SQL 문을 실행할 수 있습니다.
```SQL
INSERT ALL
  INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM')
  INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft')
  INTO suppliers (supplier_id, supplier_name) VALUES (3000, 'Google')
SELECT * FROM dual;
```
이는 다음 3개의 INSERT 문과 동일합니다.
```SQL
INSERT INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM');

INSERT INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft');

INSERT INTO suppliers (supplier_id, supplier_name) VALUES (3000, 'Google');
```

---
## 예제 - 여러 테이블에 삽입
INSERT ALL 문을 사용하여 하나의 명령으로 여러 행을 둘 이상의 테이블에 삽입할 수도 있습니다.

예를 들어 suppliers 및 customers 테이블에 모두 삽입하려는 경우 다음 SQL 문을 실행할 수 있습니다.
```SQL
INSERT ALL
  INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM')
  INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft')
  INTO customers (customer_id, customer_name, city) VALUES (999999, 'Anderson Construction', 'New York')
SELECT * FROM dual;
```
이 예제에서는 suppliers 테이블에 2행, customers 테이블에 1행이 삽입됩니다. 이는 3개의 INSERT 문을 실행하는 것과 동일합니다.
```SQL
INSERT INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM');

INSERT INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft');

INSERT INTO customers (customer_id, customer_name, city) VALUES (999999, 'Anderson Construction', 'New York');
```

---
**[< 이전](INSERT.md) / [다음 : UPDATE >](UPDATE.md)**