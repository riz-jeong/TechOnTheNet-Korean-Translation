# Oracle / PLSQL : AND 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **AND 조건**을 사용하는 방법을 설명합니다.

## 설명
Oracle AND 조건(AND 연산자라고도 함)은 SELECT, INSERT, UPDATE 또는 DELETE 문에서 두 개 이상의 조건을 테스트하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 AND 조건의 구문은 다음과 같습니다.
```SQL
WHERE condition1
AND condition2
...
AND condition_n;
```
### 매개변수 및 인수
#### condition1, condition2, ... condition_n
- 레코드를 선택하기 위해 충족해야 하는 모든 조건입니다.

## 참고
- Oracle AND 조건을 사용하면 2개 이상의 조건을 테스트할 수 있습니다.
- Oracle AND 조건은 레코드가 결과 집합에 포함되려면 모든 조건(예: condition1, condition2, condition_n)을 충족해야 합니다.

---
## 예제 - SELECT 문 사용
첫 번째 Oracle AND 조건 쿼리에는 두 개의 조건이 있는 [SELECT 문](SELECT.md)이 포함됩니다.
```SQL
SELECT *
FROM customers
WHERE state = 'Florida'
AND customer_id > 5000;
```
이 Oracle AND 예제는 Florida 주에 거주하고 customer_id가 5000을 초과하는 모든 고객을 반환합니다. SELECT 문에 *가 사용되었으므로, customers 테이블의 모든 필드가 결과 집합에 나타납니다.

---
## 예제 - 테이블 조인
다음 Oracle AND 예제에서는 AND 조건을 사용하여 SELECT 문에서 여러 테이블을 조인하는 방법을 보여 줍니다.
```SQL
SELECT orders.order_id, suppliers.supplier_name
FROM suppliers, orders
WHERE suppliers.supplier_id = orders.supplier_id
AND suppliers.supplier_name = 'Microsoft';
```
위의 SQL은 정상적으로 작동하지만, 더 일반적으로는 적절한 [INNER JOIN](JOINS.md)을 사용하여 다음과 같이 작성합니다.
```SQL
SELECT orders.order_id, suppliers.supplier_name
FROM suppliers
INNER JOIN orders
ON suppliers.supplier_id = orders.supplier_id
WHERE suppliers.supplier_name = 'Microsoft';
```
이 Oracle AND 조건 예제는 supplier_name이 Microsoft인 모든 행을 반환합니다. 그리고 suppliers 및 orders 테이블은 supplier_id를 기준으로 조인됩니다. 모든 필드 앞에 테이블 이름(예: orders.order_id)이 접두사로 붙어 있는 것을 알 수 있습니다. 이는 suppliers 테이블과 orders 테이블 모두에 동일한 필드 이름이 존재할 수 있으므로 어떤 필드를 참조하고 있는지 모호하지 않도록 하기 위해 필요합니다.

이 경우 결과 집합은 SELECT 문의 첫 번째 부분에 나열된 대로 order_id 및 supplier_name 필드만 표시합니다.

---
## 예제 - INSERT 문 사용
다음 Oracle AND 예제에서는 [INSERT 문](INSERT.md)에서 AND 조건을 사용하는 방법을 보여 줍니다.
```SQL
INSERT INTO suppliers
(supplier_id, supplier_name)
SELECT customer_id, customer_name
FROM customers
WHERE customer_name = 'Microsoft'
AND customer_id <= 1000;
```
이 Oracle AND 조건 예제는 customers 테이블에서 customer_name이 Microsoft이고 customer_id가 1000보다 작거나 같은 모든 customer_id 및 customer_name 레코드를 suppliers 테이블에 삽입합니다.

---
## 예제 - UPDATE 문 포함
이 Oracle AND 조건 예제에서는 [UPDATE 문](UPDATE.md)에서 AND 조건을 사용하는 방법을 보여 줍니다.
```SQL
UPDATE suppliers
SET supplier_name = 'Apple'
WHERE supplier_name = 'RIM'
AND offices = 8;
```
이 Oracle AND 조건 예제는 suppliers 테이블의 supplier_name이 RIM이고 offices가 8개인 모든 supplier_name 값을 Apple로 업데이트합니다.

---
## 예제 - DELETE 문 사용
마지막으로, 이 마지막 Oracle AND 예제는 [DELETE 문](DELETE.md)에서 AND 조건을 어떻게 사용할 수 있는지 보여줍니다.
```SQL
DELETE FROM suppliers
WHERE supplier_name = 'Apple'
AND product = 'iPod';
```
이 Oracle AND 조건 예제는 suppliers 테이블에서 supplier_name이 Apple이고 product가 iPod인 모든 레코드를 삭제합니다.

Oracle의 [테이블 조인](JOINS.md)에 대해 자세히 알아보세요.

---
**[< 이전](ORDER_BY.md) / [다음 : OR >](OR.md)**