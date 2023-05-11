# Oracle / PLSQL : CHECK 제약 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 CHECK 제약 조건을 사용하는 방법을 설명합니다.

---
## Oracle에서 CHECK 제약 조건이란 무엇인가요?
CHECK 제약 조건을 사용하면 테이블의 각 행에 조건을 지정할 수 있습니다.

## 참고
- SQL 뷰에는 CHECK 제약 조건을 정의할 수 없습니다.
- 테이블에 정의된 CHECK 제약 조건은 해당 테이블의 열만 참조해야 합니다. 다른 테이블의 열을 참조할 수 없습니다.
- CHECK 제약 조건에는 SQL 하위 쿼리가 포함될 수 없습니다.
- CHECK 제약 조건은 SQL CREATE TABLE 문 또는 SQL ALTER TABLE 문에서 정의할 수 있습니다.

## CREATE TABLE 문 사용
Oracle에서 CREATE TABLE 문을 사용하여 CHECK 제약 조건을 생성하는 구문은 다음과 같습니다.
```sql
CREATE TABLE table_name
(
  column1 datatype null/not null,
  column2 datatype null/not null,

  ...

  CONSTRAINT constraint_name CHECK (column_name condition) [DISABLE]

);
```
DISABLE 키워드는 선택 사항이다. DISABLE 키워드를 사용하여 CHECK 제약 조건을 생성하는 경우 제약 조건은 생성되지만 조건은 적용되지 않습니다.

### 예제
```sql
CREATE TABLE suppliers
(
  supplier_id numeric(4),
  supplier_name varchar2(50),
  CONSTRAINT check_supplier_id
  CHECK (supplier_id BETWEEN 100 and 9999)
);
```
이 첫 번째 예제에서는 suppliers 테이블에 check_supplier_id라는 CHECK 제약 조건을 만들었습니다. 이 제약 조건은 supplier_id 필드에 100에서 9999 사이의 값이 포함되도록 합니다.
```sql
CREATE TABLE suppliers
(
  supplier_id numeric(4),
  supplier_name varchar2(50),
  CONSTRAINT check_supplier_name
  CHECK (supplier_name = upper(supplier_name))
);
```
이 두 번째 예제에서는 check_supplier_name이라는 CHECK 제약 조건을 만들었습니다. 이 제약 조건은 supplier_name 열에 항상 대문자가 포함되도록 합니다.

---
## ALTER TABLE 문 사용
Oracle의 ALTER TABLE 문에서 CHECK 제약 조건을 생성하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (column_name condition) [DISABLE];
```
DISABLE 키워드는 선택 사항입니다. DISABLE 키워드를 사용하여 CHECK 제약 조건을 생성하는 경우 제약 조건은 생성되지만 조건은 적용되지 않습니다.

### 예제
```sql
ALTER TABLE suppliers
ADD CONSTRAINT check_supplier_name
  CHECK (supplier_name IN ('IBM', 'Microsoft', 'NVIDIA'));
```
이 예제에서는 기존 suppliers 테이블에 check_supplier_name이라는 CHECK 제약 조건을 만들었습니다. 이 제약 조건은 supplier_name 필드에 다음 값만 포함되도록 합니다. (IBM, Microsoft, NVIDIA).

---
## CHECK 제약 조건 삭제
CHECK 제약 조건을 삭제하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

### 예제
```sql
ALTER TABLE suppliers
DROP CONSTRAINT check_supplier_id;
```
이 예제에서는 suppliers 테이블에 check_supplier_id라는 CHECK 제약 조건을 삭제합니다.

---
## CHECK 제약 조건 활성화
Oracle에서 CHECK 제약 조건을 활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ENABLE CONSTRAINT constraint_name;
```

### 예제
```sql
ALTER TABLE suppliers
ENABLE CONSTRAINT check_supplier_id;
```
이 예제에서는 suppliers 테이블에 check_supplier_id라는 CHECK 제약 조건을 활성화합니다.

---
## CHECK 제약 조건 비활성화
Oracle에서 CHECK 제약 조건을 비활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
DISABLE CONSTRAINT constraint_name;
```

### 예제
```sql
ALTER TABLE suppliers
DISABLE CONSTRAINT check_supplier_id;
```
이 예제에서는 suppliers 테이블에서 check_supplier_id라는 CHECK 제약 조건을 비활성화합니다.

---
**[< 이전](UNIQUE_Constraints.md) / [다음 : Indexes >](Indexes.md)**