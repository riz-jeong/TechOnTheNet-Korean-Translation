# Oracle / PLSQL : Roles

이 Oracle 튜토리얼에서는 역할을 만들고, 역할에 권한을 부여/해지하고, 역할을 활성화/비활성화하고, 역할을 기본값으로 설정하고, Oracle에서 역할을 삭제하는 방법을 구문과 예제를 통해 설명합니다.

## 설명
**역할**은 사용자 또는 다른 역할에 부여할 수 있는 권한의 집합 또는 그룹입니다. 데이터베이스 관리자가 시간과 노력을 절약할 수 있는 좋은 방법입니다.

---
## 역할 만들기
사용자의 권한을 논리적으로 그룹화할 수 있도록 역할을 만들 수 있습니다. 역할을 만들려면 역할 만들기 시스템 권한이 있어야 한다는 점에 유의하세요.

### 구문
Oracle에서 역할을 만드는 구문은 다음과 같습니다.
```sql
CREATE ROLE role_name
[ NOT IDENTIFIED | 
IDENTIFIED {BY password | USING [schema.] package | EXTERNALLY | GLOBALLY } ;
```
#### **role_name**
- 새로 만들 역할의 이름입니다. 권한 그룹을 참조하는 방법입니다.
#### **NOT IDENTIFIED**
- 역할이 즉시 사용하도록 설정되었음을 의미합니다. 역할을 활성화하는 데 비밀번호가 필요하지 않습니다.
#### **IDENTIFIED**
- 역할이 활성화되기 전에 사용자가 지정된 방법으로 권한을 부여받아야 합니다.
#### **BY password**
- 사용자가 역할을 활성화하려면 비밀번호를 제공해야 합니다.
#### **USING package**
- 애플리케이션 역할을 생성한다는 의미입니다. (인증된 패키지를 사용하는 애플리케이션에서만 활성화되는 역할입니다.)
#### **EXTERNALLY**
- 사용자가 역할을 활성화하려면 외부 서비스에서 권한을 부여받아야 합니다. 외부 서비스는 운영 체제 또는 타사 서비스일 수 있습니다.
#### **GLOBALLY**
- 사용자가 역할을 활성화하려면 엔터프라이즈 디렉터리 서비스에서 권한을 부여받아야 합니다.

### 참고
- CREATE ROLE 문에서 NOT IDENTIFIED 및 IDENTIFIED가 모두 생략된 경우 역할은 NOT IDENTIFIED 역할로 생성됩니다.

### 예제
Oracle에서 역할을 만드는 방법의 예를 살펴보겠습니다.
```sql
CREATE ROLE test_role;
```
이 첫 번째 예제에서는 test_role이라는 역할을 만듭니다.
```sql
CREATE ROLE test_role
IDENTIFIED BY test123;
```
이 두 번째 예제에서는 test_role이라는 동일한 역할을 만들지만 이제는 test123이라는 비밀번호로 비밀번호로 보호됩니다.

---
## 역할에 테이블 권한 부여
Oracle에서 역할을 만들었으면 다음 단계는 해당 역할에 권한을 부여하는 것입니다.

사용자에게 권한을 부여한 것과 마찬가지로 역할에 권한을 부여할 수 있습니다. 역할에 테이블 권한을 부여하는 것부터 시작하겠습니다. 테이블 권한은 SELECT, INSERT, UPDATE, DELETE, REFERENCES, ALTER, INDEX 또는 ALL의 모든 조합이 될 수 있습니다.

### 구문
Oracle에서 역할에 테이블 권한을 부여하는 구문은 다음과 같습니다.
```sql
GRANT privileges ON object TO role_name
```
#### **privileges**
- 역할에 할당할 권한입니다. 다음 값 중 하나를 사용할 수 있습니다.

| 권한 | 설명 |
| :-- | :-- |
| SELECT | 테이블에서 SELECT 문을 수행할 수 있습니다. |
| INSERT | 테이블에서 INSERT 문을 수행할 수 있습니다. |
| UPDATE | 테이블에서 UPDATE 문을 수행할 수 있습니다. |
| DELETE | 테이블에서 DELETE 문을 수행할 수 있습니다. |
| REFERENCES | 테이블을 참조하는 제약 조건을 생성할 수 있습니다. |
| ALTER | 테이블 정의를 변경하기 위해 ALTER TABLE 문을 수행할 수 있습니다. |
| INDEX | CREATE INDEX 문을 사용하여 테이블에 인덱스를 생성할 수 있습니다. |
| ALL | 테이블에 대한 모든 권한입니다. |

#### **object**
- 권한을 부여할 데이터베이스 객체의 이름입니다. 테이블에 권한을 부여하는 경우에는 테이블 이름이 됩니다.
#### **role_name**
- 권한이 부여될 역할의 이름입니다.

### 예제
Oracle에서 역할에 테이블 권한을 부여하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

suppliers라는 테이블에 대한 SELECT, INSERT, UPDATE 및 DELETE 권한을 test_role이라는 역할에 부여하려는 경우 다음 GRANT 문을 실행합니다.
```sql
GRANT select, insert, update, delete ON suppliers TO test_role;
```
ALL 키워드를 사용하여 모든 권한을 부여하도록 지정할 수도 있습니다.
```sql
GRANT all ON suppliers TO test_role;
```

---
## 역할에서 테이블 권한 제거
역할에 테이블 권한을 부여한 후에는 이러한 권한의 일부 또는 전부를 제거해야 할 수 있습니다. 이렇게 하려면 제거 명령을 실행하면 됩니다. SELECT, INSERT, UPDATE, DELETE, REFERENCES, ALTER, INDEX 또는 ALL의 모든 조합을 제거할 수 있습니다.

### 구문
Oracle에서 역할에서 테이블 권한을 제거하는 구문은 다음과 같습니다.
```sql
REVOKE privileges ON object FROM role_name;
```
#### **privileges**
- 역할에서 제거할 권한입니다. 다음 값 중 하나를 사용할 수 있습니다.

| 권한 | 설명 |
| :-- | :-- |
| SELECT | 테이블에서 SELECT 문을 수행할 수 있습니다. |
| INSERT | 테이블에서 INSERT 문을 수행할 수 있습니다. |
| UPDATE | 테이블에서 UPDATE 문을 수행할 수 있습니다. |
| DELETE | 테이블에서 DELETE 문을 수행할 수 있습니다. |
| REFERENCES | 테이블을 참조하는 제약 조건을 생성할 수 있습니다. |
| ALTER | 테이블 정의를 변경하기 위해 ALTER TABLE 문을 수행할 수 있습니다. |
| INDEX | CREATE INDEX 문을 사용하여 테이블에 인덱스를 생성할 수 있습니다. |
| ALL | 테이블에 대한 모든 권한입니다. |

#### **object**
- 권한을 제거하려는 데이터베이스 객체의 이름입니다. 테이블에 대한 권한을 제거하는 경우에는 테이블 이름이 됩니다.
#### **role_name**
- 권한이 제거될 역할의 이름입니다.

### 예제
Oracle에서 역할에서 테이블 권한을 제거하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

test_role이라는 역할에서 suppliers라는 테이블에 대한 DELETE 권한을 제거하려는 경우 다음 REVOKE 문을 실행합니다.
```sql
REVOKE delete ON suppliers FROM test_role;
```
test_role이라는 역할에서 suppliers라는 테이블에 대한 모든 권한을 제거하려는 경우 ALL 키워드를 사용할 수 있습니다.
```sql
REVOKE all ON suppliers FROM test_role;
```

---
## 역할에 함수/프로시저 권한 부여하기
함수 및 프로시저를 처리할 때 역할에 이러한 함수 및 프로시저를 실행할 수 있는 권한을 부여할 수 있습니다.

### 구문
Oracle에서 역할에 함수/프로시저에 대한 EXECUTE 권한을 부여하는 구문은 다음과 같습니다.
```sql
GRANT EXECUTE ON object TO role_name;
```
#### **EXECUTE**
- 함수/프로시저를 컴파일하는 기능 및 함수/프로시저를 직접 실행하는 기능입니다.
#### **object**
- 권한을 부여할 데이터베이스 객체의 이름입니다. 함수 또는 프로시저에 EXECUTE 권한을 부여하는 경우 함수 이름 또는 프로시저 이름이 됩니다.
#### **role_name**
- 실행 권한이 부여될 역할의 이름입니다.

### 예제
Oracle에서 역할에 함수 또는 프로시저에 대한 실행 권한을 부여하는 방법의 예를 살펴보겠습니다.

예를 들어 Find_Value라는 함수가 있고 test_role이라는 역할에 EXECUTE 액세스 권한을 부여하려는 경우 다음 GRANT 문을 실행합니다.
```sql
GRANT execute ON Find_Value TO test_role;
```

---
## 역할에서 기능/절차 권한 제거하기
함수 또는 프로시저에 대한 EXECUTE 권한을 역할에 부여한 후에는 해당 역할에서 이러한 권한을 제거해야 할 수 있습니다. 이렇게 하려면 REVOKE 명령을 실행하면 됩니다.

### 구문
Oracle에서 역할에서 함수 또는 프로시저에 대한 권한을 제거하는 구문은 다음과 같습니다.
```sql
REVOKE execute ON object FROM role_name;
```
#### **EXECUTE**
- 함수/프로시저를 컴파일하는 기능 및 함수/프로시저를 직접 실행하는 기능을 제거합니다.
#### **object**
- 권한을 제거하려는 데이터베이스 개체의 이름입니다. 함수 또는 프로시저에 대한 실행 권한을 제거하는 경우 함수 이름 또는 프로시저 이름이 됩니다.
#### **role_name**
- 실행 권한이 제거될 역할의 이름입니다.

### 예제
Oracle에서 역할에 함수 또는 프로시저에 대한 실행 권한을 제거하는 방법의 예를 살펴보겠습니다.

test_role이라는 역할에서 Find_Value라는 함수에 대한 EXECUTE 권한을 제거하려는 경우 다음 REVOKE 문을 실행합니다.
```sql
REVOKE execute ON Find_Value FROM test_role;
```

---
## 사용자에게 역할 부여
이제 역할을 만들고 역할에 권한을 할당했으므로 특정 사용자에게 역할을 부여할 수 있습니다.

### 구문
Oracle에서 사용자에게 역할을 부여하는 구문은 다음과 같습니다.
```sql
GRANT role_name TO user_name;
```
#### **role_name**
- 부여하려는 역할의 이름입니다.
#### **user_name**
- 역할이 부여될 사용자의 이름입니다.

### 예제
Oracle에서 사용자에게 역할을 부여하는 방법의 예를 살펴보겠습니다.
```sql
GRANT test_role TO smithj;
```
이 예제에서는 smithj라는 사용자에게 test_role이라는 역할을 부여합니다.

---
## 역할 활성화/비활성화(SET ROLE 문)
현재 세션에 대한 역할을 활성화 또는 비활성화하려면 SET ROLE 문을 사용하면 됩니다.

사용자가 Oracle에 로그인하면 모든 기본 역할이 사용하도록 설정되지만 기본 역할이 아닌 역할은 SET ROLE 문을 사용하여 사용하도록 설정해야 합니다.

### 구문
Oracle에서 SET ROLE 문의 구문은 다음과 같습니다.
```sql
SET ROLE
( role_name [ IDENTIFIED BY password ] | ALL [EXCEPT role1, role2, ... ] | NONE );
```
#### **role_name**
- 사용 설정하려는 역할의 이름입니다.
#### **IDENTIFIED BY password**
- 활성화할 역할의 비밀번호입니다. 역할에 비밀번호가 없는 경우에는 이 문구를 생략할 수 있습니다.
#### **ALL**
- 현재 세션에 대해 예외에 나열된 역할을 제외한 모든 역할을 활성화해야 함을 의미합니다.
#### **NONE**
- 현재 세션의 모든 역할(모든 기본 역할 포함)을 비활성화합니다.

### 예제
Oracle에서 역할을 활성화하는 방법의 예를 살펴보겠습니다.
```sql
SET ROLE test_role IDENTIFIED BY test123;
```
이 예제에서는 비밀번호가 test123인 test_role이라는 역할을 사용하도록 설정합니다.

---
## 역할을 기본 역할로 설정
기본 역할은 로그온 시 현재 세션에 대해 해당 역할이 항상 사용하도록 설정되어 있음을 의미합니다. SET ROLE 문을 실행할 필요가 없습니다. 역할을 기본 역할로 설정하려면 ALTER USER 문을 실행해야 합니다.

### 구문
Oracle에서 역할을 기본 역할로 설정하는 구문은 다음과 같습니다.
```sql
ALTER USER user_name
DEFAULT ROLE
( role_name | ALL [EXCEPT role1, role2, ... ] | NONE );
```
#### **user_name**
- 기본값으로 설정할 역할을 가진 사용자의 이름입니다.
#### **role_name**
- 기본값으로 설정할 역할의 이름입니다.
#### **ALL**
- 예외에 나열된 역할을 제외한 모든 역할을 기본값으로 사용하도록 설정해야 합니다.
#### **NONE**
- 모든 역할을 기본값으로 비활성화합니다.

### 예제
Oracle에서 역할을 기본 역할로 설정하는 방법의 예를 살펴보겠습니다.
```sql
ALTER USER smithj
DEFAULT ROLE
test_role;
```
이 예제에서는 test_role이라는 역할을 smithj라는 사용자에 대한 기본 역할로 설정합니다.
```sql
ALTER USER smithj
DEFAULT ROLE
ALL;
```
이 예제에서는 smithj에 할당된 모든 역할을 기본값으로 설정합니다.
```sql
ALTER USER smithj
DEFAULT ROLE
ALL EXCEPT test_role;
```
이 예제에서는 test_role이라는 역할을 제외하고 smithj에 할당된 모든 역할을 DEFAULT로 설정합니다.

---
## 역할 삭제
Oracle에서 역할을 생성한 후에는 어느 시점에서 역할을 삭제해야 할 수도 있습니다.

### 구문
Oracle에서 역할을 삭제하는 구문은 다음과 같습니다.
```sql
DROP ROLE role_name;
```
#### **role_name**
- 삭제할 역할의 이름입니다.

### 예제
Oracle에서 역할을 삭제하는 방법의 예를 살펴보겠습니다.
```sql
DROP ROLE test_role;
```
이 DROP 문은 앞서 정의한 test_role이라는 역할을 삭제합니다.

---
**[< 이전](Synonyms.md) / [다음 : Create User >](CREATE_USER.md)**