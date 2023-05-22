# Oracle / PLSQL : DROP USER 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **DROP USER 문**을 사용하는 방법을 설명합니다.

## 설명
**DROP USER 문**은 Oracle 데이터베이스에서 사용자를 제거하고 해당 사용자가 소유한 모든 객체를 제거하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 **DROP USER 문**의 구문은 다음과 같습니다.
```sql
DROP USER user_name [ CASCADE ];
```
### 매개변수 및 인수
#### **user_name**
- Oracle 데이터베이스에서 제거할 사용자의 이름입니다.
#### **CASCADE**
- 선택 사항입니다. user_name이 객체(스키마의 테이블 또는 뷰)를 소유하고 있는 경우 객체를 모두 삭제하려면 CASCADE를 지정해야 합니다.

---
## 예제
간단한 DROP USER 문을 살펴보겠습니다.

사용자가 스키마에 어떤 객체도 소유하고 있지 않은 경우 다음 DROP USER 문을 실행할 수 있습니다.
```sql
DROP USER smithj;
```
그러면 smithj라는 사용자가 삭제됩니다. 이 DROP USER 문은 smithj가 스키마에 어떤 객체도 소유하지 않은 경우에만 실행됩니다.

smithj가 스키마에 객체를 소유하고 있는 경우 다음 DROP USER 문을 실행해야 합니다.
```sql
DROP USER smithj CASCADE;
```
이 DROP USER 문은 사용자 smithj를 제거하고, smithj가 소유한 모든 객체(테이블 및 뷰)를 삭제하며, smithj의 객체에 대한 모든 참조 무결성 제약 조건도 삭제됩니다.

---
**[< 이전](Change_Password.md) / [다음 : Find Users >](Find_Users.md)**