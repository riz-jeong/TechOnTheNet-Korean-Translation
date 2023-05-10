# Oracle / PLSQL : UNIQUE 제약 조건

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 UNIQUE 제약 조건을 생성, 삭제, 비활성화 및 활성화하는 방법을 설명합니다.

## Oracle에서 UNIQUE 제약 조건이란 무엇인가요?
UNIQUE 제약 조건은 레코드를 고유하게 정의하는 단일 필드 또는 필드 조합입니다. 일부 필드는 값의 조합이 고유한 경우 null 값을 포함할 수 있습니다.

## 참고
- Oracle에서 UNIQUE 제약 조건은 32개 이상의 열을 포함할 수 없습니다.
- UNIQUE 제약 조건은 CREATE TABLE 문 또는 ALTER TABLE 문에서 정의할 수 있습니다.


## UNIQUE 제약 조건과 기본 키의 차이점은 무엇입니까?
| 기본 키 | UNIQUE 제약 조건 |
|:--|:--|
| 기본 키의 일부인 필드 중 어느 것도 널 값을 포함할 수 없습니다. | UNIQUE 제약 조건의 일부인 일부 필드는 값의 조합이 고유한 경우 null 값을 포함할 수 있습니다. |

Oracle에서는 동일한 열에 기본 키와 UNIQUE 제약 조건을 모두 생성하는 것을 허용하지 않습니다.

---
## UNIQUE 제약 조건 만들기 - CREATE TABLE 문 사용
Oracle에서 CREATE TABLE 문을 사용하여 UNIQUE 제약 조건을 생성하는 구문은 다음과 같습니다.
```sql
CREATE TABLE table_name
(
  column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],
  ...

  CONSTRAINT constraint_name UNIQUE (uc_col1, uc_col2, ... uc_col_n)
);
```
#### **table_name**
- 생성하려는 테이블의 이름입니다.
#### **column1, column2**
- 테이블에 만들려는 열입니다.
#### **constraint_name**
- UNIQUE 제약 조건의 이름입니다.
#### **uc_col1, uc_col2, ... uc_col_n**
- UNIQUE 제약 조건을 구성하는 열입니다.

### 예제
CREATE TABLE 문을 사용하여 Oracle에서 UNIQUE 제약 조건을 생성하는 방법의 예를 살펴보겠습니다.
```sql
CREATE TABLE supplier
( supplier_id numeric(10) NOT NULL,
  supplier_name varchar2(50) NOT NULL,
  CONTACT_NAME VARCHAR2(50),
  CONSTRAINT supplier_unique UNIQUE (supplier_id)
);
```
이 예제에서는 supplier 테이블에 supplier_unique라는 UNIQUE 제약 조건을 만들었습니다. 이 제약 조건은 supplier_id 필드라는 하나의 필드로만 구성됩니다.

아래 예제에서처럼 둘 이상의 필드로 UNIQUE 제약 조건을 만들 수도 있습니다.
```sql
CREATE TABLE supplier
( supplier_id numeric(10) NOT NULL,
  supplier_name varchar2(50) NOT NULL,
  CONTACT_NAME VARCHAR2(50),
  CONSTRAINT supplier_unique UNIQUE (supplier_id, supplier_name)
);
```

---
## UNIQUE 제약 조건 만들기 - ALTER TABLE 문 사용
Oracle에서 ALTER TABLE 문을 사용하여 UNIQUE 제약 조건을 생성하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column1, column2, ... column_n);
```
#### **table_name**
- 수정할 테이블의 이름입니다. UNIQUE 제약 조건을 추가하려는 테이블입니다.
#### **constraint_name**
- UNIQUE 제약 조건의 이름입니다.
#### **column1, column2, ... column_n**
- UNIQUE 제약 조건을 구성하는 열입니다.

### 예제
ALTER TABLE 문을 사용하여 Oracle의 기존 테이블에 UNIQUE 제약 조건을 추가하는 방법에 대한 예제를 살펴보겠습니다.
```sql
ALTER TABLE supplier
ADD CONSTRAINT supplier_unique UNIQUE (supplier_id);
```
이 예제에서는 기존 supplier 테이블에 supplier_unique라는 UNIQUE 제약 조건을 만들었습니다. 이 제약 조건은 supplier_id라는 필드로 구성됩니다.

아래 예제에서처럼 둘 이상의 필드를 사용하여 UNIQUE 제약 조건을 만들 수도 있습니다.
```sql
ALTER TABLE supplier
ADD CONSTRAINT supplier_name_unique UNIQUE (supplier_id, supplier_name);
```

---
## UNIQUE 제약 조건 삭제
Oracle에서 UNIQUE 제약 조건을 삭제하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```
#### **table_name**
- 수정할 테이블의 이름입니다. UNIQUE 제약 조건을 제거하려는 테이블입니다.
#### **constraint_name**
- 제거할 UNIQUE 제약 조건의 이름입니다.

### 예제
Oracle의 테이블에서 UNIQUE 제약 조건을 제거하는 방법의 예를 살펴보겠습니다.
```sql
ALTER TABLE supplier
DROP CONSTRAINT supplier_unique;
```
이 예제에서는 supplier 테이블에서 supplier_unique라는 UNIQUE 제약 조건을 삭제합니다.

---
## UNIQUE 제약 조건 비활성화
Oracle에서 UNIQUE 제약 조건을 비활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
DISABLE CONSTRAINT constraint_name;
```
#### **table_name**
- 수정할 테이블의 이름입니다. 비활성화하려는 UNIQUE 제약 조건이 있는 테이블입니다.
#### **constraint_name**
- 비활성화할 UNIQUE 제약 조건의 이름입니다.

### 예제
Oracle에서 UNIQUE 제약 조건을 비활성화하는 방법의 예를 살펴보겠습니다.
```sql
ALTER TABLE supplier
DISABLE CONSTRAINT supplier_unique;
```
이 예제에서는 supplier 테이블에서 supplier_unique라는 UNIQUE 제약 조건을 비활성화합니다.

---
## UNIQUE 제약 조건 활성화
Oracle에서 UNIQUE 제약 조건을 활성화하는 구문은 다음과 같습니다.
```sql
ALTER TABLE table_name
ENABLE CONSTRAINT constraint_name;
```
#### **table_name**
- 수정할 테이블의 이름입니다. UNIQUE 제약 조건을 활성화하려는 테이블입니다.
#### **constraint_name**
- 활성화할 UNIQUE 제약 조건의 이름입니다.

### 예제
Oracle에서 UNIQUE 제약 조건을 활성화하는 방법에 대한 예제를 살펴보겠습니다.
```sql
ALTER TABLE supplier
ENABLE CONSTRAINT supplier_unique;
```
이 예제에서는 supplier 테이블에 supplier_unique라는 UNIQUE 제약 조건을 활성화합니다.

---
**[< 이전](Foreign_Keys_Enable.md) / [다음 : Check Constraints >](CHECK_Constraints.md)**