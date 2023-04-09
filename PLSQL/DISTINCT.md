# Oracle / PLSQL : DISTINCT 절

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **DISTINCT 절**을 사용하는 방법을 설명합니다.

## 설명
Oracle DISTINCT 절은 결과 집합에서 중복을 제거하는 데 사용됩니다. DISTINCT 절은 [SELECT 문](SELECT.md)과 함께만 사용할 수 있습니다.

## 구문
Oracle/PLSQL에서 DISTINCT 절의 구문은 다음과 같습니다.
```SQL
SELECT DISTINCT expressions
FROM tables
[WHERE conditions];
```
### 매개 변수 및 인수
#### **expressions(표현식)**
검색하려는 열 또는 계산입니다.
#### **tables**
레코드를 검색하려는 테이블입니다. FROM 절에 하나 이상의 테이블이 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.

## 참고
- DISTINCT 절에 하나의 표현식만 제공된 경우 쿼리는 해당 표현식에 대한 고유 값을 반환합니다.
- DISTINCT 절에 둘 이상의 표현식이 제공된 경우 쿼리는 나열된 표현식에 대한 고유한 조합을 검색합니다.
- Oracle에서 DISTINCT 절은 NULL 값을 무시하지 않습니다. 따라서 SQL 문에서 DISTINCT 절을 사용하면 결과 집합에 NULL이 고유 값으로 포함됩니다.

---
## 예제 - 단일 표현식 사용
가장 간단한 Oracle DISTINCT 절 예제를 살펴보겠습니다. Oracle DISTINCT 절을 사용하여 결과 집합에서 중복을 제거하는 단일 필드를 반환할 수 있습니다.
```SQL
SELECT DISTINCT state
FROM customers
WHERE last_name = 'Smith';
```
이 Oracle DISTINCT 예제는 고객의 last_name이 'Smith'인 customers 테이블에서 모든 고유 상태 값을 반환합니다.

---
## 예제 - 여러 표현식 사용
Oracle DISTINCT 절을 사용하여 SELECT 문에서 둘 이상의 필드에서 중복을 제거하는 방법을 살펴보겠습니다.
```SQL
SELECT DISTINCT city, state
FROM customers
WHERE total_orders > 10
ORDER BY city;
```
이 Oracle DISTINCT 절 예제에서는 customers 테이블에서 total_orders가 10보다 큰 각각의 고유한 city 및 state 조합을 반환합니다. 결과는 city별로 오름차순으로 정렬됩니다.

이 경우 DISTINCT 키워드 뒤에 나열된 각 필드에 DISTINCT가 적용되므로 고유한 조합을 반환합니다.

---
**[< 이전](AND_OR.md) / [다음 : IN >](IN.md)**