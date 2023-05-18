# Oracle / PLSQL : Synonyms

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **시노님을 만들고 삭제**하는 방법을 설명합니다.

## 설명
**시노님**은 테이블, 뷰, 시퀀스, 저장 프로시저 및 기타 데이터베이스 개체와 같은 개체의 대체 이름입니다.

일반적으로 다른 스키마의 개체에 대한 액세스 권한을 부여할 때 시노님을 사용하며, 사용자가 어떤 스키마가 개체를 소유하고 있는지 걱정할 필요가 없도록 하려는 경우에도 시노님을 사용합니다.

---
## 시노님 생성 혹은 교체
사용자가 쿼리에서 테이블을 사용할 때 테이블 이름 앞에 스키마 이름을 붙이지 않아도 되도록 시노님을 만들 수 있습니다.

### 구문
Oracle에서 시노님을 만드는 구문은 다음과 같습니다.
```sql
CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema .] synonym_name
  FOR [schema .] object_name [@ dblink];
```
#### **OR REPLACE**
- DROP 시노님 명령을 실행하지 않고도 시노님을 다시 생성할 수 있습니다.
#### **PUBLIC**
- 시노님이 공개 시노님이며 모든 사용자가 액세스할 수 있음을 의미합니다. 하지만 시노님을 사용하려면 먼저 사용자에게 해당 개체에 대한 적절한 권한이 있어야 합니다.
#### **schema**
- 적절한 스키마. 이 문구를 생략하면 Oracle은 사용자가 자신의 스키마를 참조하는 것으로 간주합니다.
#### **object_name**
- 시노님을 만들려는 객체의 이름입니다. 다음 중 하나가 될 수 있습니다.
    + 테이블
    + 뷰
    + 시퀀스
    + 저장 프로시저
    + 함수
    + 패키지
    + 구체화 뷰
    + 자바 클래스 스키마 객체
    + 사용자 정의 객체
    + 시노님

### 예제
Oracle에서 시노님을 만드는 방법의 예를 살펴보겠습니다.
```sql
CREATE PUBLIC SYNONYM suppliers
FOR app.suppliers;
```
이 첫 번째 CREATE SYNONYM 예제에서는 suppliers라는 시노님을 만드는 방법을 보여 줍니다. 이제 다른 스키마 사용자는 테이블 이름 앞에 app이라는 스키마를 붙이지 않고도 suppliers라는 테이블을 참조할 수 있습니다.
```sql
SELECT *
FROM suppliers;
```
이 시노님이 이미 존재하고 이를 재정의하려는 경우 다음과 같이 OR REPLACE 구문을 사용할 수 있습니다:
```sql
CREATE OR REPLACE PUBLIC SYNONYM suppliers
FOR app.suppliers;
```

---
## 시노님 삭제
Oracle에서 시노님이 생성된 후 시노님을 삭제할 수도 있습니다.

### 구문
Oracle에서 시노님을 삭제하는 구문은 다음과 같습니다.
```sql
DROP [PUBLIC] SYNONYM [schema .] synonym_name [force];
```
#### **PUBLIC**
- 공개 시노님을 삭제할 수 있습니다. PUBLIC을 지정한 경우 스키마를 지정하지 않습니다.
#### **force**
- 종속성이 있는 경우에도 Oracle이 시노님을 강제로 삭제합니다. 강제로 삭제하면 Oracle 객체가 무효화될 수 있으므로 사용하지 않는 것이 좋습니다.

### 예제
Oracle에서 시노님을 삭제하는 방법의 예를 살펴보겠습니다.
```sql
DROP PUBLIC SYNONYM suppliers;
```
이 DROP 문은 앞서 정의한 suppliers라는 시노님을 삭제합니다.

---
**[< 이전](Grant_Revoke.md) / [다음 : Roles >](Roles.md)**