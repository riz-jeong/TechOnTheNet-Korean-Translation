# Oracle / PLSQL : UPDATE 문

이 Oracle 튜토리얼에서는 구문, 예제 및 연습 문제를 통해 Oracle UPDATE 문을 사용하는 방법을 설명합니다.

## 설명
Oracle UPDATE 문은 Oracle 데이터베이스의 테이블에 있는 기존 레코드를 업데이트하는 데 사용됩니다. 기존 업데이트를 수행하는지 또는 다른 테이블의 데이터로 한 테이블을 업데이트하는지에 따라 Oracle의 업데이트 쿼리에는 두 가지 구문이 있습니다.

## 구문
Oracle/PLSQL에서 하나의 테이블을 업데이트할 때 UPDATE 문의 구문은 다음과 같습니다.
```SQL
UPDATE table
SET column1 = expression1,
    column2 = expression2,
    ...
    column_n = expression_n
[WHERE conditions];
```
OR

한 테이블을 다른 테이블의 데이터로 업데이트할 때 Oracle UPDATE 문의 구문은 다음과 같습니다.
```SQL
UPDATE table1
SET column1 = (SELECT expression1
               FROM table2
               WHERE conditions)
[WHERE conditions];
```
### 매개변수 및 인수
#### **column1, column2, ... column_n**
- 업데이트하려는 열입니다.
#### **expression1, expression2, ... expression_n**
- column1, column2, ... column_n에 할당할 새 값입니다. 따라서 column1에는 expression1의 값이 할당되고, column2에는 expression2의 값이 할당되는 식으로 할당됩니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 업데이트를 실행하기 위해 충족해야 하는 조건입니다. 조건을 제공하지 않으면 테이블의 모든 레코드가 업데이트됩니다.

---
## 예제 - 단일 열 업데이트
아주 간단한 Oracle UPDATE 쿼리 예제를 살펴보겠습니다.
```SQL
UPDATE customers
SET last_name = 'Anderson'
WHERE customer_id = 5000;
```
이 Oracle UPDATE 예제는 customers 테이블에서 customer_id가 5000인 last_name을 'Anderson'으로 업데이트합니다.

---
## 예제 - 여러 열 업데이트
단일 UPDATE 문으로 둘 이상의 열을 업데이트할 수 있는 Oracle UPDATE 예제를 살펴보겠습니다.
```SQL
UPDATE customers
SET state = 'California',
    customer_rep = 32
WHERE customer_id > 100;
```
여러 열을 업데이트하려는 경우 열/값 쌍을 쉼표로 구분하여 이 작업을 수행할 수 있습니다.

이 Oracle UPDATE 문 예제에서는 state를 'California'로 업데이트하고 customer_id가 100보다 큰 경우 customer_rep를 32로 업데이트합니다.

---
## 예제 - 다른 테이블의 데이터로 테이블 업데이트
다른 테이블의 데이터로 테이블을 업데이트하는 방법을 보여주는 Oracle UPDATE 예제를 살펴보겠습니다.
```SQL
UPDATE customers
SET c_details = (SELECT contract_date
                 FROM suppliers
                 WHERE suppliers.supplier_name = customers.customer_name)
WHERE customer_id < 1000;
```
이 UPDATE 예제는 customer_id가 1000보다 작은 모든 레코드에 대해 customers 테이블만 업데이트합니다. suppliers 테이블의 supplier_name이 customers 테이블의 customer_name과 일치하면 suppliers 테이블의 contract_date가 customers 테이블의 c_details 필드에 복사됩니다.

---
## 예제 - EXISTS 절 사용
Oracle에서 더 복잡한 업데이트를 수행할 수도 있습니다.

다른 테이블의 값을 기반으로 한 테이블의 레코드를 업데이트하고 싶을 수 있습니다. Oracle UPDATE 문에는 둘 이상의 테이블을 나열할 수 없으므로 Oracle [EXISTS 절](EXISTS.md)을 사용할 수 있습니다.
```SQL
UPDATE suppliers
SET supplier_name = (SELECT customers.customer_name
                     FROM customers
                     WHERE customers.customer_id = suppliers.supplier_id)
WHERE EXISTS (SELECT customers.customer_name
              FROM customers
              WHERE customers.customer_id = suppliers.supplier_id);
```
이 Oracle 업데이트 예제에서는 supplier_id가 customer_id 값과 일치할 때마다 supplier_name을 customers 테이블의 customer_name으로 덮어씁니다.

---
## 연습 문제 #1
다음 데이터로 채워진 suppliers 테이블을 기반으로 supplier_name이 "IBM"인 모든 레코드에 대해 city를 "San Francisco"로 업데이트합니다.
```SQL
CREATE TABLE suppliers
( supplier_id number(10) not null,
  supplier_name varchar2(50) not null,
  city varchar2(50),
  CONSTRAINT suppliers_pk PRIMARY KEY (supplier_id)
);

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5001, 'Microsoft', 'Chicago');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5002, 'IBM', 'Chicago');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5003, 'Red Hat', 'Detroit');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5004, 'NVIDIA', 'New York');
```

### 연습 문제 플이 #1
다음 UPDATE 문은 Oracle에서 이 업데이트를 수행합니다.
```SQL
UPDATE suppliers
SET city = 'San Francisco'
WHERE supplier_name = 'IBM';
```
이제 suppliers 테이블은 다음과 같이 표시됩니다.

| SUPPLIER_ID | SUPPLIER_NAME | CITY          |
| :---------- | :------------ | :------------ |
| 5001        | Microsoft     | Chicago       |
| 5002        | IBM           | San Francisco |
| 5003        | Red Hat       | Detroit       |
| 5004        | NVIDIA        | New York      |

---
## 연습 문제 #2
다음 데이터로 채워진 suppliers 및 customers 테이블을 기반으로 suppliers 테이블의 supplier_name이 customers 테이블의 customer_name과 일치할 때 suppliers 테이블의 city를 customers 테이블의 city로 업데이트합니다.
```SQL
CREATE TABLE suppliers
( supplier_id number(10) not null,
  supplier_name varchar2(50) not null,
  city varchar2(50),
  CONSTRAINT suppliers_pk PRIMARY KEY (supplier_id)
);

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5001, 'Microsoft', 'New York');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5002, 'IBM', 'Chicago');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5003, 'Red Hat', 'Detroit');

INSERT INTO suppliers (supplier_id, supplier_name, city)
VALUES (5005, 'NVIDIA', 'LA');

CREATE TABLE customers
( customer_id number(10) not null,
  customer_name varchar2(50) not null,
  city varchar2(50),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);

INSERT INTO customers (customer_id, customer_name, city)
VALUES (7001, 'Microsoft', 'San Francisco');

INSERT INTO customers (customer_id, customer_name, city)
VALUES (7002, 'IBM', 'Toronto');

INSERT INTO customers (customer_id, customer_name, city)
VALUES (7003, 'Red Hat', 'Newark');
```

### 연습 문제 플이 #2
다음 UPDATE 문은 Oracle에서 이 업데이트를 수행합니다.
```SQL
UPDATE suppliers
SET city = (SELECT customers.city
            FROM customers
            WHERE customers.customer_name = suppliers.supplier_name)
WHERE EXISTS (SELECT customers.city
              FROM customers
              WHERE customers.customer_name = suppliers.supplier_name);
```
이제 suppliers 테이블은 다음과 같이 표시됩니다.

| SUPPLIER_ID | SUPPLIER_NAME | CITY          |
| :---------- | :------------ | :------------ |
| 5001        | Microsoft     | San Francisco |
| 5002        | IBM           | Toronto       |
| 5003        | Red Hat       | Newark        |
| 5004        | NVIDIA        | LA            |

---
**[< 이전](INSERT_ALL.md) / [다음 : DELETE >](DELETE.md)**