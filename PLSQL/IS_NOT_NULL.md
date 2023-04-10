# Oracle / PLSQL: IS NOT NULL 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **IS NOT NULL 조건**을 사용하는 방법을 설명합니다.

## 설명
Oracle IS NOT NULL 조건은 NOT NULL 값을 테스트하는 데 사용됩니다. SQL 문 또는 PLSQL 코드 블록에서 Oracle IS NOT NULL 조건을 사용할 수 있습니다.

## 구문
Oracle/PLSQL에서 IS NOT NULL 조건의 구문은 다음과 같습니다.
```SQL
expression IS NOT NULL
```
### 매개변수 또는 인수
#### expression(표현식)
- null이 아닌 값인지 테스트할 값입니다.

## 참고
- 표현식이 NULL 값이 아닌 경우 조건은 TRUE로 평가됩니다.
- 표현식이 NULL 값인 경우 조건은 FALSE로 평가됩니다.

---
## 예제 - SELECT 문 사용
다음은 [SELECT 문](SELECT.md)에서 Oracle IS NOT NULL 조건을 사용하는 방법에 대한 예제입니다.
```SQL
SELECT *
FROM customers
WHERE customer_name IS NOT NULL;
```
이 Oracle IS NOT NULL 예제는 customers 테이블에서 customer_name에 null 값이 포함되지 않은 모든 레코드를 반환합니다.

---
## 예제 - INSERT 문 사용
다음은 [INSERT 문](INSERT.md)에서 Oracle IS NOT NULL 조건을 사용하는 방법에 대한 예제입니다.
```SQL
INSERT INTO suppliers
(supplier_id, supplier_name)
SELECT account_no, name
FROM customers
WHERE account_no IS NOT NULL;
```
이 Oracle IS NOT NULL 예제는 customers 테이블에서 account_no에 null 값이 포함되지 않은 레코드를 suppliers 테이블에 삽입합니다.

---
## 예제 - UPDATE 문 사용
다음은 [UPDATE 문](UPDATE.md)에서 Oracle IS NOT NULL 조건을 사용하는 방법에 대한 예제입니다.
```SQL
UPDATE customers
SET status = 'Active'
WHERE customer_name IS NOT NULL;
```
이 Oracle IS NOT NULL 예제는 customer_name에 null 값이 포함되지 않은 customers 테이블의 레코드를 업데이트합니다.

---
## 예제 - DELETE 문 사용
다음은 [DELETE 문](DELETE.md)에서 Oracle IS NOT NULL 조건을 사용하는 방법에 대한 예제입니다.
```SQL
DELETE FROM customers
WHERE status IS NOT NULL;
```
이 Oracle IS NOT NULL 예제는 customers 테이블에서 상태에 null 값이 포함되지 않은 모든 레코드를 삭제합니다.

---
## 예제 - PLSQL 코드 사용
PLSQL에서 Oracle IS NOT NULL 조건을 사용하여 값이 null이 아닌지 확인할 수 있습니다.
```SQL
IF Lvalue IS NOT NULL then

   ...

END IF;
```
Lvalue에 null 값이 포함되어 있지 않으면 "IF" 표현식은 TRUE로 평가됩니다.

---
**[< 이전](IS_NULL.md) / [다음 : LIKE >](LIKE.md)**