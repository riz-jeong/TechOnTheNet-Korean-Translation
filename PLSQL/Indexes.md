# Oracle / PLSQL : 인덱스

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 인덱스를 만들고, 이름을 바꾸고, 삭제하는 방법을 설명합니다.

## Oracle에서 인덱스란 무엇인가요?
인덱스는 레코드를 더 빠르게 검색할 수 있도록 하는 성능 튜닝 방법입니다. 인덱스는 인덱싱된 열에 나타나는 각 값에 대한 항목을 만듭니다. 기본적으로 Oracle은 B-트리 인덱스를 생성합니다.

---
## 인덱스 만들기

### 구문
Oracle/PLSQL에서 인덱스를 생성하는 구문은 다음과 같습니다.
```sql
CREATE [UNIQUE] INDEX index_name
  ON table_name (column1, column2, ... column_n)
  [ COMPUTE STATISTICS ];
```
#### **UNIQUE**
- 인덱싱된 행의 값 조합이 고유해야 함을 나타냅니다.
#### **index_name**
- 인덱스에 할당할 이름입니다.
#### **table_name**
- 인덱스를 생성할 테이블의 이름입니다.
#### **column1, column2, ... column_n**
- 인덱스에서 사용할 열입니다.
#### **COMPUTE STATISTICS**
- 인덱스를 생성하는 동안 Oracle에 통계를 수집하도록 지시합니다. 그런 다음 최적화 프로그램에서 이 통계를 사용하여 SQL 문이 실행될 때 "실행 계획"을 선택합니다.

### 예제
Oracle/PLSQL에서 인덱스를 생성하는 방법의 예를 살펴보겠습니다.
```sql
CREATE INDEX supplier_idx
  ON supplier (supplier_name);
```
이 예제에서는 supplier 테이블에 supplier_idx라는 인덱스를 생성했습니다. 이 인덱스는 supplier_name 필드라는 하나의 필드로만 구성됩니다.

아래 예제에서와 같이 둘 이상의 필드로 인덱스를 생성할 수도 있습니다.
```sql
CREATE INDEX supplier_idx
  ON supplier (supplier_name, city);
```
또한 다음과 같이 인덱스 생성 시 통계를 수집하도록 선택할 수도 있습니다.
```sql
CREATE INDEX supplier_idx
  ON supplier (supplier_name, city)
  COMPUTE STATISTICS;
```

---
## 함수 기반 인덱스 만들기
Oracle에서는 열에 대해서만 인덱스를 생성하는 것으로 제한되지 않습니다. 함수 기반 인덱스를 만들 수 있습니다.

### 구문
Oracle/PLSQL에서 함수 기반 인덱스를 생성하는 구문은 다음과 같습니다.
```sql
CREATE [UNIQUE] INDEX index_name
  ON table_name (function1, function2, ... function_n)
  [ COMPUTE STATISTICS ];
```
#### **UNIQUE**
- 인덱싱된 행의 값 조합이 고유해야 함을 나타냅니다.
#### **index_name**
- 인덱스에 할당할 이름입니다.
#### **table_name**
- 인덱스를 생성할 테이블의 이름입니다.
#### **function1, function2, ... function_n**
- 인덱스에 사용할 함수입니다.
#### **COMPUTE STATISTICS**
- 인덱스를 생성하는 동안 오라클에 통계를 수집하도록 지시합니다. 그런 다음 최적화 프로그램에서 이 통계를 사용하여 SQL 문이 실행될 때 "실행 계획"을 선택합니다.

### 예제
Oracle/PLSQL에서 함수 기반 인덱스를 생성하는 방법의 예를 살펴보겠습니다.
```sql
CREATE INDEX supplier_idx
  ON supplier (UPPER(supplier_name));
```
이 예제에서는 supplier_name 필드의 대문자 평가를 기반으로 인덱스를 생성했습니다.

그러나 Oracle 옵티마이저가 SQL 문을 실행할 때 이 인덱스를 사용하도록 하려면 UPPER(supplier_name)가 NULL 값으로 평가되지 않는지 확인해야 합니다. 이를 확인하려면 다음과 같이 WHERE 절에 **UPPER(supplier_name) IS NOT NULL**을 추가합니다.
```sql
SELECT supplier_id, supplier_name, UPPER(supplier_name)
FROM supplier
WHERE UPPER(supplier_name) IS NOT NULL
ORDER BY UPPER(supplier_name);
```

---
## 인덱스 이름 바꾸기

### 구문
Oracle/PLSQL에서 인덱스 이름을 바꾸는 구문은 다음과 같습니다.
```sql
ALTER INDEX index_name
  RENAME TO new_index_name;
```
#### **index_name**
- 이름을 바꾸려는 인덱스의 이름입니다.
#### **NEW_INDEX_NAME**
- 인덱스에 할당할 새 이름입니다.

### 예제
Oracle/PLSQL에서 인덱스 이름을 바꾸는 방법의 예를 살펴보겠습니다.
```sql
ALTER INDEX supplier_idx
  RENAME TO supplier_index_name;
```
이 예제에서는 supplier_idx라는 인덱스의 이름을 supplier_index_name으로 변경합니다.

---
## 인덱스에 대한 통계 수집
인덱스를 처음 생성할 때 인덱스에 대한 통계를 수집하는 것을 잊었거나 통계를 업데이트하려는 경우, 나중에 언제든지 ALTER INDEX 명령을 사용하여 통계를 수집할 수 있습니다.

### 구문
Oracle/PLSQL에서 인덱스에 대한 통계를 수집하는 구문은 다음과 같습니다.
```sql
ALTER INDEX index_name
  REBUILD COMPUTE STATISTICS;
```
#### **index_name**
- 통계를 수집할 인덱스입니다.

### 예제
Oracle/PLSQL에서 인덱스에 대한 통계를 수집하는 방법의 예를 살펴보겠습니다.
```sql
ALTER INDEX supplier_idx
  REBUILD COMPUTE STATISTICS;
```
이 예제에서는 supplier_idx라는 인덱스에 대한 통계를 수집합니다.

---
## 인덱스 삭제

### 구문
Oracle/PLSQL에서 인덱스를 삭제하는 구문은 다음과 같습니다.
```sql
DROP INDEX index_name;
```
#### **index_name**
- 삭제할 인덱스의 이름입니다.

### 예제
Oracle/PLSQL에서 인덱스를 삭제하는 방법의 예를 살펴보겠습니다.
```sql
DROP INDEX supplier_idx;
```
이 예제에서는 supplier_idx라는 인덱스를 삭제합니다.

---
**[< 이전](CHECK_Constraints.md) / [다음 : Grant/Revoke >](Grant_Revoke.md)**