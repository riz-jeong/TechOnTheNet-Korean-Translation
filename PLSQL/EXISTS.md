# Oracle / PLSQL : EXISTS 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **EXISTS 조건**을 사용하는 방법을 설명합니다.

Oracle EXISTS 조건은 하위 쿼리와 함께 사용되며 하위 쿼리가 하나 이상의 행을 반환하면 "조건이 충족된 것"으로 간주됩니다. 이 조건은 [SELECT](SELECT.md), [INSERT](INSERT.md), [UPDATE](UPDATE.md), [DELETE](DELETE.md) 문에서 사용할 수 있습니다.

## 구문
Oracle/PLSQL에서 EXISTS 조건의 구문은 다음과 같습니다.
```SQL
WHERE EXISTS ( subquery );
```
### 매개변수 및 인수
#### **subquery**
- 하위 쿼리는 SELECT 문입니다. 하위 쿼리가 결과 집합에서 하나 이상의 레코드를 반환하는 경우 EXISTS 절이 true로 평가되고 EXISTS 조건이 충족됩니다. 하위 쿼리가 레코드를 반환하지 않으면 EXISTS 절이 false로 평가되고 EXISTS 조건이 충족되지 않습니다.

## 참고
- Oracle EXISTS 조건을 사용하는 Oracle SQL 문은 하위 쿼리가 외부 쿼리 테이블의 모든 행에 대해 다시 실행되므로 매우 비효율적입니다. 대부분의 쿼리를 작성하는 더 효율적인 방법에는 EXISTS 조건을 사용하지 않는 방법이 있습니다.

---
## 예제 - SELECT 문 사용
간단한 예제를 살펴보겠습니다.

다음은 EXISTS 조건을 사용하는 [SELECT 문](SELECT.md)입니다.
```SQL
SELECT *
FROM customers
WHERE EXISTS (SELECT *
              FROM order_details
              WHERE customers.customer_id = order_details.customer_id);
```
이 Oracle EXISTS 조건 예제는 order_details 테이블에 customer_id가 일치하는 레코드가 하나 이상 있는 customers 테이블의 모든 레코드를 반환합니다.

---
## 예제 - NOT EXISTS를 사용하는 SELECT 문 사용
Oracle EXISTS 조건은 NOT 연산자와 결합할 수도 있습니다.
```SQL
SELECT *
FROM customers
WHERE NOT EXISTS (SELECT *
                  FROM order_details
                  WHERE customers.customer_id = order_details.customer_id);
```
이 Oracle EXISTS 예제는 주어진 customer_id에 대한 order_details 테이블에 레코드가 없는 경우 customers 테이블의 모든 레코드를 반환합니다.

---
## 예제 - INSERT 문 사용
다음은 EXISTS 조건을 사용하는 [INSERT 문](INSERT.md)의 예제입니다.
```SQL
INSERT INTO contacts
(contact_id, contact_name)
SELECT supplier_id, supplier_name
FROM suppliers
WHERE EXISTS (SELECT *
              FROM order_details
              WHERE suppliers.supplier_id = order_details.supplier_id);
```

---
## 예제 - UPDATE 문 사용
다음은 EXISTS 조건을 사용하는 [UPDATE 문](UPDATE.md)의 예입니다.
```SQL
UPDATE suppliers
SET supplier_name = (SELECT customers.name
                     FROM customers
                     WHERE customers.customer_id = suppliers.supplier_id)
WHERE EXISTS (SELECT customers.name
              FROM customers
              WHERE customers.customer_id = suppliers.supplier_id);
```

---
## 예제 - DELETE 문 사용
다음은 EXISTS 조건을 사용하는 [DELETE 문](DELETE.md)의 예제입니다.
```SQL
DELETE FROM suppliers
WHERE EXISTS (SELECT *
              FROM order_details
              WHERE suppliers.supplier_id = order_details.supplier_id);
```

---
**[< 이전](TRUNCATE.md) / [다음 : GROUP BY >](GROUP_BY.md)**