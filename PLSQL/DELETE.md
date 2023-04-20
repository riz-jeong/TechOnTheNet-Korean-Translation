# Oracle / PLSQL : DELETE 문

이 Oracle 튜토리얼에서는 구문, 예제 및 연습 문제를 통해 Oracle DELETE 문을 사용하는 방법을 설명합니다.

## 설명
Oracle DELETE 문은 Oracle의 테이블에서 단일 레코드 또는 여러 레코드를 삭제하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 DELETE 문의 구문은 다음과 같습니다.
```SQL
DELETE FROM table
[WHERE conditions];
```
### 매개변수 및 인수
#### **table**
- 레코드를 삭제할 테이블입니다.
#### **WHERE 조건**
- 선택 사항입니다. 삭제할 레코드에 대해 충족해야 하는 조건입니다. 조건을 제공하지 않으면 테이블의 모든 레코드가 삭제됩니다.

## 참고
테이블에서 전체 행을 삭제하므로 Oracle DELETE 문에 필드를 나열할 필요가 없습니다.

---
## 예제 - 하나의 조건 사용
DELETE 문에 조건이 하나만 있는 간단한 Oracle DELETE 쿼리 예제를 살펴보겠습니다.
```SQL
DELETE FROM customers
WHERE last_name = 'Smith';
```
이 Oracle DELETE 예제는 last_name이 Smith인 customers 테이블에서 모든 레코드를 삭제합니다.

삭제될 행 수를 확인할 수 있습니다. 삭제를 수행하기 전에 다음 Oracle SELECT 문을 실행하여 삭제될 행 수를 확인할 수 있습니다.
```SQL
SELECT count(*)
FROM customers
WHERE last_name = 'Smith';
```

---
## 예제 - 두 개의 조건 사용
DELETE 문에 두 개의 조건만 있는 Oracle DELETE 예제를 살펴보겠습니다.
```SQL
DELETE FROM customers
WHERE last_name = 'Anderson'
AND customer_id > 25;
```
이 Oracle DELETE 예제는 customers 테이블에서 last_name이 'Anderson'이고 customer_id가 25보다 큰 모든 레코드를 삭제합니다.

삭제할 행 수를 확인할 수 있습니다. 삭제를 수행하기 전에 다음 Oracle SELECT 문을 실행하여 삭제될 행 수를 확인할 수 있습니다.
```SQL
SELECT count(*)
FROM customers
WHERE last_name = 'Anderson'
AND customer_id > 25;
```

---
## 예제 - EXISTS 절 사용
더 복잡한 삭제를 수행할 수도 있습니다.

다른 테이블의 값을 기반으로 한 테이블의 레코드를 삭제하고 싶을 수 있습니다. 삭제를 수행할 때 Oracle FROM 절에 둘 이상의 테이블을 나열할 수 없으므로 Oracle EXISTS 절을 사용할 수 있습니다.
```SQL
DELETE FROM suppliers
WHERE EXISTS
  ( SELECT customers.customer_name
    FROM customers
    WHERE customers.customer_id = suppliers.supplier_id
    AND customer_id > 25 );
```
이 Oracle DELETE 예제는 customers 테이블에 customer_id가 25보다 큰 레코드가 있고 customer_id가 supplier_id와 일치하는 suppliers 테이블의 모든 레코드를 삭제합니다.

삭제할 행 수를 확인하려는 경우 삭제를 수행하기 전에 다음 Oracle SELECT 문을 실행할 수 있습니다.
```SQL
SELECT COUNT(*) FROM suppliers
WHERE EXISTS
  ( SELECT customers.customer_name
    FROM customers
    WHERE customers.customer_id = suppliers.supplier_id
    AND customer_id > 25 );
```

---
## 자주 묻는 질문
- 질문 : field1 및 field2의 데이터가 TableB의 fieldx 및 fieldz의 데이터와 일치하지 않는 TableA의 모든 레코드를 삭제하기 위해 Oracle DELETE 문을 작성하려면 어떻게 해야 합니까?

- 답변 : Oracle DELETE 문에 다음과 같이 시도해 볼 수 있습니다.
```SQL
DELETE FROM TableA
WHERE NOT EXISTS
  ( SELECT *
    FROM TableB
    WHERE TableA.field1 = TableB.fieldx
    AND TableA.field2 = TableB.fieldz );
```

---
## 연습 문제 #1
contacts 테이블을 기반으로 contacts 테이블에서 city가 'Las Vegas'고 first_name이 'Jane'인 모든 레코드를 삭제합니다.
```SQL
CREATE TABLE contacts
( contact_id number(10) not null,
  last_name varchar2(50) not null,
  first_name varchar2(50) not null,
  address varchar2(50),
  city varchar2(50),
  state varchar2(2),
  zip_code varchar2(10),
  CONSTRAINT contacts_pk PRIMARY KEY (contact_id)
);
```

### 연습 문제 풀이 #1
다음 Oracle DELETE 문은 contacts 테이블에서 이러한 레코드를 삭제합니다.
```SQL
DELETE FROM contacts
WHERE city = 'Las Vegas'
AND first_name = 'Jane';
```

---
## 연습 문제 #2
contacts 테이블을 기준으로 contacts 테이블에서 contact_id가 5000 이상 6000 미만인 모든 레코드를 삭제합니다.
```SQL
CREATE TABLE contacts
( contact_id number(10) not null,
  last_name varchar2(50) not null,
  first_name varchar2(50) not null,
  address varchar2(50),
  city varchar2(50),
  state varchar2(2),
  zip_code varchar2(10),
  CONSTRAINT contacts_pk PRIMARY KEY (contact_id)
);
```

### 연습 문제 풀이 #2
다음 Oracle DELETE 문은 contacts 테이블에서 이러한 레코드를 삭제합니다.
```SQL
DELETE FROM contacts
WHERE contact_id >= 5000
AND contact_id < 6000;
```
또는 다음과 같이 BETWEEN 절을 사용하여 솔루션을 작성할 수도 있습니다.
```SQL
DELETE FROM contacts
WHERE contact_id BETWEEN 5000 AND 5999;
```

---
**[< 이전](UPDATE.md) / [다음 : TRUNCATE >](TRUNCATE.md)**