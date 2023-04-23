# Oracle / PLSQL: UNION ALL 연산자

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **UNION ALL 연산자**를 사용하는 방법을 설명합니다.

## 설명
Oracle UNION ALL 연산자는 2개 이상의 [SELECT 문](SELECT.md)의 결과 집합을 결합하는 데 사용됩니다. 이 연산자는 쿼리에서 모든 행을 반환하며 여러 SELECT 문 간에 중복되는 행을 제거하지 않습니다.

Oracle UNION ALL 연산자 내의 각 [SELECT 문](SELECT.md)은 결과 집합에 데이터 유형이 유사한 동일한 수의 필드가 있어야 합니다.

## 구문
Oracle/PLSQL에서 UNION ALL 연산자의 구문은 다음과 같습니다.
```sql
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION ALL
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.

## 참고
- 두 SELECT 문에는 동일한 수의 표현식이 있어야 합니다.

---
## 예제 - 단일 필드 반환
다음은 여러 SELECT 문에서 하나의 필드를 반환하는 Oracle UNION ALL 연산자의 예제입니다. (두 필드 모두 데이터 유형이 동일함)
```sql
SELECT supplier_id
FROM suppliers
UNION ALL
SELECT supplier_id
FROM orders;
```
suppliers 및 orders 테이블에 모두 supplier_id가 표시되는 경우 이 Oracle UNION ALL 연산자는 결과 집합에서 supplier_id를 여러 번 반환합니다. Oracle UNION ALL 연산자는 중복을 제거하지 않습니다. 중복을 제거하려면 Oracle [UNION 연산자](UNION.md)를 사용해보십시오.

---
## 예제 - ORDER BY 사용
Oracle UNION ALL 연산자는 Oracle [ORDER BY 절](ORDER_BY.md)을 사용하여 쿼리 결과의 순서를 지정할 수 있습니다.
```sql
SELECT supplier_id, supplier_name
FROM suppliers
WHERE state = 'California'
UNION ALL
SELECT company_id, company_name
FROM companies
WHERE company_id > 1000
ORDER BY 2;
```
이 Oracle UNION ALL 연산자에서는 두 [SELECT 문](SELECT.md) 간에 열 이름이 다르기 때문에 결과 집합에서 열의 위치에 따라 [ORDER BY 절](ORDER_BY.md)의 열을 참조하는 것이 더 유리합니다. 이 예제에서는 ORDER BY 2로 표시된 대로 supplier_name / company_name별로 결과를 오름차순으로 정렬했습니다.

supplier_name / company_name 필드는 결과 집합에서 2번 위치에 있습니다.

---
**[< 이전](UNION.md) / [다음 : INTERSECT >](INTERSECT.md)**