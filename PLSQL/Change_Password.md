# Oracle / PLSQL : Oracle에서 사용자 비밀번호 변경

**질문** : Oracle에서 사용자의 비밀번호를 변경하려면 어떻게 해야 하나요?

**답변** : Oracle에서 사용자의 비밀번호를 변경하려면 ALTER USER 명령을 실행해야 합니다.

## 구문
Oracle에서 비밀번호를 변경하는 구문은 다음과 같습니다.
```sql
ALTER USER user_name IDENTIFIED BY new_password;
```
### 매개변수 및 인수
#### **user_name**
- 비밀번호를 변경하려는 사용자입니다.
#### **new_password**
- 할당할 새 비밀번호입니다.

## 예제
Oracle/PLSQL에서 사용자의 비밀번호를 변경하는 방법의 예를 살펴보겠습니다.
```sql
ALTER USER smithj IDENTIFIED BY autumn;
```
이 예제에서는 smithj라는 사용자의 비밀번호를 autumn으로 변경합니다.

---
**[< 이전](CREATE_USER.md) / [다음 : Drop User >](DROP_USER.md)**