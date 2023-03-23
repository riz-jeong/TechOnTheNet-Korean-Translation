# SQL : UNION 연산자

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL UNION 연산자를 사용하는 방법을 설명합니다.

## 설명
SQL UNION 연산자는 2개 이상의 SELECT 문의 결과 집합을 결합하는 데 사용됩니다. 이 연산자는 여러 SELECT 문 사이의 중복 행을 제거합니다.

UNION 내의 각 SELECT 문은 결과 집합에 데이터 유형이 유사한 동일한 수의 필드가 있어야 합니다.

## UNION과 UNION ALL의 차이점은 무엇인가요?
- UNION은 중복 행을 제거합니다.
- [UNION ALL](UNION_ALL.md)은 중복 행을 제거하지 않습니다.

## 구문
SQL에서 UNION 연산자의 구문은 다음과 같습니다.
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
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.

## 참고
- 두 SELECT 문에는 동일한 수의 표현식이 있어야 합니다.
- 해당 표현식은 SELECT 문에서 동일한 데이터 유형을 가져야 합니다.  
예시: expression1은 첫 번째 및 두 번째 SELECT 문 모두에서 동일한 데이터 유형이어야 합니다.
- [UNION ALL 연산자](UNION_ALL.md)도 참조하십시오.

---
## 예제 - 이름이 같은 단일 필드
하나의 필드를 반환하는 SQL UNION 연산자를 사용하는 방법을 살펴보겠습니다. 이 간단한 예제에서는 두 SELECT 문에 있는 필드의 이름과 데이터 유형이 동일합니다.

예를 들어
```SQL
SELECT supplier_id
FROM suppliers
UNION
SELECT supplier_id
FROM orders
ORDER BY supplier_id;
```
이 SQL UNION 연산자 예제에서 suppliers 및 orders 테이블에 모두 supplier_id가 나타나면 결과 집합에 한 번 나타납니다. UNION 연산자는 중복을 제거합니다. 중복을 제거하지 않으려면 [UNION ALL 연산자](UNION_ALL.md)를 사용해보십시오.

이제 이 예제에서 일부 데이터를 더 살펴보겠습니다.

suppliers 테이블에 다음과 같은 레코드가 채워져 있다고 가정합니다.

| supplier_id | supplier_name |
| :---------- | :------------ |
| 1000        | Microsoft     |
| 2000        | Oracle        |
| 3000        | Apple         |
| 4000        | Samsung       |

orders 테이블은 다음 레코드로 채워져있습니다.

| order_id | order_date | supplier_id |
| :------- | :--------- | :---------- |
| 1        | 2015-08-01 | 2000        |
| 2        | 2015-08-01 | 6000        |
| 3        | 2015-08-02 | 7000        |
| 4        | 2015-08-03 | 8000        |

그리고 다음 UNION 문을 실행했습니다.
```SQL
SELECT supplier_id
FROM suppliers
UNION
SELECT supplier_id
FROM orders
ORDER BY supplier_id;
```
다음과 같은 결과를 얻을 수 있습니다.

| supplier_id |
| :---------- |
| 1000        |
| 2000        |
| 3000        |
| 4000        |
| 6000        |
| 7000        |
| 8000        |

이 예제에서 볼 수 있듯이 UNION 연산자는 suppliers 테이블과 orders 테이블 모두에서 모든 supplier_id 값을 가져와서 결합된 결과 집합을 반환했습니다. UNION 연산자가 결과 집합 간의 중복을 제거했기 때문에 suppliers 및 orders 테이블 모두에서 발견되었음에도 불구하고 2000의 supplier_id는 한 번만 나타납니다. 중복을 제거하지 않으려면 [UNION ALL 연산자](UNION_ALL.md)를 대신 사용해보십시오.

---
## 예제 - 다양한 필드 이름
각 SELECT 문에서 해당 열의 이름이 같을 필요는 없지만 해당 데이터 유형이 같아야 합니다.

SELECT 문 간에 열 이름이 같지 않은 경우, 특히 [ORDER BY 절](ORDER_BY.md)을 사용하여 쿼리 결과를 정렬하려는 경우 약간 까다로워질 수 있습니다.

열 이름이 다른 UNION 연산자를 사용하여 쿼리 결과를 정렬하는 방법을 살펴보겠습니다.

예를 들어
```SQL
SELECT supplier_id, supplier_name
FROM suppliers
WHERE supplier_id > 2000
UNION
SELECT company_id, company_name
FROM companies
WHERE company_id > 1000
ORDER BY 1;
```
이 SQL UNION 예제에서는 두 SELECT 문 간에 열 이름이 다르기 때문에 결과 집합에서 열의 위치에 따라 ORDER BY 절에서 열을 참조하는 것이 더 유리합니다. 이 예제에서는 **ORDER BY 1**로 표시된 것처럼 supplier_id / company_id별로 결과를 오름차순으로 정렬했습니다. supplier_id / company_id 필드는 결과 집합에서 1번 위치에 있습니다.

이제 데이터를 사용하여 이 예제를 더 자세히 살펴보겠습니다.

suppliers 테이블에 다음과 같은 레코드가 채워져 있다고 가정해 보겠습니다.

| supplier_id | supplier_name |
| :---------- | :------------ |
| 1000        | Microsoft     |
| 2000        | Oracle        |
| 3000        | Apple         |
| 4000        | Samsung       |

그리고 companies 테이블에 다음 레코드가 채워져있습니다.

| company_id | company_name |
| :--------- | :----------- |
| 1000       | Microsoft    |
| 3000       | Apple        |
| 7000       | Sony         |
| 8000       | IBM          |

그리고 다음 UNION 문을 실행했습니다.
```SQL
SELECT supplier_id, supplier_name
FROM suppliers
WHERE supplier_id > 2000
UNION
SELECT company_id, company_name
FROM companies
WHERE company_id > 1000
ORDER BY 1;
```
다음과 같은 결과를 얻을 수 있습니다.

| supplier_id | supplier_name |
| :---------- | :------------ |
| 3000        | Apple         |
| 4000        | Samsung       |
| 7000        | Sony          |
| 8000        | IBM           |

첫째, UNION 쿼리가 중복 항목을 제거했기 때문에 supplier_id가 3000인 레코드가 결과 집합에 한 번만 나타납니다.

둘째, 결과 집합의 열 이름이 supplier_id 및 supplier_name이라는 것을 알 수 있습니다. 이는 UNION의 첫 번째 SELECT 문에서 사용된 열 이름이기 때문입니다.

원한다면 다음과 같이 열의 [별칭](ALIASES.md)을 지정할 수 있습니다.
```SQL
SELECT supplier_id AS ID_Value, supplier_name AS Name_Value
FROM suppliers
WHERE supplier_id > 2000
UNION
SELECT company_id AS ID_Value, company_name AS Name_Value
FROM companies
WHERE company_id > 1000
ORDER BY 1;
```
이제 결과의 열 이름이 첫 번째 열의 경우 ID_Value로, 두 번째 열의 경우 Name_Value로 별칭이 지정됩니다.

| ID_Value | Name_Value |
| :------- | :--------- |
| 3000     | Apple      |
| 4000     | Samsung    |
| 7000     | Sony       |
| 8000     | IBM        |

---
## 자주 묻는 질문
- 질문 : 두 날짜를 비교하고 날짜 값을 기반으로 필드의 개수를 반환해야 합니다. 예를 들어 테이블에 last_updated_date라는 날짜 필드가 있습니다. TRUNC(last_updated_date) >= TRUNC(sysdate-13)인지 확인해야 합니다.

- 답변 : 집계 함수인 [COUNT 함수](COUNT.md)를 사용하고 있으므로 Oracle UNION 연산자를 사용하는 것이 좋습니다. 예를 들어 다음을 시도해 볼 수 있습니다.
```SQL
SELECT a.code AS Code, a.name AS Name, COUNT(b.Ncode)
FROM cdmaster a, nmmaster b
WHERE a.code = b.code
AND a.status = 1
AND b.status = 1
AND b.Ncode <> 'a10'
AND TRUNC(last_updated_date) <= TRUNC(sysdate-13)
GROUP BY a.code, a.name
UNION
SELECT a.code AS Code, a.name AS Name, COUNT(b.Ncode)
FROM cdmaster a, nmmaster b
WHERE a.code = b.code
AND a.status = 1
AND b.status = 1
AND b.Ncode <> 'a10'
AND TRUNC(last_updated_date) > TRUNC(sysdate-13)
GROUP BY a.code, a.name;
```
Oracle UNION을 사용하면 하나의 기준 집합을 기반으로 카운트를 수행할 수 있습니다.
```SQL
TRUNC(last_updated_date) <= TRUNC(sysdate-13)
```
또한 다른 기준 집합을 기반으로 카운트를 수행합니다.
```SQL
TRUNC(last_updated_date) > TRUNC(sysdate-13)
```

---
**[< 이전](SELECT_TOP.md) / [다음 : UNION ALL >](UNION_ALL.md)**