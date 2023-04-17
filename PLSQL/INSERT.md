# Oracle / PLSQL : INSERT 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **INSERT 문**을 사용하는 방법을 설명합니다. 또한 직접 시도해 볼 수 있는 몇 가지 연습 문제도 추가했습니다.

## 설명
Oracle INSERT 문은 Oracle의 테이블에 단일 레코드 또는 여러 레코드를 삽입하는 데 사용됩니다.

## 구문
VALUES 키워드를 사용하여 단일 레코드를 삽입할 때 Oracle INSERT 문의 구문은 다음과 같습니다.
```SQL
INSERT INTO table
(column1, column2, ... column_n )
VALUES
(expression1, expression2, ... expression_n );
```
또는 SELECT 문을 사용하여 여러 레코드를 삽입할 때 Oracle INSERT 문의 구문은 다음과 같습니다.
```SQL
INSERT INTO table
(column1, column2, ... column_n )
SELECT expression1, expression2, ... expression_n
FROM source_table
[WHERE conditions];
```
### 매개 변수 및 인수
#### **table**
- 레코드를 삽입할 테이블입니다.
#### **column1, column2, ... column_n**
- 값을 삽입할 테이블의 열입니다.
#### **EXPRESSION1, EXPRESSION2, ... EXPRESSION_N**
- 테이블의 열에 할당할 값입니다. 따라서 column1에는 expression1의 값이 할당되고 column2에는 expression2의 값이 할당되는 식으로 할당됩니다.
#### **source_table**
- 다른 테이블에서 데이터를 삽입할 때 소스 테이블입니다.
#### **(WHERE 조건)**
- 선택 사항입니다. 삽입할 레코드에 대해 충족해야 하는 조건입니다.

## 참고
- Oracle INSERT 문을 사용하여 테이블에 레코드를 삽입하는 경우 모든 NOT NULL 열에 대해 값을 제공해야 합니다.
- 열이 NULL 값을 허용하는 경우 Oracle INSERT 문에서 열을 생략할 수 있습니다.

---
## 예제 - VALUES 키워드 사용
VALUES 키워드를 사용하여 값을 나열하는 Oracle INSERT 쿼리를 생성하는 가장 간단한 방법입니다.
```SQL
INSERT INTO suppliers
(supplier_id, supplier_name)
VALUES
(5000, 'Apple');
```
이 Oracle INSERT 문은 suppliers 테이블에 하나의 레코드를 삽입하는 결과를 가져옵니다. 이 새 레코드의 supplier_id는 5000이고 supplier_name은 'Apple'이 됩니다.

---
## 예제 - SELECT 문 사용
SELECT 문을 사용하여 더 복잡한 Oracle INSERT 문을 만들 수도 있습니다.
```SQL
INSERT INTO suppliers
(supplier_id, supplier_name)
SELECT account_no, name
FROM customers
WHERE customer_id > 5000;
```
INSERT 문 안에 SELECT 문을 배치하면 여러 개의 삽입을 빠르게 수행할 수 있습니다.

이 유형의 삽입에서는 삽입되는 행 수를 확인해야 할 수 있습니다. 삽입을 수행하기 전에 다음 Oracle SELECT 문을 실행하여 삽입할 행 수를 확인할 수 있습니다.
```SQL
SELECT count(*)
FROM customers
WHERE customer_id > 5000;
```

---
## 자주 묻는 질문
- 질문 : 클라이언트가 있는 데이터베이스를 설정하고 있습니다. 데이터베이스에 정보를 삽입할 때 Oracle INSERT 문을 사용한다는 것을 알고 있는데 동일한 클라이언트 정보를 다시 입력하지 않으려면 어떻게 해야 하나요?

- 답변 : [EXISTS 조건](EXISTS.md)을 사용하여 중복 정보를 삽입하지 않도록 할 수 있습니다.

예를 들어 기본 키가 client_id인 clients 테이블이 있는 경우 다음과 같은 Oracle INSERT 문을 사용할 수 있습니다.
```SQL
INSERT INTO clients
(client_id, client_name, client_type)
SELECT supplier_id, supplier_name, 'advertising'
FROM suppliers
WHERE NOT EXISTS (SELECT *
                  FROM clients
                  WHERE clients.client_id = suppliers.supplier_id);
```
이 Oracle INSERT 문은 하위 선택이 있는 여러 레코드를 삽입합니다.

단일 레코드를 삽입하려는 경우 다음 Oracle INSERT 문을 사용할 수 있습니다.
```SQL
INSERT INTO clients
(client_id, client_name, client_type)
SELECT 10345, 'IBM', 'advertising'
FROM dual
WHERE NOT EXISTS (SELECT *
                  FROM clients
                  WHERE clients.client_id = 10345);
```
듀얼 테이블을 사용하면 값이 현재 테이블에 저장되어 있지 않더라도 선택 문에 값을 입력할 수 있습니다.

---

- 질문 : Oracle에서 하나의 INSERT 명령에 여러 행의 명시적 데이터를 삽입하려면 어떻게 해야 합니까?
- 답변 : 다음은 Oracle INSERT 문을 사용하여 Oracle의 suppliers 테이블에 3개의 행을 삽입하는 방법의 예입니다.
```SQL
INSERT ALL
  INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM')
  INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft')
  INTO suppliers (supplier_id, supplier_name) VALUES (3000, 'Google')
SELECT * FROM dual;
```

---
## 연습 문제 #1
contacts 테이블을 기반으로 contact_id가 1000, last_name이 Smith, first_name이 Jane, address가 10 Somewhere St.인 연락처 레코드를 삽입합니다.
```SQL
CREATE TABLE contacts
( contact_id number(10) not null,
  last_name varchar2(50) not null,
  first_name varchar2(50) not null,
  address varchar2(50),
  city varchar2(50),
  state varchar2(20),
  zip_code varchar2(10),
  CONSTRAINT contacts_pk PRIMARY KEY (contact_id)
);
```

### 연습 문제 풀이 #1
다음 Oracle INSERT 문은 이 레코드를 contacts 테이블에 삽입합니다.
```SQL
INSERT INTO contacts
(contact_id, last_name, first_name, address)
VALUES
(1000, 'Smith', 'Jane', '10 Somewhere St.');
```

---
## 연습 문제 #2
contacts 및 customers 테이블을 기반으로 state가 'Florida'인 모든 고객을 contacts 테이블에 삽입합니다.
```SQL
CREATE TABLE contacts
( contact_id number(10) not null,
  last_name varchar2(50) not null,
  first_name varchar2(50) not null,
  address varchar2(50),
  city varchar2(50),
  state varchar2(20),
  zip_code varchar2(10),
  CONSTRAINT contacts_pk PRIMARY KEY (contact_id)
);

CREATE TABLE customers
( customer_id number(10) not null,
  last_name varchar2(50) not null,
  first_name varchar2(50) not null,
  address varchar2(50),
  city varchar2(50),
  state varchar2(20),
  zip_code varchar2(10),
  CONSTRAINT customers_pk PRIMARY KEY (customer_id)
);
```

### 연습 문제 풀이 #2
다음 Oracle INSERT 문은 이 레코드를 contacts 테이블에 삽입합니다.
```SQL
INSERT INTO contacts
(contact_id, last_name, first_name, address, city, state, zip_code)
SELECT customer_id, last_name, first_name, address, city, state, zip_code
FROM customers
WHERE state = 'Florida';
```
contacts 및 customers 테이블의 필드 수가 동일하고 필드가 동일한 순서로 나열되므로 다음과 같이 솔루션을 작성할 수 있습니다. (일반적으로 테이블 정의가 변경될 경우를 대비하여 열 이름을 나열하는 것이 더 좋습니다)
```SQL
INSERT INTO contacts
SELECT *
FROM customers
WHERE state = 'Florida';
```

---
**[< 이전](BETWEEN.md) / [다음 : INSERT ALL >](INSERT_ALL.md)**