# Oracle / PLSQL : WHERE 절

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **WHERE 절**을 사용하는 방법을 설명합니다.

## 설명
Oracle WHERE 절은 [SELECT](SELECT.md), [INSERT](INSERT.md), [UPDATE](UPDATE.md), [DELETE](DELETE.md) 문에서 결과를 필터링하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 WHERE 절의 구문은 다음과 같습니다:
```SQL
WHERE conditions;
```
### 매개변수 또는 인수
#### **conditions**
- 레코드를 선택하기 위해 충족해야 하는 조건입니다.

---
## 예제 - 단일 조건 포함
Oracle WHERE 절의 구문을 설명하기는 어렵기 때문에 몇 가지 예를 살펴보겠습니다.
```SQL
SELECT *
FROM customers
WHERE last_name = 'Anderson';
```
이 Oracle WHERE 절 예제에서는 customers 테이블에서 결과를 필터링하기 위해 WHERE 절을 사용했습니다. 위의 SELECT 문은 customers 테이블에서 last_name이 Anderson인 모든 행을 반환합니다. SELECT에 *가 사용되었으므로 customers 테이블의 모든 필드가 결과 집합에 나타납니다.

---
## 예제 - AND 조건 사용
```SQL
SELECT *
FROM suppliers
WHERE state = 'California'
AND supplier_id <= 750;
```
이 Oracle WHERE 절 예제에서는 WHERE 절을 사용하여 여러 조건을 정의합니다. 이 경우 이 SELECT 문은 [AND 조건](AND.md)을 사용하여 California 주에 위치하고 supplier_id가 750 이하인 모든 공급업체를 반환합니다.

---
## 예제 - OR 조건 사용
```SQL
SELECT supplier_id
FROM suppliers
WHERE supplier_name = 'Apple'
OR supplier_name = 'Microsoft'
```
이 Oracle WHERE 절 예제에서는 WHERE 절을 사용하여 여러 조건을 정의하지만 [AND 조건](AND.md)을 사용하는 대신 [OR 조건](OR.md)을 사용합니다. 이 경우 이 SELECT 문은 supplier_name이 Apple 또는 Microsoft인 모든 supplier_id 값을 반환합니다.

---
## 예제 - AND 및 OR 조건 결합
```SQL
SELECT *
FROM suppliers
WHERE (state = 'Florida' AND supplier_name = 'IBM')
OR (supplier_id > 5000);
```
이 Oracle WHERE 절 예제에서는 WHERE 절을 사용하여 여러 조건을 정의하지만, [AND 조건](AND.md)과 [OR 조건](OR.md)을 결합합니다. 이 예제에서는 Florida 주에 거주하고 supplier_name이 IBM인 모든 공급업체와 supplier_id가 5000보다 큰 모든 공급업체가 반환됩니다.

괄호는 AND 및 OR 조건이 평가되는 순서를 결정합니다. 수학 시간에 연산 순서에서 배운 것과 같습니다!

---
## 예제 - 테이블 조인
```SQL
SELECT suppliers.suppler_name, orders.order_id
FROM suppliers
INNER JOIN orders
ON suppliers.supplier_id = orders.supplier_id
WHERE suppliers.state = 'California';
```
이 Oracle WHERE 절 예제에서는 WHERE 절을 사용하여 단일 SELECT 문에서 여러 테이블을 함께 조인합니다. 이 SELECT 문은 supplier_id를 기준으로 공급업체 및 주문 테이블에 일치하는 레코드가 있고 공급업체의 주가 California인 모든 supplier_name 및 order_id 값을 반환합니다.

[Oracle 조인](JOINS.md)에 대해 자세히 알아보십시오.

---
**[< 이전](Comparison_Operators.md) / [다음 : ORDER BY >](ORDER_BY.md)**