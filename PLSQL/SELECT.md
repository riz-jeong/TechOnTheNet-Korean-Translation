# Oracle / PLSQL : SELECT 문

이 Oracle 튜토리얼에서는 구문, 예제 및 연습 문제를 통해 Oracle **SELECT 문**을 사용하는 방법을 설명합니다.

## 설명
Oracle SELECT 문은 Oracle 데이터베이스의 하나 이상의 테이블에서 레코드를 검색하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 SELECT 문의 구문은 다음과 같습니다.
```SQL
SELECT expressions
FROM tables
[WHERE conditions];
```
### 매개변수 및 인수
#### **expressions**
- 검색하려는 열 또는 계산입니다. 모든 열을 선택하려면 *를 사용합니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어야 합니다.
#### **WHERE conditions**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다. 조건을 제공하지 않으면 모든 레코드가 선택됩니다.

---
## 예제 - 하나의 테이블에서 모든 필드 선택
Oracle SELECT 쿼리를 사용하여 테이블에서 모든 필드를 선택하는 방법을 살펴보겠습니다.
```SQL
SELECT *
FROM homes
WHERE bathrooms >= 2
ORDER BY home_type ASC;
```
이 Oracle SELECT 문 예제에서는 *를 사용하여 homes 테이블에서 욕실 수가 2보다 크거나 같은 모든 필드를 선택하고자 함을 나타냅니다. 결과 집합은 home_type별로 오름차순으로 정렬됩니다.

---
## 예제 - 하나의 테이블에서 개별 필드 선택
Oracle SELECT 문을 사용하여 테이블의 모든 필드가 아닌 테이블에서 개별 필드를 선택할 수도 있습니다.
```SQL
SELECT home_id, home_type, bathrooms
FROM homes
WHERE home_id < 500
AND home_type = 'two-storey'
ORDER BY home_type ASC, bathrooms DESC;
```
이 Oracle SELECT 예제는 home_id가 500보다 작고 home_type이 'two-storey'인 homes 테이블에서 home_id, home_type 및 bathrooms 필드만 반환합니다. 결과는 home_type을 오름차순으로 정렬한 다음 욕실을 내림차순으로 정렬합니다.

---
## 예제 - 여러 테이블에서 필드 선택
Oracle SELECT 문을 사용하여 조인을 사용하여 여러 테이블에서 필드를 검색할 수도 있습니다.
```SQL
SELECT homes.home_id, customers.customer_name
FROM customers
INNER JOIN homes
ON customers.customer_id = homes.customer_id
ORDER BY home_id;
```
이 Oracle SELECT 예제는 [두 테이블을 함께 조인](JOINS.md)하여 customers 및 homes 테이블 모두에서 customer_id 값이 일치하는 home_id 및 customer_name 필드를 표시하는 결과 집합을 제공합니다. 결과는 home_id를 기준으로 오름차순으로 정렬됩니다.

---
## 연습 문제 #1
아래 contacts 테이블을 기준으로 contacts 테이블에서 성이 'Smith', contact_id가 1000보다 크거나 같고 contact_id가 2000보다 작은 모든 필드를 선택합니다. (정렬할 필요 없음)
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

### 연습 문제 #1 풀이
다음 Oracle SELECT 문은 employees 테이블에서 이러한 레코드를 선택합니다.
```SQL
SELECT *
FROM contacts
WHERE last_name = 'Smith'
AND contact_id >= 1000
AND contact_id <= 2000;
```
또는 다음과 같이 [BETWEEN 절](BETWEEN.md)을 사용하여 솔루션을 작성할 수도 있습니다.
```SQL
SELECT *
FROM contacts
WHERE last_name = 'Smith'
AND contact_id BETWEEN 1000 AND 2000;
```

---
**[< 이전](README.md) / [다음 : FROM >](FROM.md)**