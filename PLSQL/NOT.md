# Oracle / PLSQL: NOT 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle NOT 조건을 사용하는 방법을 설명합니다.

## 설명
Oracle NOT 조건(NOT 연산자라고도 함)은 [SELECT](SELECT.md), [INSERT](INSERT.md), [UPDATE](UPDATE.md), [DELETE](DELETE.md) 문에서 조건을 무효화하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 NOT 조건의 구문은 다음과 같습니다.
```SQL
NOT condition
```
### 매개변수 및 인수
#### **condition**
- 부정할 조건입니다.

## 참고
- Oracle NOT 조건은 레코드가 결과 집합에 포함되려면 조건의 반대 조건이 충족되어야 합니다.

---
## 예제 - IN 조건과 결합
Oracle NOT 조건은 [IN 조건](IN.md)과 결합할 수
```SQL
SELECT *
FROM customers
WHERE customer_name NOT IN ( 'IBM', 'Hewlett Packard', 'Microsoft' );
```
이 Oracle NOT 예제는 customers 테이블에서 customer_name이 IBM, Hewlett Packard 또는 Microsoft가 아닌 모든 행을 반환합니다. 때로는 원하는 값과 반대로 원하지 않는 값을 나열하는 것이 더 효율적일 수 있습니다.

---
## 예제 - IS NULL 조건과 결합
Oracle NOT 조건은 [IS NULL 조건](IS_NULL.md)과 결합할 수도 있습니다.
```SQL
SELECT *
FROM customers
WHERE last_name IS NOT NULL;
```
이 Oracle NOT 예제는 last_name에 NULL 값이 포함되지 않은 customers 테이블의 모든 레코드를 반환합니다.

---
## 예제 - LIKE 조건과 결합
Oracle NOT 조건은 [LIKE 조건](LIKE.md)과 결합할 수도 있습니다.
```SQL
SELECT customer_name
FROM customers
WHERE customer_name NOT LIKE 'S%';
```
LIKE 조건 앞에 Oracle NOT 연산자를 배치하면 customer_name이 'S'로 시작하지 않는 모든 고객을 검색할 수 있습니다.

---
## 예제 - BETWEEN 조건과 결합하기
Oracle NOT 조건은 [BETWEEN 조건](BETWEEN.md)과 결합할 수도 있습니다. 다음은 NOT 연산자를 BETWEEN 조건과 결합하는 방법의 예입니다.
```SQL
SELECT *
FROM customers
WHERE customer_id NOT BETWEEN 4000 AND 4100;
```
이 Oracle NOT 예제는 customer_id가 4000에서 4100 사이가 **아닌** 모든 행을 반환합니다. 이는 다음 Oracle SELECT 문과 동일합니다.
```SQL
SELECT *
FROM customers
WHERE customer_id < 4000
OR customer_id > 4100;
```

---
## 예제 - EXISTS 조건과 결합
Oracle NOT 조건은 [EXISTS 조건](EXISTS.md)과 결합할 수도 있습니다.
```SQL
SELECT *
FROM suppliers
WHERE NOT EXISTS (SELECT * 
                  FROM orders
                  WHERE suppliers.supplier_id = orders.supplier_id);
```
이 Oracle NOT 예제는 주문 테이블에 지정된 supplier_id에 대한 레코드가 없는 경우 suppliers 테이블의 모든 레코드를 반환합니다.

---
**[< 이전](REGEXP_LIKE.md) / [다음 : ALIASES >](ALIASES.md)**