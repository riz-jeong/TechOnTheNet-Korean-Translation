# SQL 튜토리얼
**SQL**은 구조화된 쿼리 언어의 약자로, 거의 모든 데이터베이스 제품에서 지원하는 표준 관계형 언어입니다.  
모든 데이터베이스 전문가는 SQL을 작성하고, 문제를 해결하고, 최적화하는 방법을 알고 있어야 합니다.

이 튜토리얼에서는 데이터를 검색하고 조작하는 방법과 같은 SQL의 기본 사항부터 시작하겠습니다.  
그런 다음 테이블과 뷰를 만드는 방법과 같은 고급 주제로 이동합니다.

이 튜토리얼을 통해 SQL을 작성, 실행 및 최적화하는 데 능숙해질 수 있을 것입니다.

## 전제 조건
이 SQL 튜토리얼을 위한 전제 조건은 없습니다. 이 자습서를 쉽게 이해하고 고급 SQL 주제를 진행하면서 SQL의 기본 개념을 배울 수 있어야 합니다.  

이제 시작하겠습니다!

### **[튜토리얼 시작](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT.md)**

#
혹은 SQL의 항목으로 바로 이동합니다.

## SQL 쿼리 유형

| | |
| :- | :- |
| [SELECT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT.md) | 테이블에서 레코드 검색 |
| [SELECT LIMIT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT_LIMIT.md) | 테이블에서 레코드 검색 및 결과 제한 |
| [SELECT TOP 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SELECT_TOP.md) | 테이블에서 레코드 검색 및 결과 제한 |
| [INSERT 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/INSERT.md) | 테이블에서 레코드 삽입 |
| [UPDATE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/UPDATE.md) | 테이블에서 레코드 갱신 |
| [DELETE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/DELETE.md) | 테이블에서 레코드 삭제 |
| [TRUNCATE TABLE 문](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/TRUNCATE_TABLE.md) | 테이블에서 모든 레코드 삭제(롤백 없음) |
| [UNION 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/UNION.md) | 결과 세트 2개 결합(중복 제거) |
| [UNION ALL 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/UNION_ALL.md) | 결과 세트 2개 결합(중복 포함) |
| [INTERSECT 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/INTERSECT.md) | 두 결과 세트의 교집합 |
| [MINUS 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/MINUS.md) | 하나의 결과 집합에서 다른 결과 집합을 뺀 값 |
| [EXCEPT 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/EXCEPT.md) | 하나의 결과 집합에서 다른 결과 집합을 뺀 값 |

#
## SQL 비교 연산자

| | |
| :- | :- |
| [비교 연산자](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/Comparison_Operators.md) | =, <>, !=, >, < 등과 같은 연산자 |

#
## SQL 조인

| | |
| :- | :- |
| [JOIN 테이블](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/JOINS.md) | 내부 및 외부 조인 |

#
## SQL 별칭

| | |
| :- | :- |
| [ALIASES](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/ALIAS.md) | 열 또는 테이블의 임시 이름 만들기 |

#
## SQL 절

| | |
| :- | :- |
| [DISTINCT 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/DISTINCT.md) | 고유 레코드 검색 |
| [FROM 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/FROM.md) | 테이블 및 조인 정보 나열 |
| [WHERE 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/WHERE.md) | 필터 결과 |
| [ORDER BY 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/ORDER_BY.md) | 쿼리 결과 정렬 |
| [GROUP BY 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/GROUP_BY.md) | 하나 이상의 열로 그룹화 |
| [HAVING 절](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/COHAVINGUNT.md) | 반환된 행의 그룹 제한 |

#
## SQL 함수

| | |
| :- | :- |
| [COUNT 함수](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/COUNT.md) | 표현식의 개수를 반환 |
| [SUM 함수](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/SUM.md) | 표현식의 합을 반환 |
| [MIN 함수](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/MIN.md) | 표현식의 최소값을 반환 |
| [MAX 함수](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/MAX.md) | 표현식의 최대값을 반환 |
| [AVG 함수](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/AVG.md) | 표현식의 평균값을 반환 |

#
## SQL 조건

| | |
| :- | :- |
| [AND 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/AND.md) | 충족해야 할 조건 2개 이상 |
| [OR 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/OR.md) | 조건 중 하나라도 충족되는 경우 |
| [AND & OR](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/AND_OR.md) | AND 및 OR 조건 결합 |
| [LIKE 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/LIKE.md) | WHERE 절에 와일드카드 사용 |
| [IN 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/IN.md) | 여러 OR 조건의 대안 |
| [NOT 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/NOT.md) | 부정 연산 |
| [IS NULL 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/IS_NULL.md) | NULL 값 확인 |
| [IS NOT NULL 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/IS_NOT_NULL.md) | NOT NULL 값 확인 |
| [BETWEEN 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/BETWEEN.md) | 범위 내 검색(포함) |
| [EXISTS 조건](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/EXISTS.md) | 하위 쿼리가 하나 이상의 행을 반환하면 조건충족 |

#
## SQL 테이블 및 뷰

| | |
| :- | :- |
| [CREATE TABLE](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/CREATE_TABLE.md) | 테이블 생성 |
| [CREATE TABLE AS](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/CREATE_TABLE_AS.md) | 다른 테이블의 정의 및 데이터로 테이블 생성 |
| [ALTER TABLE](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/ALTER_TABLE.md) | 테이블의 열 추가, 수정 또는 삭제, 테이블 이름 바꾸기 |
| [DROP TABLE](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/DROP_TABLE.md) | 테이블 삭제 |
| [GLOBAL TEMP 테이블](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/GLOBAL_TEMP.md) | SQL 세션 내에서 고유한 테이블 |
| [LOCAL TEMP 테이블](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/LOCAL_TEMP.md) | 모듈 및 임베디드 SQL 프로그램 내에서 구분되는 테이블 |
| [SQL VIEW](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/VIEW.md) | 가상 테이블(다른 테이블의 보기) |

#
## SQL 키, 제약 조건 및 인덱스

| | |
| :- | :- |
| [기본 키](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/Primary_Keys.md) | 	기본 키 생성 또는 삭제 |
| [인덱스](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/Indexes.md) | 인덱스 생성 및 삭제(성능 튜닝) |

#
## SQL 데이터 형식

| | |
| :- | :- |
| [데이터 형식](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/Data_Types.md) | SQL의 데이터 형식 |

#
## SQL 프로그래밍

| | |
| :- | :- |
| [주석](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/master/SQL/Comments.md) | SQL 문 내에서 주석을 만드는법 |