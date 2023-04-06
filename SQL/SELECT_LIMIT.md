# SQL : SELECT LIMIT 문

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL에서 **SELECT LIMIT 문**을 사용하는 방법을 설명합니다.

## 설명
SQL SELECT LIMIT 문은 데이터베이스의 하나 이상의 테이블에서 레코드를 검색하고 제한 값에 따라 반환되는 레코드 수를 제한하는 데 사용됩니다.

>팁: 모든 SQL 데이터베이스에서 SELECT LIMIT가 지원되는 것은 아닙니다.
>
>SQL Server 또는 MSAccess와 같은 데이터베이스의 경우 SELECT TOP 문을 사용하여 결과를 제한합니다. SELECT TOP 문은 SELECT LIMIT 문에 해당하는 Microsoft의 독점 문입니다.

## 구문
SQL에서 SELECT LIMIT 문의 구문은 다음과 같습니다.
```SQL
SELECT expressions
FROM tables
[WHERE conditions]
[ORDER BY expression [ ASC | DESC ]]
LIMIT number_rows [ OFFSET offset_value ];
```
### 매개변수 및 인수
#### **expressions(표현식)**
- 검색하려는 열 또는 계산입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.
#### **ORDER BY expression**
- 선택 사항입니다. 결과 순서를 지정하고 반환하려는 레코드를 대상으로 지정할 수 있도록 SELECT LIMIT 문에서 사용됩니다. ASC는 오름차순, DESC는 내림차순입니다.
#### **LIMIT number_rows**
- number_rows를 기준으로 반환할 결과 집합의 행 수를 제한하도록 지정합니다. 예를 들어, LIMIT 10은 SELECT 조건과 일치하는 처음 10개의 행을 반환합니다. 이 경우 정렬 순서가 중요하므로 ORDER BY 절을 적절히 사용해야 합니다.
#### **OFFSET offset_value**
- 선택 사항입니다. LIMIT가 반환하는 첫 번째 행은 offset_value에 의해 결정됩니다.

---
## 예제 - LIMIT 키워드 사옹
SQL에서 LIMIT 절과 함께 SELECT 문을 사용하는 방법을 살펴보겠습니다.
```SQL
SELECT contact_id, last_name, first_name
FROM contacts
WHERE website = 'TechOnTheNet.com'
ORDER BY contact_id DESC
LIMIT 5;
```
이 SQL SELECT LIMIT 예제는 contacts 테이블에서 website가 'TechOnTheNet.com'인 처음 5개의 레코드를 선택합니다. 결과는 contact_id를 기준으로 내림차순으로 정렬되므로 SELECT LIMIT 문에서 가장 큰 5개 contact_id 값이 반환된다는 의미입니다.

contacts 테이블에 website 값이 'TechOnTheNet.com'인 다른 레코드가 있는 경우 SQL의 SELECT LIMIT 문에 의해 반환되지 않습니다.

가장 큰 값 대신 가장 작은 5개의 contact_id 값을 선택하려면 다음과 같이 정렬 순서를 변경할 수 있습니다:
```SQL
SELECT contact_id, last_name, first_name
FROM contacts
WHERE website = 'TechOnTheNet.com'
ORDER BY contact_id ASC
LIMIT 5;
```
이제 결과는 contact_id를 기준으로 오름차순으로 정렬되므로 이 SELECT LIMIT 문에서는 website가 'TechOnTheNet.com'인 가장 작은 contact_id 레코드 5개가 반환됩니다. 이 쿼리에서는 다른 레코드는 반환되지 않습니다.

---
## 예제 - OFFSET 키워드 사용
OFFSET 키워드를 사용하면 LIMIT 절에서 반환된 첫 번째 레코드를 오프셋할 수 있습니다.
```SQL
LIMIT 3 OFFSET 1
```
이 LIMIT 절은 결과 집합에서 오프셋이 1인 레코드 3개를 반환합니다. 즉, SELECT 문은 일반적으로 반환되는 첫 번째 레코드를 건너뛰고 대신 두 번째, 세 번째 및 네 번째 레코드를 반환합니다.

SQL에서 OFFSET 절과 함께 SELECT LIMIT 문을 사용하는 방법을 살펴보겠습니다.
```SQL
SELECT contact_id, last_name, first_name
FROM contacts
WHERE website = 'TechOnTheNet.com'
ORDER BY contact_id DESC
LIMIT 5 OFFSET 2;
```
이 SQL SELECT LIMIT 예제에서는 결과 집합의 첫 번째 및 두 번째 레코드를 건너뛰고 다음 5개의 행을 반환한다는 의미의 OFFSET 2를 사용합니다.

---
**[< 이전](HAVING.md) / [다음 : SELECT TOP >](SELECT_TOP.md)**