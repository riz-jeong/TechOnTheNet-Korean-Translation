# Oracle / PLSQL : 지역 임시 테이블

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle 지역 임시 테이블을 사용하는 방법을 설명합니다.

## 설명
Oracle 지역 임시 테이블은 Oracle 세션 내의 모듈 및 임베디드 SQL 프로그램 내에서 구별됩니다.

## 구문
Oracle 지역 임시 테이블 선언 구문은 다음과 같습니다.
```sql
DECLARE LOCAL TEMPORARY TABLE table_name
( column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],
  ...
  column_n datatype [ NULL | NOT NULL ]
);
```
### 매개변수 및 인수
#### **table_name**
- 생성하려는 지역 임시 테이블의 이름입니다.
#### **column1, column2, ... column_n**
- 지역 임시 테이블에 만들려는 열입니다. 각 열에는 데이터 유형이 있어야 합니다. 열은 NULL 또는 NOT NULL로 정의되어야 하며, 이 값을 비워두면 데이터베이스는 NULL을 기본값으로 간주합니다.

---
## 예제
Oracle 지역 임시 테이블 선언 예제를 살펴보겠습니다.
```sql
DECLARE LOCAL TEMPORARY TABLE suppliers_temp
( supplier_id number(10) NOT NULL,
  supplier_name varchar2(50) NOT NULL,
  contact_name varchar2(50)
);
```
이 예제는 Oracle에서 suppliers_temp라는 지역 임시 테이블을 생성합니다.

---
**[< 이전](GLOBAL_TEMP.md) / [다음 : Foreign Keys >](Foreign_Keys.md)**