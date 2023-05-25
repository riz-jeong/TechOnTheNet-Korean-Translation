# Oracle / PLSQL : Oracle/PLSQL에 로그인한 사용자 찾기

이 Oracle 튜토리얼에서는 현재 Oracle 데이터베이스에 로그인한 모든 사용자를 찾는 방법을 설명합니다.

## 설명
명령 프롬프트에서 쿼리를 실행하여 현재 Oracle에 로그인한 모든 사용자를 찾을 수 있습니다. Oracle/PLSQL에는 데이터베이스의 각 현재 세션에 대한 세션 정보를 표시하는 V$SESSION이라는 시스템 보기가 있습니다. 이 시스템 보기에 대한 쿼리를 실행하여 현재 Oracle/PLSQL 데이터베이스에서 연결이 실행 중인 모든 사용자를 반환할 수 있습니다.

## 구문
Oracle에 로그인한 사용자를 검색하는 구문은 다음과 같습니다.
```sql
SELECT USERNAME FROM V$SESSION;
```
이 SELECT 문은 로그인한 각 사용자 이름을 반환합니다.

V$SESSION 뷰에는 다음과 같은 열이 포함됩니다.

| 열 | 설명 |
| :-- | :-- |
| SADDR | 세션 주소 |
| SID | 세션 식별자 |
| SERIAL# | 세션의 일련 번호 |
| AUDSID | 감사 세션 ID |
| PADDR | 세션을 소유한 프로세스의 주소 |
| USER# | 사용자 식별자 |
| USERNAME | 사용자 이름(예: root, techonthenet 등) |
| COMMAND | 마지막으로 구문 분석된 문 |
| OWNERID | 마이그레이션 가능한 세션을 소유한 사용자 식별자 |
| TADDR | 트랜잭션 상태 개체의 주소 |
| LOCKWAIT | 잠금 대기를 위한 주소 |
| STATUS | 세션의 상태. 다음 중 하나일 수 있습니다 : ACTIVE, INACTIVE, KILLED, CACHED, or SNIPED. |
| SERVER | 서버 유형. 다음 중 하나일 수 있습니다 : DEDICATED, SHARED, PSEUDO, or NONE. |
| SCHEMA# | 스키마의 사용자 식별자 |
| SCHEMANAME | 스키마의 사용자 이름 |
| OSUSER | 운영 체제 클라이언트 사용자 이름 |
| PROCESS | 운영 체제 클라이언트 프로세스 ID |
| MACHINE | 운영 체제 머신 이름 |
| TERMINAL | 운영 체제 터미널 이름 |
| PROGRAM | 운영 체제 프로그램 이름 |
| TYPE | 세션 유형 |
| SQL_ADDRESS | 현재 실행 중인 SQL 문을 식별합니다(SQL_HASH_VALUE와 함께 사용). |
| SQL_HASH_VALUE | 현재 실행 중인 SQL 문을 식별합니다(SQL_ADDRESS와 함께 사용). |
| SQL_ID | 현재 실행 중인 SQL 문의 SQL 식별자 |
| SQL_CHILD_NUMBER | 현재 실행 중인 SQL 문의 하위 번호입니다. |
| PREV_SQL_ADDR | 마지막으로 실행된 SQL 문을 식별합니다(PREV_HASH_VALUE와 함께 사용). |
| PREV_HASH_VALUE | 마지막으로 실행된 SQL 문을 식별합니다(PREV_SQL_ADDR과 함께 사용). |
| PREV_SQL_ID | 마지막으로 실행된 SQL 문의 SQL 식별자 |
| PREV_CHILD_NUMBER | 마지막으로 실행된 SQL 문의 자식 번호 |
| MODULE | 현재 실행 중인 모듈의 이름(DBMS_APPLICATION_INFO.SET_MODULE에 따름) |
| MODULE_HASH | 현재 실행 중인 모듈의 해시 값 |
| ACTION | 현재 실행 중인 작업의 이름(DBMS_APPLICATION_INFO.SET_ACTION에 따름) |
| ACTION_HASH | 현재 실행 중인 액션의 해시값입니다. |
| CLIENT_INFO | 클라이언트 정보(DBMS_APPLICATION_INFO.SET_CLIENT_INFO에 따름) |
| FIXED_TABLE_SEQUENCE | 동적 성능 테이블에서 중간 선택이 있을 때마다 증가하는 시퀀스 번호입니다. |
| ROW_WAIT_OBJ# | ROW_WAIT_ROW#에 지정된 테이블의 객체 식별자 |
| ROW_WAIT_FILE# | ROW_WAIT_ROW#에 지정된 데이터 파일의 식별자 |
| ROW_WAIT_BLOCK# | ROW_WAIT_ROW#에 지정된 블록의 식별자 |
| ROW_WAIT_ROW# | 현재 잠긴 행 |
| LOGON_TIME | 사용자가 로그인한 시간 |
| LAST_CALL_ET | STATUS가 ACTIVE인 경우, LAST_CALL_ET은 세션이 활성화된 후 경과한 시간(초)입니다. STATUS가 INACTIVE인 경우, LAST_CALL_ET은 세션이 비활성 상태가 된 후 경과한 시간(초)입니다. |
| PDML_ENABLED | PDML_STATUS로 대체됨 |
| FAILOVER_TYPE | 세션에 대해 활성화된 투명 애플리케이션 장애 조치 유형입니다. 다음 중 하나일 수 있습니다: NONE, SESSION, or SELECT. |
| FAILOVER_METHOD | 세션에 대한 투명 애플리케이션 장애 조치 방법입니다. 다음 중 하나일 수 있습니다 : NONE, BASIC, or PRECONNECT. |
| FAILED_OVER | YES 또는 NO로 장애 조치 발생 여부를 나타냅니다. |
| RESOURCE_CONSUMER_GROUP | 세션의 리소스 소비자 그룹 |
| PDML_STATUS | ENABLED 또는 DISABLED |
| PDDL_STATUS | ENABLED 또는 DISABLED |
| PQ_STATUS | ENABLED 또는 DISABLED |
| CURRENT_QUEUE_DURATION | 세션이 큐에 대기된 기간 |
| CLIENT_IDENTIFIER | 세션의 클라이언트 식별자 |
| BLOCKING_SESSION_STATUS | 다음 값 중 하나 일 수 있습니다 : VALID, NO HOLDER, GLOBAL, NOT IN WAIT, UNKNOWN |
| BLOCKING_INSTANCE | 차단 세션의 인스턴스 식별자 |
| BLOCK_SESSION | 차단 세션의 세션 식별자 |
| SEQ# | 대기할 때마다 증가하는 시퀀스 번호 |
| EVENT# | 이벤트 번호 |
| EVENT | 세션이 대기 중인 리소스 |
| P1TEXT | 첫 번째 추가 매개변수에 대한 설명 |
| P1 | 첫 번째 추가 매개변수 |
| P1RAW | 첫 번째 추가 매개변수 |
| P2TEXT | 두 번째 추가 매개변수에 대한 설명 |
| P2 | 두 번째 추가 매개변수 |
| P2RAW | 두 번째 추가 매개변수 |
| P3TEXT | 세 번째 추가 매개변수에 대한 설명 |
| P3 | 세 번째 추가 매개변수 |
| P3RAW | 세 번째 추가 매개변수 |
| WAIT_CLASS_ID | 대기 클래스의 식별자 |
| WAIT_CLASS# | 대기 클래스의 번호 |
| WAIT_CLASS | 대기 클래스의 이름 |
| WAIT_TIME | 세션의 마지막 대기 시간 값입니다. 0이면 세션이 현재 대기 중입니다. |
| SECONDS_IN_WAIT | WAIT_TIME > 0이면 SECOND_IN_WAIT는 마지막 대기가 시작된 후의 시간(초)입니다.<br>WAIT_TIME = 0이면 SECONDS_IN_WAIT는 현재 대기에서 경과한 시간(초)입니다. |
| STATE | 0은 대기 중<br>-2는 알 수 없는 시간 대기<br>-1은 짧은 시간 대기 중<br>>0은 알려진 시간 대기 |
| SERVICE_NAME | 세션의 서비스 이름 |
| SQL_TRACE | ENABLED 또는 DISABLED |
| SQL_TRACE_WAITS | TRUE 또는 FALSE |
| SQL_TRACE_BINDS | TRUE 또는 FALSE |

---
**[< 이전](Find_Users.md) / [다음 : Comments in SQL >](Comments.md)**