# Oracle / PLSQL : BETWEEN 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **BETWEEN 조건**을 사용하는 방법을 설명합니다.

## 설명
Oracle BETWEEN 조건은 [SELECT](SELECT.md), [INSERT](INSERT.md), [UPDATE](UPDATE.md), [DELETE](DELETE.md) 문에서 범위 내의 값을 검색하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 BETWEEN 조건의 구문은 다음과 같습니다.
```SQL
expression BETWEEN value1 AND value2;
```
### 매개변수 및 인수
#### expression(표현식)
- 열 또는 계산입니다.
### value1 and value2
- 표현식이 비교되는 포괄적인 범위를 만드는 두 값입니다.

## 참고
- Oracle BETWEEN 조건은 표현식이 value1 및 value2 범위(포함) 내에 있는 레코드를 반환합니다.

---
## 예제 - 숫자 사용
숫자 값을 사용하는 몇 가지 Oracle BETWEEN 조건 예제를 살펴보겠습니다. 다음 숫자 예제에서는 숫자 범위 내의 값을 검색하기 위해 BETWEEN 조건을 사용합니다.
```SQL
SELECT *
FROM customers
WHERE customer_id BETWEEN 4000 AND 4999;
```
이 Oracle BETWEEN 예제는 customer_id가 4000에서 4999 사이인(포함) customers 테이블의 모든 행을 반환합니다. 이는 다음 SELECT 문과 동일합니다.
```SQL
SELECT *
FROM customers
WHERE customer_id >= 4000
AND customer_id <= 4999;
```

---
## 예제 - 날짜 포함
날짜에 Oracle BETWEEN 조건을 사용하는 방법을 살펴보겠습니다. 다음 날짜 예제에서는 날짜 범위 내의 값을 검색하기 위해 BETWEEN 조건을 사용합니다.
```SQL
SELECT *
FROM order_details
WHERE order_date BETWEEN TO_DATE ('2014/02/01', 'yyyy/mm/dd')
AND TO_DATE ('2014/02/28', 'yyyy/mm/dd');
```
이 Oracle BETWEEN 조건 예제는 order_date가 2014년 2월 1일에서 2014년 2월 28일 사이인(포함) order_details 테이블의 모든 레코드를 반환합니다. 이는 다음 SELECT 문과 동일합니다.
```SQL
SELECT *
FROM order_details
WHERE order_date >= TO_DATE('2014/02/01', 'yyyy/mm/dd')
AND order_date <= TO_DATE('2014/02/28','yyyy/mm/dd');
```

---
## 예제 - NOT 연산자 사용
Oracle BETWEEN 조건은 Oracle NOT 연산자와 결합할 수도 있습니다. 다음은 BETWEEN 조건과 NOT 연산자를 결합하는 방법의 예제입니다.
```SQL
SELECT *
FROM customers
WHERE customer_id NOT BETWEEN 3000 AND 3500;
```
이 Oracle BETWEEN 예제는 customer_id가 3000에서 3500 사이가 아닌 customers 테이블의 모든 행을 반환합니다. 이는 다음 SELECT 문과 동일합니다.
```SQL
SELECT *
FROM customers
WHERE customer_id < 3000
OR customer_id > 3500;
```

---
**[< 이전](JOINS.md) / [다음 : INSERT >](INSERT.md)**