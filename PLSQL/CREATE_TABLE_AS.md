# Oracle / PLSQL : CREATE TABLE AS 문

이 Oracle 튜토리얼에서는 구문 및 예제와 함께 Oracle CREATE TABLE AS 문을 사용하는 방법을 설명합니다.

## 설명
Oracle CREATE TABLE AS 문을 사용하여 기존 테이블의 열을 복사하여 기존 테이블에서 테이블을 만들 수도 있습니다.

이 방법으로 테이블을 생성할 때 새 테이블은 기존 테이블의 레코드로 채워진다는 점에 유의해야 합니다. (SELECT 문에 따라)

---
## 테이블 만들기 - 다른 테이블에서 모든 열 복사하기
### 구문
Oracle/PLSQL의 모든 열을 복사하는 CREATE TABLE AS 문의 구문은 다음과 같습니다.
```sql
CREATE TABLE new_table
  AS (SELECT * FROM old_table);
```

### 예제
다른 테이블의 모든 열을 복사하여 테이블을 만드는 방법을 보여 주는 CREATE TABLE AS 예제를 살펴 보겠습니다.
```sql
CREATE TABLE suppliers
AS (SELECT *
    FROM companies
    WHERE company_id < 5000);
```
이 예제에서는 companies 테이블의 모든 열을 포함하는 suppliers라는 새 테이블을 만듭니다.

companies 테이블에 레코드가 있는 경우 새 suppliers 테이블은 SELECT 문에서 반환된 레코드로 채워집니다.

---
## 테이블 만들기 - 다른 테이블에서 선택한 열 복사하기
### 구문
Oracle/PLSQL에서 선택한 열을 복사하는 CREATE TABLE AS 문의 구문은 다음과 같습니다.
```sql
CREATE TABLE new_table
  AS (SELECT column_1, column2, ... column_n
      FROM old_table);
```

### 예제
다른 테이블에서 선택한 열을 복사하여 테이블을 만드는 방법을 보여 주는 CREATE TABLE AS 예제를 살펴보겠습니다.
```sql
CREATE TABLE suppliers
  AS (SELECT company_id, address, city, state, zip
      FROM companies
      WHERE company_id < 5000);
```
이 예제에서는 suppliers라는 새 테이블을 만들지만 새 테이블에는 companies 테이블에서 지정된 열(예: company_id, address, city, state 및 zip)만 포함됩니다.

다시 말하지만, companies 테이블에 레코드가 있는 경우 새 suppliers 테이블은 SELECT 문에서 반환된 레코드로 채워집니다.

---
## 테이블 만들기 - 여러 테이블에서 선택한 열 복사하기
### 구문
Oracle/PLSQL에서 여러 테이블의 열을 복사하는 CREATE TABLE AS 문의 구문은 다음과 같습니다.
```sql
CREATE TABLE new_table
  AS (SELECT column_1, column2, ... column_n
      FROM old_table_1, old_table_2, ... old_table_n);
```

### 예제
여러 테이블에서 선택한 열을 복사하여 테이블을 만드는 방법을 보여 주는 CREATE TABLE AS 예제를 살펴보겠습니다.
```sql
CREATE TABLE suppliers
  AS (SELECT companies.company_id, companies.address, categories.category_type
      FROM companies, categories
      WHERE companies.company_id = categories.category_id
      AND companies.company_id < 5000);
```

이 예제에서는 companies 및 categories 테이블의 열 정의(예: company_id, address 및 category_type)를 기반으로 suppliers라는 새 테이블을 만듭니다.

---
## 자주 묻는 질문
- 질문 : 이전 테이블의 값을 복사하지 않고 다른 테이블에서 Oracle 테이블을 만들려면 어떻게 해야 하나요?

- 답변 : 이를 위해 Oracle CREATE TABLE 구문을 사용하면 됩니다.
```sql
CREATE TABLE new_table
  AS (SELECT *
      FROM old_table WHERE 1=2);
```
예를 들어
```sql
CREATE TABLE suppliers
  AS (SELECT *
      FROM companies WHERE 1=2);
```
이렇게 하면 companies 테이블의 모든 열 정의가 포함되지만 companies 테이블의 데이터는 포함되지 않는 suppliers라는 새 테이블이 만들어집니다.

감사의 말씀: 이 솔루션을 제공해 주신 Daniel W.에게 감사의 말씀을 드립니다!

---
**[< 이전](CREATE_TABLE.md) / [다음 : Primary Keys >](Primary_Keys.md)**