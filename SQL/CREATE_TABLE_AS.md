# SQL : CREATE TABLE AS 문

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **CREATE TABLE AS 문**을 사용하는 방법을 설명합니다.

## 설명
SQL CREATE TABLE AS 문을 사용하여 기존 테이블의 열을 복사하여 기존 테이블에서 테이블을 만들 수도 있습니다.

이 방법으로 테이블을 만들 때 새 테이블은 기존 테이블의 레코드로 채워진다는 점에 유의해야 합니다. ([SELECT 문](SELECT.md)에 따라)

---
## 테이블 만들기 - 다른 테이블에서 모든 열 복사하기

### 구문
SQL에서 모든 열을 복사할 때 CREATE TABLE AS 문의 구문은 다음과 같습니다.
```SQL
CREATE TABLE new_table
  AS (SELECT * FROM old_table);
```

### 예제
다른 테이블에서 모든 열을 복사하여 테이블을 만드는 방법을 보여주는 예제를 살펴보겠습니다.
```SQL
CREATE TABLE suppliers
AS (SELECT *
    FROM companies
    WHERE id > 1000)
```
이렇게 하면 companies 테이블의 모든 열이 포함된 suppliers라는 새 테이블이 만들어집니다.

companies 테이블에 레코드가 있는 경우 새 suppliers 테이블에는 SELECT 문으로 선택한 레코드도 포함됩니다.

---
## 테이블 만들기 - 다른 테이블에서 선택한 열 복사하기

### 구문
선택한 열을 복사하는 CREATE TABLE AS 문의 구문은 다음과 같습니다.
```SQL
CREATE TABLE new_table
  AS (SELECT column_1, column2, ... column_n
      FROM old_table);
```

### 예제
다른 테이블에서 선택한 열을 복사하여 테이블을 만드는 방법을 보여주는 예제를 살펴보겠습니다.
```SQL
CREATE TABLE suppliers
  AS (SELECT id, address, city, state, zip
      FROM companies
      WHERE id > 1000);
```
이렇게 하면 suppliers라는 새 테이블이 만들어지지만 새 테이블에는 companies 테이블의 지정된 열만 포함됩니다.

다시 말하지만, companies 테이블에 레코드가 있는 경우 새 suppliers 테이블에는 SELECT 문으로 선택한 레코드도 포함됩니다.

---
## 테이블 만들기 - 여러 테이블에서 선택한 열 복사하기

### 구문
여러 테이블의 열을 복사하는 CREATE TABLE AS 문의 구문은 다음과 같습니다.
```SQL
CREATE TABLE new_table
  AS (SELECT column_1, column2, ... column_n
      FROM old_table_1, old_table_2, ... old_table_n);
```

### 예제
여러 테이블에서 선택한 열을 복사하여 테이블을 만드는 방법을 보여주는 예제를 살펴보겠습니다.
```SQL
CREATE TABLE suppliers
  AS (SELECT companies.id, companies.address, categories.cat_type
      FROM companies, categories
      WHERE companies.id = categories.id
      AND companies.id > 1000);
```
이렇게 하면 companies 및 categories 테이블의 열을 기반으로 suppliers라는 새 테이블이 만들어집니다.

---
## 자주 묻는 질문
- 질문 : 이전 테이블의 값을 복사하지 않고 다른 테이블에서 SQL 테이블을 만들려면 어떻게 해야 하나요?

- 답변 : 이를 위해 SQL CREATE TABLE 구문은 다음과 같습니다.
```SQL
CREATE TABLE new_table
  AS (SELECT *
      FROM old_table WHERE 1=2);
```
예를 들어
```SQL
CREATE TABLE suppliers
  AS (SELECT *
      FROM companies WHERE 1=2);
```
이렇게 하면 companies 테이블의 모든 열을 포함하지만 companies 테이블의 데이터는 포함하지 않는 suppliers라는 새 테이블이 만들어집니다.

감사의 말씀: 이 솔루션을 제공해 주신 Daniel W.에게 감사의 말씀을 드립니다!

---
**[< 이전](CREATE_TABLE.md) / [다음 : Primary Keys >](Primary_Keys.md)**