# SQL : DROP TABLE 문

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **DROP TABLE 문**을 사용하는 방법을 설명합니다.

## 설명
SQL DROP TABLE 문을 사용하면 SQL 데이터베이스에서 테이블을 제거하거나 삭제할 수 있습니다.

## 구문
SQL에서 DROP TABLE 문의 구문은 다음과 같습니다.
```SQL
DROP TABLE table_name;
```
### 매개변수 및 인수
#### **table_name**
- 데이터베이스에서 제거할 테이블의 이름입니다.

## 예제
더 이상 필요하지 않은 테이블을 생성했을 수 있습니다. DROP TABLE 문을 사용하여 데이터베이스에서 테이블을 제거할 수 있습니다.

DROP TABLE 문을 사용하여 테이블을 삭제하는 방법을 보여주는 예제를 살펴보겠습니다.
```SQL
DROP TABLE suppliers;
```
이 DROP TABLE 문 예제는 suppliers라는 테이블을 삭제합니다. 이렇게 하면 suppliers 테이블과 관련된 레코드와 해당 테이블 정의가 모두 제거됩니다.

테이블을 삭제한 후에는 테이블이 이미 존재한다는 오류 없이 suppliers 테이블을 다시 만들 수 있습니다.

테이블 이름 앞에 데이터베이스 이름을 접두사로 붙이는 예제를 하나 더 살펴보겠습니다.
```SQL
DROP TABLE totn.contacts;
```
이 예제에서는 totn 데이터베이스에 있는 contacts라는 테이블을 삭제했습니다.

>팁: 테이블의 정의를 변경하기 위해 ALTER TABLE 문을 사용하는 대신 테이블을 삭제하고 다시 생성하는 것이 더 쉬운 경우가 있습니다.

---
**[< 이전](ALTER_TABLE.md) / [다음 : VIEWS >](VIEWS.md)**