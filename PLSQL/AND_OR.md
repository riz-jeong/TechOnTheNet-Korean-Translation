# Oracle / PLSQL : AND 및 OR 조건 결합하기

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle 쿼리에서 **AND 조건**과 **OR 조건**을 함께 사용하는 방법을 설명합니다.

## 설명
Oracle [AND 조건](AND.md)과 [OR 조건](OR.md)은 [SELECT](SELECT.md), [INSERT](INSERT.md), [UPDATE](UPDATE.md), [DELETE](DELETE.md) 문에서 결합할 수 있습니다.

이러한 조건을 결합할 때는 괄호를 사용하여 데이터베이스가 각 조건을 평가할 순서를 알 수 있도록 하는 것이 중요합니다. (마치 수학 시간에 연산 순서를 배울 때와 같습니다!)

## 구문
Oracle/PLSQL에서 **AND 조건**과 **OR 조건**을 함께 사용하는 구문은 다음과 같습니다.
```SQL
WHERE condition1
AND condition2
...
OR condition_n;
```
### 매개변수 및 인수
#### **condition1, condition2, ... condition_n**
- 레코드 선택 여부를 결정하기 위해 평가되는 조건입니다.

## 참고
- Oracle AND 및 OR 조건을 사용하면 여러 조건을 테스트할 수 있습니다.
- 괄호 안의 연산 순서를 잊지 마세요!

---
## 예제 - SELECT 문 사용
[SELECT 문](SELECT.md)에서 AND 및 OR 조건을 결합하는 예제를 살펴보겠습니다.
```SQL
SELECT *
FROM suppliers
WHERE (state = 'California' AND supplier_name = 'IBM')
OR (supplier_id < 5000);
```
이 AND & OR 예제는 state가 California이고 supplier_name이 IBM인 모든 공급업체와 supplier_id가 5000 미만인 모든 공급업체를 반환합니다. 괄호는 AND 및 OR 조건이 평가되는 순서를 결정합니다. 수학 시간에 배운 연산 순서와 같습니다!

다음 예제에서는 좀 더 복잡한 문을 살펴보겠습니다.
```SQL
SELECT supplier_id
FROM suppliers
WHERE (supplier_name = 'IBM')
OR (supplier_name = 'Apple' AND state = 'Florida')
OR (supplier_name = 'Best Buy' AND status = 'Active' AND state = 'California');
```
이 AND & OR 예제는 supplier_name이 IBM이거나 supplier_name이 Apple이고 state가 Florida이거나 supplier_name이 Best Buy이고 status가 Active이고 state가 California인 모든 supplier_id 값을 반환합니다.

---
## 예제 - INSERT 문 사용
다음 AND & OR 예제에서는 [INSERT 문](INSERT.md)에서 AND 조건과 OR 조건을 결합하는 방법을 보여 줍니다.
```SQL
INSERT INTO suppliers
(supplier_id, supplier_name)
SELECT account_no, customer_name
FROM customers
WHERE (customer_name = 'Apple' OR customer_name = 'Samsung')
AND customer_id > 20;
```
이 Oracle AND 및 OR 예제는 customers 테이블에서 customer_name이 Apple 또는 Samsung이고 customer_id가 20보다 큰 모든 account_no 및 customer_name 레코드를 suppliers 테이블에 삽입합니다.

---
## 예제 - UPDATE 문 사용
이 AND & OR 예제는 [UPDATE 문](UPDATE.md)에서 AND 및 OR 조건을 사용하는 방법을 보여줍니다.
```SQL
UPDATE suppliers
SET supplier_name = 'Samsung'
WHERE supplier_name = 'RIM'
AND (state = 'California' OR state = 'Florida');
```
이 Oracle AND & OR 조건 예제는 suppliers 테이블의 supplier_name이 RIM이고 state가 California 또는 Florida인 모든 supplier_name 값을 Samsung으로 업데이트합니다.

---
## 예제 - DELETE 문 사용
마지막으로, 이 마지막 AND & OR 예제에서는 [DELETE 문](DELETE.md)에서 AND 및 OR 조건을 사용하는 방법을 보여 줍니다.
```SQL
DELETE FROM suppliers
WHERE state = 'Florida'
AND (product = 'PC computers' OR supplier_name = 'Dell');
```
이 Oracle AND 및 OR 조건 예제는 suppliers 테이블에서 state가 Florida이고 product가 PC computers이거나 supplier_name이 Dell인 모든 레코드를 삭제합니다.

---
**[< 이전](OR.md) / [다음 : DISTINCT >](DISTINCT.md)**