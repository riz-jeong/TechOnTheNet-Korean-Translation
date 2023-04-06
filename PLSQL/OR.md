# Oracle / PLSQL : OR 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **OR 조건**을 사용하는 방법을 설명합니다.

## 설명
Oracle OR 조건은 조건 중 하나라도 충족되면 레코드가 반환되는 여러 조건을 테스트하는 데 사용됩니다. [SELECT](SELECT.md), [INSERT](INSERT.md), [UPDATE](UPDATE.md) 또는 [DELETE](DELETE.md) 문에서 사용할 수 있습니다.

## 구문
Oracle/PLSQL에서 OR 조건의 구문은 다음과 같습니다.
```SQL
WHERE condition
OR condition2
...
OR condition_n;
```
### 매개변수 또는 인수
#### condition1, condition2, condition_n
- 레코드를 선택하기 위해 어떤 조건이든 충족하여야 합니다.

## 참고
- Oracle OR 조건을 사용하면 2개 이상의 조건을 테스트할 수 있습니다.
- Oracle OR 조건은 레코드가 결과 집합에 포함되려면 조건(예: condition1, condition2, condition_n) 중 하나라도 충족되어야 합니다.

---
## 예제 - SELECT 문 사용
첫 번째로 살펴볼 Oracle OR 조건 예제에는 두 개의 조건이 있는 Oracle [SELECT 문](SELECT.md)이 포함됩니다.
```SQL
SELECT *
FROM customers
WHERE state = 'California'
OR available_credit > 500;
```
이 Oracle OR 조건 예제는 California 주에 거주하거나 available_credit이 500보다 큰 모든 고객을 반환합니다. [SELECT 문](SELECT.md)에 *가 사용되었으므로, customers 테이블의 모든 필드가 결과 집합에 나타납니다.

---
## 예제 - SELECT 문 사용(조건 3개)
다음 Oracle OR 예제에서는 3개의 조건이 있는 Oracle [SELECT 문](SELECT.md)을 살펴봅니다. 이러한 조건 중 하나라도 충족되면 레코드가 결과 집합에 포함됩니다.
```SQL
SELECT supplier_id
FROM suppliers
WHERE supplier_name = 'IBM'
OR city = 'New York'
OR offices > 5;
```
이 Oracle OR 조건 예제는 supplier_name이 IBM이거나, city가 New York이거나, offices가 5보다 큰 모든 supplier_id 값을 반환합니다.

---
## 예제 - INSERT 문 사용
Oracle OR 조건은 Oracle [INSERT 문](INSERT.md)에서 사용할 수 있습니다.
```SQL
INSERT INTO suppliers
(supplier_id, supplier_name)
SELECT account_no, name
FROM customers
WHERE city = 'New York'
OR city = 'Newark'
```
이 Oracle OR 예제는 customers 테이블에서 New York 또는 Newark에 있는 모든 account_no 및 name 레코드를 suppliers 테이블에 삽입합니다.

---
## 예제 - UPDATE 문 사용
Oracle OR 조건은 Oracle [UPDATE 문](UPDATE.md)에서 사용할 수 있습니다.
```SQL
UPDATE suppliers
SET supplier_name = 'Apple'
WHERE supplier_name = 'RIM'
OR available_products < 10;
```
이 Oracle OR 조건 예제는 suppliers 테이블의 supplier_name이 RIM이거나 availabe_products가 10 미만인 모든 supplier_name 값을 Apple로 업데이트합니다.

---
## 예제 - DELETE 문 사용
Oracle OR 조건은 Oracle [DELETE 문](DELETE.md)에서 사용할 수 있습니다.
```SQL
DELETE FROM suppliers
WHERE supplier_name = 'HP'
OR employees >= 60;
```
이 Oracle OR 조건의 예는 suppliers 테이블에서 supplier_name이 HP이거나 employees가 60보다 큰 모든 공급업체를 삭제합니다.

---
**[< 이전](AND.md) / [다음 : AND OR >](AND_OR.md)**