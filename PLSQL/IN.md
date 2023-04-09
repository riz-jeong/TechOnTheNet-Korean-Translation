# Oracle / PLSQL : IN 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **IN 조건**을 사용하는 방법을 설명합니다.

## 설명
Oracle IN 조건은 SELECT, INSERT, UPDATE, DELETE 문에서 여러 [OR 조건](OR.md)을 사용할 필요성을 줄이는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 IN 조건의 구문은 다음과 같습니다.
```SQL
expression IN (value1, value2, ... value_n);
```
OR
```SQL
expression IN (subquery);
```
### 매개변수 또는 인수
#### **expression(표현식)**
- 테스트할 값입니다.
#### **value1, value2 ..., value_n**
- 표현식에 대해 테스트할 값입니다.
#### **subquery(하위 쿼리)**
- 결과 집합이 표현식에 대해 테스트되는 [SELECT 문](SELECT.md)입니다. 이러한 값 중 표현식과 일치하는 값이 하나라도 있으면 IN 조건은 참으로 평가됩니다.

## 참고
- Oracle IN 조건은 표현식이 value1, value2..., value_n인 레코드를 반환합니다.
- Oracle IN 조건은 Oracle IN 연산자라고도 합니다.

---
## 예제 - 문자 포함
문자 값을 사용하는 Oracle IN 조건 예제를 살펴보겠습니다.

다음은 IN 조건을 사용하여 문자 값을 비교하는 Oracle SELECT 문입니다.
```SQL
SELECT *
FROM customers
WHERE customer_name IN ('IBM', 'Hewlett Packard', 'Microsoft');
```
이 Oracle IN 조건 예제는 customer_name이 IBM, Hewlett Packard, Microsoft인 모든 행을 반환합니다. SELECT에 *가 사용되었으므로, customers 테이블의 모든 필드가 결과 집합에 나타납니다.

위의 IN 예제는 다음 SELECT 문과 동일합니다.
```SQL
SELECT *
FROM customers
WHERE customer_name = 'IBM'
OR customer_name = 'Hewlett Packard'
OR customer_name = 'Microsoft'
```
보시다시피, Oracle IN 조건을 사용하면 더 읽기 쉽고 효율적으로 만들 수 있습니다.

---
## 예제 - 숫자 사용
다음으로 숫자 값을 사용하는 Oracle IN 조건 예제를 살펴보겠습니다.
```SQL
SELECT *
FROM orders
WHERE order_id IN (10000, 10001, 10003, 10005);
```
이 Oracle IN 조건 예제는 order_id가 10000, 10001, 10003, 10005인 모든 주문을 반환합니다.

위의 IN 예제는 다음 SELECT 문과 동일합니다.
```SQL
SELECT *
FROM orders
WHERE order_id = 10000
OR order_id = 10001
OR order_id = 10003
OR order_id = 10005;
```

---
## 예제 - NOT 연산자 사용
마지막으로 Oracle NOT 연산자를 사용하는 IN 조건 예제를 살펴보겠습니다.
```SQL
SELECT *
FROM customers
WHERE customer_name NOT IN ('IBM', 'Hewlett Packard', 'Microsoft');
``` 
이 Oracle IN 조건 예제는 customer_name이 IBM, Hewlett Packard, Microsoft가 아닌 모든 행을 반환합니다. 때로는 원하는 값과 반대로 원하지 않는 값을 나열하는 것이 더 효율적일 수 있습니다.

---
**[< 이전](DISTINCT.md) / [다음 : IS NULL >](IS_NULL.md)**