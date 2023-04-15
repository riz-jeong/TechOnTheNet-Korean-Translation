# Oracle 튜토리얼
**Oracle**은 Oracle에서 개발한 관계형 데이터베이스 기술입니다.

**PLSQL**은 "SQL에 대한 절차적 언어 확장"의 약자로, Oracle에서 사용되는 SQL의 확장입니다. PLSQL은 SQL 언어와 밀접하게 통합되어 있지만, SQL에 기본이 아닌 프로그래밍 구성을 추가합니다.

이 튜토리얼에서는 데이터를 검색하고 조작하는 방법과 같은 Oracle의 기본 사항부터 시작합니다. 그런 다음 테이블, 함수, 프로시저, 트리거, 테이블 스페이스 및 스키마를 만드는 방법과 같은 고급 주제로 이동합니다. 마지막으로 오라클 고유의 함수에 대한 검토로 마무리하겠습니다.

이 튜토리얼을 통해 Oracle 및 PLSQL에 능숙해질 수 있을 것입니다.

## 전제 조건
이 Oracle 튜토리얼에는 사전 요구 사항이 없습니다. 이 튜토리얼을 쉽게 이해하고 고급 주제로 진행하면서 Oracle의 기본 개념을 배울 수 있어야 합니다.

이제 시작하겠습니다!

**[튜토리얼 시작](SELECT.md)**

---
혹은 Oracle/PLSQL의 항목으로 바로 이동합니다.

## Oracle/PLSQL 함수

| | |
| :- | :- |
| [함수 - 알파벳순](Functions_Index_Alpha.md) | 알파벳순으로 나열된 Oracle/PLSQL 함수 |
| [함수 - 카테고리](Functions_Index.md) | 카테고리별로 나열된 Oracle/PLSQL 함수 |

---
## Oracle 키, 제약 조건 및 인덱스

| | |
| :- | :- |
| [기본 키](Primary_Keys.md) | 	기본 키 생성, 변경, 삭제, 활성화 및 비활성화 |
| [외래 키](Foreign_Key.md) | 	외래 키 생성, 삭제, 활성화 및 비활성화 |
| [Unique 제약 조건](Unique.md) | Unique 제약 조건 생성, 변경, 삭제, 활성화 및 비활성화 |
| [Check 제약 조건](Check.md) | Check 제약 조건 생성, 변경, 삭제, 활성화 및 비활성화 |
| [인덱스](Indexes.md) | 인덱스 생성, 이름 변경 및 삭제(성능 튜닝) |

---
## Oracle 권한, 동의어, 역할 및 암호

| | |
| :- | :- |
| [Grant/Revoke 권한](Grant_Revoke.md) | 권한 부여 또는 취소 |
| [Synonyms](Synonyms.md) | 시노님 생성, 바꾸기 및 삭제 |
| [역할](Roles.md) | 권한 집합 |
| [비밀번호 변경](Password.md) | 사용자 비밀번호 변경 |

---
## Oracle 데이터베이스 관리
| | |
| :- | :- |
| [함수](Functions.md) | 함수 생성 및 삭제 |
| [프로시저](Procedures.md) | 프로시저 생성 및 삭제 |
| [트리거]() | 트리거 생성, 삭제, 활성화 및 비활성화 |
| [커서]() | 저장된 프로그램 내에서 커서 만들기 |
| [리터럴(상수)]() | 텍스트, 정수 및 숫자 리터럴 만들기 |
| [변수 선언하기]() | 변수 및 상수 선언하기 |
| [예외 처리]() | 코드에서 예외 처리 |
| [루프 및 조건문]() | FOR 루프, WHILE 루프, IF-THEN-ELSE 등 |
| [시퀀스(자동 번호)]() | 시퀀스 생성 및 삭제 |
| [트랜잭션]() | 커밋 및 롤백 |
| [SQL 내 주석]() | SQL 문 내에서 주석을 만드는 방법 |

---
## Oracle 쿼리 유형

| | |
| :- | :- |
| [SELECT 문](SELECT.md) | 테이블에서 레코드 검색 |
| [SELECT LIMIT 문](SELECT_LIMIT.md) | 테이블에서 레코드 검색 및 결과 제한 |
| [SELECT TOP 문](SELECT_TOP.md) | 테이블에서 레코드 검색 및 결과 제한 |
| [INSERT 문](INSERT.md) | 테이블에서 레코드 삽입 |
| [UPDATE 문](UPDATE.md) | 테이블에서 레코드 갱신 |
| [DELETE 문](DELETE.md) | 테이블에서 레코드 삭제 |
| [TRUNCATE TABLE 문](TRUNCATE.md) | 테이블에서 모든 레코드 삭제(롤백 없음) |
| [UNION 연산자](UNION.md) | 결과 집합 2개 결합(중복 제거) |
| [UNION ALL 연산자](UNION_ALL.md) | 결과 집합 2개 결합(중복 포함) |
| [INTERSECT 연산자](INTERSECT.md) | 두 결과 집합의 교집합 |
| [MINUS 연산자](MINUS.md) | 하나의 결과 집합에서 다른 결과 집합을 뺀 값 |
| [EXCEPT 연산자](EXCEPT.md) | 하나의 결과 집합에서 다른 결과 집합을 뺀 값 |

---
## Oracle 비교 연산자

| | |
| :- | :- |
| [비교 연산자](Comparison_Operators.md) | =, <>, !=, >, < 등과 같은 연산자 |

---
## Oracle 조인

| | |
| :- | :- |
| [JOIN 테이블](JOINS.md) | 내부 및 외부 조인 |

---
## Oracle 별칭

| | |
| :- | :- |
| [ALIASES](ALIAS.md) | 열 또는 테이블의 임시 이름 만들기 |

---
## Oracle 절

| | |
| :- | :- |
| [DISTINCT 절](DISTINCT.md) | 고유 레코드 검색 |
| [FROM 절](FROM.md) | 테이블 및 조인 정보 나열 |
| [WHERE 절](WHERE.md) | 필터 결과 |
| [ORDER BY 절](ORDER_BY.md) | 쿼리 결과 정렬 |
| [GROUP BY 절](GROUP_BY.md) | 하나 이상의 열로 그룹화 |
| [HAVING 절](COHAVINGUNT.md) | 반환된 행의 그룹 제한 |

---
## Oracle 조건

| | |
| :- | :- |
| [AND 조건](AND.md) | 충족해야 할 조건 2개 이상 |
| [OR 조건](OR.md) | 조건 중 하나라도 충족되는 경우 |
| [AND & OR](AND_OR.md) | AND 및 OR 조건 결합 |
| [LIKE 조건](LIKE.md) | WHERE 절에 와일드카드 사용 |
| [IN 조건](IN.md) | 여러 OR 조건의 대안 |
| [NOT 조건](NOT.md) | 부정 연산 |
| [IS NULL 조건](IS_NULL.md) | NULL 값 확인 |
| [IS NOT NULL 조건](IS_NOT_NULL.md) | NOT NULL 값 확인 |
| [BETWEEN 조건](BETWEEN.md) | 범위 내 검색(포함) |
| [EXISTS 조건](EXISTS.md) | 하위 쿼리가 하나 이상의 행을 반환하면 조건충족 |

---
## Oracle 테이블 및 뷰

| | |
| :- | :- |
| [CREATE TABLE](CREATE_TABLE.md) | 테이블 생성 |
| [CREATE TABLE AS](CREATE_TABLE_AS.md) | 다른 테이블의 정의 및 데이터로 테이블 생성 |
| [ALTER TABLE](ALTER_TABLE.md) | 테이블의 열 추가, 수정 또는 삭제, 테이블 이름 바꾸기 |
| [DROP TABLE](DROP_TABLE.md) | 테이블 삭제 |
| [GLOBAL TEMP 테이블](GLOBAL_TEMP.md) | SQL 세션 내에서 고유한 테이블 |
| [LOCAL TEMP 테이블](LOCAL_TEMP.md) | 모듈 및 임베디드 SQL 프로그램 내에서 구분되는 테이블 |
| [SQL VIEW](VIEW.md) | 가상 테이블(다른 테이블의 보기) |

---
## Oracle 데이터 형식

| | |
| :- | :- |
| [데이터 형식](Data_Types.md) | SQL의 데이터 형식 |

---
## Oracle 프로그래밍

| | |
| :- | :- |
| [주석](Comments.md) | SQL 문 내에서 주석을 만드는법 |