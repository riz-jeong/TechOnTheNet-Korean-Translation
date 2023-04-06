# Oracle / PLSQL : 비교 연산자

이 Oracle 튜토리얼에서는 Oracle에서 같음과 같지 않음을 테스트하는 데 사용되는 모든 비교 연산자와 고급 연산자를 살펴봅니다.

## 설명
비교 연산자는 WHERE 절에서 선택해야 할 레코드를 결정하는 데 사용됩니다.  
다음은 Oracle/PLSQL에서 사용할 수 있는 비교 연산자 목록입니다.

| 비교 연산자 | 설명                                            |
| :---------- | :---------------------------------------------- |
| =           | 같음                                            |
| <>          | 같지 않음                                       |
| !=          | 같지 않음                                       |
| >           | 보다 큼                                         |
| >=          | 크거나 같음                                     |
| <           | 보다 작음                                       |
| <=          | 작거나 같음                                     |
| IN ( )      | 리스트의 값과 일치                              |
| NOT         | 부정 연산                                       |
| BETWEEN     | 범위 내(포함)                                   |
| IS NULL     | NULL 값                                         |
| IS NOT NULL | Non-NULL 값                                     |
| LIKE        | %와 _를 사용하여 패턴 일치                      |
| REGEXP_LIKE | 정규식을 사용하여 패턴 일치                     |
| EXISTS      | 하위 쿼리가 하나 이상의 행을 반환하면 조건 충족 |

이러한 연산자 중 일부는 매우 간단하지만 다른 연산자는 더 복잡합니다. 먼저 Oracle의 더 쉬운 비교 연산자부터 살펴보겠습니다.

---
## 예제 - 동등 연산자
Oracle/PLSQL에서는 `=` 연산자를 사용하여 쿼리에서 동일성 여부를 테스트할 수 있습니다.
```SQL
SELECT *
FROM customers
WHERE last_name = 'Anderson';
```
이 예제에서 위의 SELECT 문은 customers 테이블에서 last_name이 Anderson과 같은 모든 행을 반환합니다.

---
## 예제 - 부등 연산자
Oracle/PLSQL에서는 `<>` 또는 `!=` 연산자를 사용하여 쿼리에서 불평등 여부를 테스트할 수 있습니다.

예를 들어 다음과 같이 `<>` 연산자를 사용하여 불평등 여부를 테스트할 수 있습니다.
```SQL
SELECT *
FROM customers
WHERE last_name <> 'Anderson';
```
이 예제에서 SELECT 문은 customers 테이블에서 last_name이 Anderson과 같지 않은 모든 행을 반환합니다.

또는 다음과 같이 `!=` 연산자를 사용하여 이 쿼리를 작성할 수도 있습니다.
```SQL
SELECT *
FROM customers
WHERE last_name != 'Anderson';
```
이 두 쿼리 모두 동일한 결과를 반환합니다.

---
## 예제 - 보다 큼 연산자
Oracle에서 `>` 연산자를 사용하여 보다 큰 식을 테스트할 수 있습니다.
```SQL
SELECT *
FROM suppliers
WHERE supplier_id > 1000;
```
이 예제에서 SELECT 문은 suppliers 테이블에서 supplier_id가 1000보다 큰 모든 행을 반환합니다. 1000과 같은 supplier_id는 결과 집합에 포함되지 않습니다.

---
## 예제 - 크거나 같음 연산자
Oracle에서는 `>=` 연산자를 사용하여 다음보다 크거나 같은 식을 테스트할 수 있습니다.
```SQL
SELECT *
FROM suppliers
WHERE supplier_id >= 1000;
```
이 예제에서 SELECT 문은 suppliers 테이블에서 supplier_id가 1000보다 크거나 같은 모든 행을 반환합니다. 이 경우 1000과 같은 supplier_id가 결과 집합에 포함됩니다.

---
## 예제 - 보다 작음 연산자
Oracle에서 `<` 연산자를 사용하여 다음보다 작은 식을 테스트할 수 있습니다.
```SQL
SELECT *
FROM employees
WHERE employee_id < 99;
```
이 예제에서 SELECT 문은 employees 테이블에서 employee_id가 99보다 작은 모든 행을 반환합니다. employee_id가 99와 같으면 결과 집합에 포함되지 않습니다.

---
## 예제 - 작거나 같음 연산자
Oracle에서는 `<=` 연산자를 사용하여 다음보다 작거나 같은 식을 테스트할 수 있습니다.
```SQL
SELECT *
FROM employees
WHERE employee_id <= 99;
```
이 예제에서 SELECT 문은 employees 테이블에서 employee_id가 99보다 작거나 같은 모든 행을 반환합니다. 이 경우 99와 같은 n개의 employee_id가 결과 집합에 포함됩니다.

---
## 예제 - 고급 연산자
고급 비교 연산자를 위해 각 연산자를 개별적으로 설명하는 특정 튜토리얼을 작성했습니다. 이러한 주제는 나중에 다루거나 지금 바로 튜토리얼 중 하나로 이동할 수 있습니다.

- [IN ( )](IN.md)
- [NOT](NOT.md)
- [BETWEEN](BETWEEN.md)
- [IS NULL](IS_NULL.md)
- [IS NOT NULL](IS_NOT_NULL.md)
- [LIKE](LIKE.md)
- [REGEXP_LIKE](REGEXP_LIKE.md)
- [EXISTS](EXISTS.md)

---
**[< 이전](FROM.md) / [다음 : WHERE >](WHERE.md)**
