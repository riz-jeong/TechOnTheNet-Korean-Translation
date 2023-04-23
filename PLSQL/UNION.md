# Oracle / PLSQL : UNION 연산자

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **UNION 연산자**를 사용하는 방법을 설명합니다.

## 설명
Oracle UNION 연산자는 2개 이상의 Oracle [SELECT 문](SELECT.md)의 결과 집합을 결합하는 데 사용됩니다. 이 연산자는 다양한 SELECT 문 간의 중복 행을 제거합니다.

UNION 연산자 내의 각 [SELECT 문](SELECT.md)은 결과 집합에 데이터 유형이 유사한 동일한 수의 필드가 있어야 합니다.

## 구문
Oracle/PLSQL에서 UNION 연산자의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```
### 매개변수 및 인수
#### **expression1, expression2, expression_n**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 하나 이상의 테이블이 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.

## 참고
- 두 SELECT 문에는 동일한 수의 표현식이 있어야 합니다.

---
## 예제 - 단일 필드 반환
다음은 여러 SELECT 문에서 하나의 필드를 반환하는 Oracle UNION 연산자의 예제입니다. (두 필드의 데이터 유형이 모두 동일함)
```SQL
SELECT supplier_id
FROM suppliers
UNION
SELECT supplier_id
FROM order_details;
```
이 Oracle UNION 연산자 예제에서 공급업체 및 주문 세부 정보 테이블에 모두 supplier_id가 나타나면 결과 집합에 한 번 나타납니다. Oracle UNION 연산자는 중복을 제거합니다. 중복을 제거하지 않으려면 Oracle [UNION ALL 연산자](UNION_ALL.md)를 사용해 보십시오.

---
## 예제 - ORDER BY 사용
Oracle UNION 연산자는 [ORDER BY 절](ORDER_BY.md)을 사용하여 쿼리 결과의 순서를 지정할 수 있습니다.
```SQL
SELECT supplier_id, supplier_name
FROM suppliers
WHERE supplier_id <= 500
UNION
SELECT company_id, company_name
FROM companies
WHERE company_name = 'Apple'
ORDER BY 2;
```
이 Oracle UNION 연산자에서는 두 [SELECT 문](SELECT.md) 간에 열 이름이 다르기 때문에 결과 집합에서 열의 위치에 따라 [ORDER BY 절](ORDER_BY.md)의 열을 참조하는 것이 더 유리합니다. 이 예제에서는 `ORDER BY 2`로 표시된 대로 supplier_name / company_name별로 결과를 오름차순으로 정렬했습니다.

supplier_name / company_name 필드는 결과 집합에서 2번 위치에 있습니다.

---
## 자주 묻는 질문
- 질문 : 두 날짜를 비교하고 날짜 값을 기반으로 필드의 개수를 반환해야 합니다. 예를 들어 테이블에 last_updated_date라는 날짜 필드가 있습니다. trunc(last_updated_date >= trunc(sysdate - 13))인지 확인해야 합니다.

- 답변 : 집계 함수인 Oracle [COUNT 함수](COUNT.md)를 사용하고 있으므로 Oracle UNION 연산자를 사용하는 것이 좋습니다. 예를 들어 다음을 시도해 볼 수 있습니다.
```SQL
SELECT a.code AS Code, a.name AS Name, COUNT(b.Ncode)
FROM cdmaster a, nmmaster b
WHERE a.code = b.code
AND a.status = 1
AND b.status = 1
AND b.Ncode <> 'a10'
AND TRUNC(a.last_updated_date) <= TRUNC(sysdate - 13)
GROUP BY a.code, a.name
UNION
SELECT a.code AS Code, a.name AS Name, COUNT(b.Ncode)
FROM cdmaster a, nmmaster b
WHERE a.code = b.code
AND a.status = 1
AND b.status = 1
AND b.Ncode <> 'a10'
AND TRUNC(a.last_updated_date) > TRUNC(sysdate - 13)
GROUP BY a.code, a.name;
```
Oracle UNION 연산자를 사용하면 하나의 기준 집합을 기반으로 카운트를 수행할 수 있습니다.
```SQL
TRUNC(a.last_updated_date) <= TRUNC(sysdate - 13)
```
또한 다른 기준 집합을 기반으로 카운트를 수행합니다.
```SQL
TRUNC(a.last_updated_date) > TRUNC(sysdate - 13)
```

---
**[< 이전](HAVING.md) / [다음 : UNION ALL >](UNION_ALL.md)**