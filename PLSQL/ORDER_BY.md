# Oracle / PLSQL : ORDER BY 절

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **ORDER BY 절**을 사용하는 방법을 설명합니다.

## 설명
Oracle ORDER BY 절은 결과 집합의 레코드를 정렬하는 데 사용됩니다. ORDER BY 절은 [SELECT 문](SELECT.md)에서만 사용할 수 있습니다.

## 구문
Oracle/PLSQL에서 ORDER BY 절의 구문은 다음과 같습니다.
```SQL
SELECT expressions
FROM tables
[WHERE conditions]
ORDER BY expression [ ASC | DESC ];
```
### 매개변수 및 인수
#### **expressions(표현식)**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 하나 이상의 테이블이 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.
#### **ASC**
- 선택 사항입니다. 표현식별로 결과 집합을 오름차순으로 정렬합니다. 기본 동작입니다.
#### **DESC**
- 선택 사항입니다. 결과 집합을 표현식별로 내림차순으로 정렬합니다.

## 참고
ORDER BY 절에 ASC 또는 DESC 수정자가 제공되지 않으면 결과는 표현식별로 오름차순으로 정렬됩니다. (이는 `ORDER BY expression ASC`와 동일합니다)

---
## 예제 - ASC/DESC 속성을 사용하지 않고 정렬하기
Oracle ORDER BY 절은 ASC 또는 DESC 값을 지정하지 않고 사용할 수 있습니다. 이 속성을 ORDER BY 절에서 생략하면 정렬 순서는 기본적으로 ASC 또는 오름차순으로 설정됩니다.

예를 들어
```SQL
SELECT supplier_city
FROM suppliers
WHERE supplier_name = 'Microsoft'
ORDER BY supplier_city;
```
이 Oracle ORDER BY 예제는 supplier_city 필드를 기준으로 오름차순으로 정렬된 모든 레코드를 반환하며, 이는 다음 ORDER BY 절과 동일합니다:
```SQL
SELECT supplier_city
FROM suppliers
WHERE supplier_name = 'Microsoft'
ORDER BY supplier_city ASC;
```
대부분의 프로그래머는 오름차순으로 정렬하는 경우 ASC 속성을 생략합니다.

---
## 예제 - 내림차순으로 정렬하기
결과 집합을 내림차순으로 정렬하는 경우 다음과 같이 ORDER BY 절에 DESC 속성을 사용합니다:
```SQL
SELECT supplier_city
FROM suppliers
WHERE supplier_name = 'Microsoft'
ORDER BY supplier_city DESC;
```
이 Oracle ORDER BY 예제는 supplier_city 필드를 기준으로 내림차순으로 정렬된 모든 레코드를 반환합니다.

---
## 예제 - 상대적 위치를 기준으로 정렬
Oracle ORDER BY 절을 사용하여 결과 집합의 상대적 위치를 기준으로 정렬할 수도 있습니다. 여기서 결과 집합의 첫 번째 필드는 1이고 다음 필드는 2인 식으로 정렬할 수 있습니다.

예를 들어
```SQL
SELECT supplier_city
FROM suppliers
WHERE supplier_name = 'Microsoft'
ORDER BY 1 DESC;
```
이 Oracle ORDER BY는 supplier_city 필드가 결과 집합에서 1번 위치에 있으므로 supplier_city 필드를 기준으로 내림차순으로 정렬된 모든 레코드를 반환하며, 이는 다음 ORDER BY 절과 동일합니다.
```SQL
SELECT supplier_city
FROM suppliers
WHERE supplier_name = 'Microsoft'
ORDER BY supplier_city DESC;
```

---
## 예제 - ASC 및 DESC 속성 모두 사용
Oracle ORDER BY 절을 사용하여 결과 집합을 정렬할 때 단일 [SELECT 문](SELECT.md)에서 ASC 및 DESC 속성을 사용할 수 있습니다.

예를 들면 다음과 같습니다.
```SQL
SELECT supplier_city, supplier_state
FROM suppliers
WHERE supplier_name = 'Microsoft'
ORDER BY supplier_city DESC, supplier_state ASC;
```
이 Oracle ORDER BY는 supplier_city 필드를 기준으로 내림차순으로 정렬된 모든 레코드를 반환하고, supplier_state를 기준으로 오름차순으로 2차 정렬합니다.

---
**[< 이전](WHERE.md) / [다음 : AND >](AND.md)**