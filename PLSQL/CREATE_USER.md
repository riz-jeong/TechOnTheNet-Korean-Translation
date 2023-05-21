# Oracle / PLSQL : CREATE USER 문
이 Oracle 튜토리얼에서는 구문 및 예제와 함께 Oracle **CREATE USER 문**을 사용하는 방법을 설명합니다.

## 설명
CREATE USER 문은 Oracle 데이터베이스에 로그인할 수 있는 데이터베이스 계정을 만듭니다.

## 구문

```sql
CREATE USER user_name 
  IDENTIFIED { BY password
             | EXTERNALLY [ AS 'certificate_DN' ]
             | GLOBALLY [ AS '[ directory_DN ]' ]
             }
  [ DEFAULT TABLESPACE tablespace
  | TEMPORARY TABLESPACE
       { tablespace | tablespace_group }
  | QUOTA integer [ K | M | G | T | P | E ]
        | UNLIMITED }
        ON tablespace
    [ QUOTA integer [ K | M | G | T | P | E ]
        | UNLIMITED }
            ON tablespace
    ]
  | PROFILE profile_name
  | PASSWORD EXPIRE
  | ACCOUNT { LOCK | UNLOCK }
     [ DEFAULT TABLESPACE tablespace
     | TEMPORARY TABLESPACE
         { tablespace | tablespace_group }
     | QUOTA integer [ K | M | G | T | P | E ]
           | UNLIMITED }
           ON tablespace
       [ QUOTA integer [ K | M | G | T | P | E ]
           | UNLIMITED }
           ON tablespace
        ]
     | PROFILE profile
     | PASSWORD EXPIRE
     | ACCOUNT { LOCK | UNLOCK } ]
     ] ;
```
### 매개변수 및 인수
#### **user_name**
- 만들려는 데이터베이스 계정의 이름입니다.
#### **PROFILE profile_name**
- 선택 사항입니다. 사용자 계정에 할당된 데이터베이스 리소스의 양을 제한하기 위해 사용자 계정에 할당하려는 프로필의 이름입니다. 이 옵션을 생략하면 기본 프로필이 사용자에게 할당됩니다.
#### **PASSWORD EXPIRE**
- 선택 사항입니다. 이 옵션을 설정하면 사용자가 Oracle 데이터베이스에 로그인하기 전에 비밀번호를 재설정해야 합니다.
#### **ACCOUNT LOCK**
- 선택 사항입니다. 사용자 계정에 대한 액세스를 비활성화합니다.
#### **ACCOUNT UNLOCK**
- 선택 사항입니다. 사용자 계정에 액세스할 수 있습니다.

---
## 예제
새 사용자를 만들고 비밀번호를 할당하는 간단한 CREATE USER 문을 실행하려는 경우 다음과 같이 할 수 있습니다.
```sql
CREATE USER smithj
  IDENTIFIED BY pwd4smithj
  DEFAULT TABLESPACE tbs_perm_01
  TEMPORARY TABLESPACE tbs_temp_01
  QUOTA 20M on tbs_perm_01;
```
이 CREATE USER 문은 Oracle 데이터베이스에 비밀번호는 pwd4smithj, 기본 테이블 스페이스는 20MB의 할당량을 가진 tbs_perm_01, 임시 테이블 스페이스는 tbs_temp_01인 smithj라는 새 사용자를 생성합니다.

사용자가 데이터베이스에 로그인하기 전에 비밀번호를 변경했는지 확인하려는 경우 다음과 같이 PASSWORD EXPIRE 옵션을 추가할 수 있습니다.
```sql
CREATE USER smithj
  IDENTIFIED BY pwd4smithj
  DEFAULT TABLESPACE tbs_perm_01
  TEMPORARY TABLESPACE tbs_temp_01
  QUOTA 20M on tbs_perm_01
  PASSWORD EXPIRE;
```

### 외부 데이터베이스 사용자
외부 데이터베이스 사용자를 생성하려면 다음 CREATE USER 문을 실행하면 됩니다.
```sql
CREATE USER external_user1
  IDENTIFIED EXTERNALLY
  DEFAULT TABLESPACE tbs_perm_01
  QUOTA 5M on tbs_perm_01
  PROFILE external_user_profile;
```
이 CREATE USER 문은 기본 테이블 스페이스가 tbs_perm_01이고 인용량이 5MB이며 external_user_profile에 할당된 데이터베이스 리소스에 의해 제한되는 external_user1이라는 외부 데이터베이스 사용자를 생성합니다.

운영체제 계정으로만 액세스할 수 있는 외부 데이터베이스 사용자를 만들려면 다음 CREATE USER 문을 실행하면 됩니다.
```sql
CREATE USER ops$external_user1
  IDENTIFIED EXTERNALLY
  DEFAULT TABLESPACE tbs_perm_01
  QUOTA 5M on tbs_perm_01
  PROFILE external_user_profile;
```
이 CREATE USER 문과 이전 문과의 유일한 차이점은 user_name 앞에 ops$가 있다는 점입니다.

### 전역 데이터베이스 사용자
전역 데이터베이스 사용자를 생성하려면 다음 CREATE USER 문을 실행하면 됩니다.
```sql
CREATE USER global_user1
  IDENTIFIED GLOBALLY AS 'CN=manager, OU=division, O=oracle, C=US'
  DEFAULT TABLESPACE tbs_perm_01
  QUOTA 10M on tbs_perm_01;
```
이 CREATE USER 문은 기본 테이블 스페이스가 tbs_perm_01이고 견적이 10M인 global_user1이라는 전역 데이터베이스 사용자를 생성합니다.

---
**[< 이전](Roles.md) / [다음 : Change Password >](Change_Password.md)**