# Oracle / PLSQL : TRUNCATE TABLE 문
이 Oracle 튜토리얼에서는 구문, 예제 및 연습 문제를 통해 Oracle **TRUNCATE TABLE 문**을 사용하는 방법을 설명합니다.

## 설명
TRUNCATE TABLE 문은 Oracle의 테이블에서 모든 레코드를 제거하는 데 사용됩니다. 이 문은 WHERE 절이 없는 DELETE 문과 동일한 기능을 수행합니다.

>경고 : 테이블을 잘라낸 경우 TRUNCATE TABLE 문은 롤백할 수 없습니다.

## 구문
Oracle/PLSQL에서 TRUNCATE TABLE 문의 구문은 다음과 같습니다.
```SQL
TRUNCATE TABLE [schema_name.]table_name
  [ PRESERVE MATERIALIZED VIEW LOG | PURGE MATERIALIZED VIEW LOG ]
  [ DROP STORAGE | REUSE STORAGE ] ;
```
### 매개변수 및 인수
#### **schema_name**
- 선택 사항입니다. 지정하면 테이블이 속한 스키마의 이름입니다.
#### **table_name**
- 잘라내려는 테이블입니다.
#### **PRESERVE MATERIALIZED VIEW LOG(구체화된 뷰 로그 보존)**
- 선택 사항입니다. 지정하면 테이블이 잘릴 때 구체화된 뷰 로그가 보존됩니다. 이것이 기본 동작입니다.
#### **PURGE MATERIALIZED VIEW LOG(구체화된 뷰 로그 제거)**
- 선택 사항입니다. 지정하면 테이블이 잘릴 때 구체화된 뷰 로그가 제거됩니다.
#### **DROP STORAGE(저장소 삭제)**
- 선택 사항입니다. 이 옵션을 지정하면 잘린 행에 대한 모든 저장소가 할당된 공간을 제외하고 할당 해제됩니다. 이것이 기본 동작입니다.
#### **REUSE STORAGE(저장소 재사용)**
- 선택 사항입니다. 지정하면 잘린 행에 대한 모든 저장소가 테이블에 할당된 상태로 유지됩니다.

---
## 예제
Oracle에서 테이블을 잘라내는 것은 롤백에 대해 걱정할 필요가 없는 경우 테이블에서 레코드를 빠르게 지울 수 있는 방법입니다. 그 이유 중 하나는 테이블을 잘라내도 테이블의 인덱스, 트리거 또는 종속성에 영향을 미치지 않기 때문입니다. 또한 테이블을 잘라내는 것이 테이블을 삭제하고 다시 만드는 것보다 훨씬 쉽습니다.

Oracle/PLSQL에서 TRUNCATE TABLE 문을 사용하는 방법을 예로 들어 보겠습니다.
```SQL
TRUNCATE TABLE customers;
```
이 예제는 customers 테이블을 잘라내고 해당 테이블에서 모든 레코드를 제거합니다.

이는 Oracle에서 다음과 같은 DELETE 문과 동일합니다.
```SQL
DELETE FROM customers;
```
이 두 문 모두 customers 테이블의 모든 데이터가 삭제됩니다. 이 둘의 주요 차이점은 원하는 경우 DELETE 문을 롤백할 수 있지만 TRUNCATE TABLE 문은 롤백할 수 없다는 것입니다.

테이블 이름 앞에 스키마 이름을 접두사로 붙이는 예제를 하나 더 살펴보겠습니다.
```SQL
TRUNCATE TABLE totn.suppliers;
```
이 예제에서는 suppliers라는 테이블을 totn이라는 스키마에서 잘라냅니다. 다른 스키마에서 테이블을 잘라내려면 먼저 DROP ANY TABLE과 같은 필요한 권한이 있어야 합니다.

---
**[< 이전](DELETE.md) / [다음 : EXISTS >](EXISTS.md)**