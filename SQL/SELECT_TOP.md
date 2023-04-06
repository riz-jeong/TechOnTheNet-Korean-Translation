# SQL : SELECT TOP 문

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **SELECT TOP 문**을 사용하는 방법을 설명합니다.

## 설명
SQL SELECT TOP 문은 데이터베이스의 하나 이상의 테이블에서 레코드를 검색하고 고정 값 또는 백분율에 따라 반환되는 레코드 수를 제한하는 데 사용됩니다.

>팁: SELECT TOP은 결과를 제한하기 위한 Microsoft의 독점 버전으로, SQL Server 및 MSAccess와 같은 데이터베이스에서 사용할 수 있습니다.
>
>다른 SQL 데이터베이스의 경우 [SELECT LIMIT 문](SELECT_LIMIT.md)을 사용해 보세요.

## 구문
SQL에서 SELECT TOP 문의 구문은 다음과 같습니다.
```SQL
SELECT TOP (top_value) [ PERCENT ]
expressions
FROM tables
[WHERE conditions]
[ORDER BY expression [ ASC | DESC ]];
```
### 매개변수 및 인수
#### **TOP (top_value)**
- 이 함수는 top_value를 기준으로 결과 집합에서 상위 행 수를 반환합니다. 예를 들어 TOP(10)은 전체 결과 집합에서 상위 10개 행을 반환합니다.
#### **PERCENT**
- 선택 사항입니다. PERCENT를 지정하면 상위 행은 전체 결과 집합의 백분율(top_value에 지정한 대로)을 기준으로 합니다. 예를 들어 TOP(10) PERCENT는 전체 결과 집합의 상위 10%를 반환합니다.
#### **expressions(표현식)**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.
#### **ORDER BY expression**
- 선택 사항입니다. 결과를 정렬하고 반환하려는 레코드를 대상으로 지정할 수 있도록 SELECT TOP 문에서 사용됩니다. ASC는 오름차순, DESC는 내림차순입니다.

---
## 예제 - TOP 키워드 사용
SELECT 문에서 TOP 키워드를 사용하는 SQL 예제를 살펴보겠습니다.
```SQL
SELECT TOP(5)
contact_id, last_name, first_name
FROM contacts
WHERE last_name = 'Anderson'
ORDER BY contact_id;
```
이 SQL SELECT TOP 예제는 contacts 테이블에서 last_name이 'Anderson'인 처음 5개의 레코드를 선택합니다. contacts 테이블에 last_name이 'Anderson'인 다른 레코드가 있는 경우 해당 레코드는 SELECT 문에서 반환되지 않습니다.

---
## 예제 - TOP PERCENT 키워드 사용
SELECT 문에서 TOP PERCENT 키워드를 사용하는 SQL 예제를 살펴보겠습니다.
```SQL
SELECT TOP(10) PERCENT
contact_id, last_name, first_name
FROM contacts
WHERE last_name = 'Anderson'
ORDER BY contact_id;
```
이 SQL SELECT TOP 예제는 전체 결과 집합에서 처음 10%의 레코드를 선택합니다. 따라서 이 예제에서 SELECT 문은 contacts 테이블에서 last_name이 'Anderson'인 상위 10%의 레코드를 반환합니다. 결과 집합의 나머지 90%는 SELECT 문에서 반환되지 않습니다.

---
**[< 이전](SELECT_LIMIT.md) / [다음 : UNION >](UNION.md)**