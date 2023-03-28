# SQL : 전역 임시 테이블

이 SQL 튜토리얼에서는 구문과 예제를 사용하여 SQL **전역 임시 테이블**을 만드는 방법을 설명합니다.

## 설명
SQL 전역 임시 테이블은 SQL 세션 내에서 개별적으로 생성되는 테이블입니다.

## 구문
SQL에서 전역 임시 테이블을 만드는 구문은 다음과 같습니다.
```SQL
CREATE GLOBAL TEMPORARY TABLE table_name
( column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],
  ...
);
```
### 매개변수 및 인수
#### **table_name**
- 생성하려는 전역 임시 테이블의 이름입니다.
#### **column1, column2**
- 전역 임시 테이블에 생성하려는 열입니다. 각 열에는 데이터 유형이 있어야 합니다. 열은 NULL 또는 NOT NULL로 정의되어야 하며, 이 값을 비워두면 데이터베이스는 NULL을 기본값으로 간주합니다.

---
## 예제
SQL CREATE GLOBAL TEMPORARY TABLE 예제를 살펴보겠습니다.
```SQL
CREATE GLOBAL TEMPORARY TABLE suppliers_temp
( supplier_id numeric(10) NOT NULL,
  supplier_name char(50) NOT NULL,
  contact_name char(50)
);
```
이 예제에서는 suppliers_temp라는 전역 임시 테이블을 생성합니다.

---
**[< 이전](VIEWS.md) / [다음 : LOCAL TEMP >](LOCAL_TEMP.md)**