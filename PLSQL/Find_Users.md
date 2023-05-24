# Oracle / PLSQL : 사용자 찾기

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle 데이터베이스에서 생성된 모든 사용자를 찾는 방법을 설명합니다.

## 설명
명령 프롬프트에서 쿼리를 실행하여 Oracle에서 생성된 모든 사용자를 찾을 수 있습니다. 사용자 정보는 검색하려는 사용자 정보에 따라 ALL_USERS 및 DBA_USERS와 같은 다양한 시스템 테이블에 저장됩니다.

---
## ALL_USERS
현재 사용자에게 표시되는 모든 사용자를 찾아야 하는 경우 ALL_USERS 테이블을 쿼리할 수 있습니다. Oracle/PLSQL의 ALL_USERS 테이블에서 사용자 정보를 검색하는 구문은 다음과 같습니다.
```sql
SELECT *
FROM ALL_USERS;
```
ALL_USERS 테이블에는 다음 열이 포함됩니다.

| 열 | 설명 |
| :-- | :-- |
| USERNAME | 사용자 이름 |
| USER_ID | 사용자에게 할당된 숫자 ID |
| CREATED | 사용자가 생성된 날짜 |

---
## DBA_USERS
Oracle에 존재하는 모든 사용자를 찾아야 하거나 사용자에 대한 자세한 정보가 필요한 경우 DBA_USERS라는 다른 시스템 테이블도 있습니다.

Oracle/PLSQL의 DBA_USERS 테이블에서 사용자 정보를 검색하는 구문은 다음과 같습니다.
```sql
SELECT *
FROM DBA_USERS;
```
DBA_USERS 테이블에는 다음 열이 포함됩니다.

| 열 | 설명 |
| :-- | :-- |
| USERNAME | 사용자 이름 |
| USER_ID | 사용자에게 할당된 숫자 ID |
| PASSWORD | 사용 중단 |
| ACCOUNT_STATUS | 다음과 같은 사용자 상태<br>- OPEN<br>- EXPIRED<br>- EXPIRED(GRACE)<br>- EXPIRED(TIMED)<br>- LOCKED<br>- EXPIRED & LOCKED(TIMED)<br>- EXPIRED(GRACE) & LOCKED(TIMED)<br>- EXPIRED & LOCKED<br>- EXPIRED(GRACE) & LOCKED<br> |
| LOCK_DATE | 사용자가 잠긴 날짜(해당되는 경우) |
| EXPIRY_DATE | 사용자가 만료된 날짜 |
| DEFAULT_TABLESPACE | 사용자의 기본 테이블 스페이스 |
| TEMPORARY_TABLESPACE | 사용자를 위한 임시 테이블 스페이스 |
| CREATED | 사용자가 생성된 날짜 |
| PROFILE | 사용자 리소스 프로필 이름 |
| INITIAL_RSRC_CONSUMER_GROUP | 사용자의 초기 리소스 소비자 그룹 |
| EXTERNAL_NAME | 사용자의 외부 이름 |
| PASSWORD_VERSIONS | 비밀번호 해시 버전 목록 |
| EDITIONS_ENABLED | 사용자에 대해 에디션이 활성화되었는지 여부를 나타내는 Y/N입니다. |
| AUTHENTICATION_TYPE | 사용자 인증 방법 |
| PROXY_ONLY_CONNECT | 사용자가 직접 연결할 수 있는지 또는 프록시로만 연결할 수 있는지를 나타내는 Y/N입니다. |
| COMMON | 사용자가 일반 사용자인지 여부를 나타내는 YES/NO입니다. |
| LAST_LOGIN | 마지막 로그인 시간 |
| ORACLE_MAINTAINED | Oracle에서 제공하는 스크립트에 의해 사용자가 생성 및 유지 관리되었는지 여부를 나타내는 Y/N입니다. |

---
**[< 이전](DROP_USER.md) / [다음 : Find Users Logged In >](Find_Users_Logged_In.md)**