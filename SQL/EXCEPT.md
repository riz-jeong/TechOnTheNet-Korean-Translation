# SQL : EXCEPT 연산자

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **EXCEPT 연산자**를 사용하는 방법을 설명합니다.

## 설명
SQL EXCEPT 연산자는 첫 번째 SELECT 문에서 두 번째 SELECT 문에서 반환되지 않는 모든 행을 반환하는 데 사용됩니다. 각 SELECT 문은 데이터셋을 정의합니다. EXCEPT 연산자는 첫 번째 데이터셋에서 모든 레코드를 검색한 다음 두 번째 데이터셋의 모든 레코드를 결과에서 제거합니다.

### 차집합(Except Query)

![EXCEPT](Visual-Illustration/minus.png)

**설명** : EXCEPT 쿼리는 파란색 영역에 있는 레코드를 반환합니다. 이는 Dataset1에 존재하지만 Dataset2에는 없는 레코드입니다.

EXCEPT 쿼리 내의 각 SELECT 문은 결과 집합에 유사한 데이터 유형을 가진 동일한 수의 필드가 있어야 합니다.
>팁: EXCEPT 연산자는 모든 SQL 데이터베이스에서 지원되는 것은 아닙니다. SQL Server, PostgreSQL 및 SQLite와 같은 데이터베이스에서 사용할 수 있습니다.
>
>Oracle과 같은 데이터베이스의 경우 [MINUS 연산자](MINUS.md)를 사용하여 이 유형의 쿼리를 수행합니다.

## 구문
SQL에서 EXCEPT 연산자의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
EXCEPT
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```
### 매개변수 및 인수
#### **expression1, expression2, expression_n**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하려면 반드시 충족해야 하는 조건입니다.

## 참고
- 두 SELECT 문에는 동일한 수의 표현식이 있어야 합니다.
- 해당 표현식은 SELECT 문에서 동일한 데이터 유형을 가져야 합니다.  
예시: expression1은 첫 번째 및 두 번째 SELECT 문 모두에서 동일한 데이터 유형이어야 합니다.

---
## 예시 - 단일 표현식 사용
동일한 데이터 유형을 가진 하나의 필드를 반환하는 SQL에서 EXCEPT 연산자를 사용하는 방법에 대한 예를 살펴보겠습니다.

예를 들어
```SQL
SELECT product_id
FROM products
EXCEPT
SELECT product_id
FROM inventory;
```
이 EXCEPT 연산자 예제는 products 테이블에는 있지만 inventory 테이블에는 없는 모든 product_id 값을 반환합니다. 즉, products 테이블에도 있고 inventory 테이블에도 있는 product_id 값이 있는 경우 해당 product_id 값은 EXCEPT 쿼리 결과에 나타나지 않습니다.

---
## 예시 - 여러 표현식 사용
다음으로 SQL에서 둘 이상의 열을 반환하는 EXCEPT 쿼리를 사용하는 방법에 대한 예를 살펴보겠습니다.

예를 들어
```SQL
SELECT contact_id, last_name, first_name
FROM contacts
WHERE last_name = 'Johnson'
EXCEPT
SELECT customer_id, last_name, first_name
FROM customers
WHERE customer_id > 45;
```
이 EXCEPT 예제에서 쿼리는 contacts 테이블의 contacts_id, last_name, first_name 값이 customers 테이블의 customer_id, last_name, first_name 값과 일치하지 않는 contacts 테이블의 레코드를 반환합니다.

---
## 예시 - ORDER BY 절 사용
마지막으로 SQL의 EXCEPT 쿼리에서 [ORDER BY 절](ORDER_BY.md)을 사용하는 방법을 살펴보겠습니다.

예를 들어
```SQL
SELECT supplier_id, supplier_name
FROM suppliers
WHERE supplier_id < 30
EXCEPT
SELECT company_id, company_name
FROM companies
WHERE state = 'Florida'
ORDER BY 2;
```
이 EXCEPT 예제에서는 두 SELECT 문 간에 열 이름이 다르기 때문에 결과 집합에서 열의 위치에 따라 ORDER BY 절에서 열을 참조하는 것이 더 유리합니다. 이 예제에서는 **ORDER BY 2**로 표시된 대로 supplier_name / company_name별로 결과를 오름차순으로 정렬했습니다.

supplier_name / company_name 필드는 결과 집합에서 2번 위치에 있습니다.

---
**[< 이전](MINUS.md) / [다음 : Data Types >](Data_Types.md)**