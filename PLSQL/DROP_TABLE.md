# Oracle / PLSQL : DROP TABLE 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **DROP TABLE 문**을 사용하는 방법을 설명합니다.

## 설명
Oracle DROP TABLE 문을 사용하면 Oracle 데이터베이스에서 테이블을 제거하거나 삭제할 수 있습니다.

## 구문
Oracle DROP TABLE 문의 구문은 다음과 같습니다.
```sql
DROP TABLE [schema_name].table_name
[ CASCADE CONSTRAINTS ]
[ PURGE ];
```
### 매개변수 및 인수
#### **schema_name**
- 테이블을 소유하는 스키마의 이름입니다.
#### **table_name**
- Oracle 데이터베이스에서 제거할 테이블의 이름입니다.
#### **CASCADE CONSTRAINTS**
- 선택 사항입니다. 지정하면 모든 참조 무결성 제약 조건도 삭제됩니다.
#### **PURGE**
- 선택 사항입니다. 지정하면 테이블 및 해당 종속 개체가 휴지통에서 제거되며 테이블을 복구할 수 없습니다. 지정하지 않으면 테이블 및 해당 종속 개체가 휴지통에 배치되며 필요한 경우 나중에 복구할 수 있습니다.

## 참고
- table_name에 참조 무결성 제약 조건이 있고 CASCADE CONSTRAINTS 옵션을 지정하지 않은 경우 DROP TABLE 문은 오류를 반환하고 Oracle은 테이블을 삭제하지 않습니다.

---
## 예제
DROP TABLE 문을 사용하여 Oracle에서 테이블을 삭제하는 방법을 보여주는 예제를 살펴보겠습니다.
```sql
DROP TABLE customers;
```
이 Oracle DROP TABLE 예제는 customers라는 테이블을 삭제합니다.

### Purge
Oracle에서 DROP TABLE 문과 함께 PURGE 옵션을 사용하는 방법을 살펴보겠습니다.

Oracle에서 DROP TABLE 문을 실행할 때 PURGE 옵션을 지정할 수 있습니다. PURGE 옵션은 테이블과 해당 종속 개체를 제거하여 휴지통에 나타나지 않도록 합니다. PURGE 옵션을 지정하면 테이블을 복구할 수 없다는 위험이 있습니다. 그러나 PURGE를 사용하면 중요한 데이터가 휴지통에 남아 있지 않도록 할 수 있다는 이점이 있습니다.
```sql
DROP TABLE customers PURGE;
```
이 DROP TABLE 문은 customers라는 테이블을 삭제하고 PURGE를 실행하여 customers 테이블과 관련된 공간을 해제합니다. 즉, customers 테이블은 휴지통에 배치되지 않으므로 나중에 필요한 경우 복구할 수 없습니다.

---
**[< 이전](ALTER_TABLE.md) / [다음 : VIEWS >](VIEWS.md)**