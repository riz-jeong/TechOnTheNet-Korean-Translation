# Oracle / PLSQL : 명명된 시스템 예외

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle/PLSQL에서 명명된 시스템 예외를 사용하는 방법을 설명합니다.

## Oracle에서 명명된 시스템 예외란 무엇인가요?
명명된 시스템 예외는 PL/SQL에서 이름을 지정한 예외입니다. 이러한 예외는 PL/SQL의 STANDARD 패키지에 이름이 지정되며 프로그래머가 정의할 필요가 없습니다.

Oracle에는 이미 다음과 같이 명명된 표준 예외 집합이 있습니다.

| Oracle 예외 이름 | Oracle 오류 | 설명 |
| :-- | :-- | :-- |
| DUP_VAL_ON_INDEX       | ORA-00001   | 고유 인덱스에 의해 제한된 필드에 중복 값을 생성하는 INSERT 또는 UPDATE 문을 실행하려고 했습니다.                                               |
| TIMEOUT_ON_RESOURCE    | ORA-00051   | 리소스를 기다리는 동안 시간이 초과되었습니다.                                                                                                  |
| TRANSACTION_BACKED_OUT | ORA-00061   | 트랜잭션의 원격 부분이 롤백되었습니다.                                                                                                         |
| INVALID_CURSOR         | ORA-01001   | 아직 존재하지 않는 커서를 참조하려고 했습니다. 커서를 열기 전에 커서 가져오기 또는 커서 닫기를 실행했기 때문에 이런 일이 발생했을 수 있습니다. |
| NOT_LOGGED_ON          | ORA-01012   | 로그인하기 전에 Oracle에 대한 호출을 실행하려고 했습니다.                                                                                      |
| LOGIN_DENIED           | ORA-01017   | 잘못된 사용자 이름/비밀번호 조합으로 Oracle에 로그인하려고 했습니다.                                                                           |
| NO_DATA_FOUND          | ORA-01403   | 다음 중 하나를 시도했습니다<br>1. SELECT INTO 문을 실행했지만 행이 반환되지 않았습니다.<br>2. 테이블에서 초기화되지 않은 행을 참조했습니다.<br>3. UTL_FILE 패키지로 파일 끝을 지나서 읽었습니다. |
| TOO_MANY_ROWS       | ORA-01422 | SELECT INTO 문을 실행하려고 했는데 둘 이상의 행이 반환되었습니다.                                        |
| ZERO_DIVIDE         | ORA-01476 | 숫자를 0으로 나누려고 했습니다.                                                                          |
| INVALID_NUMBER      | ORA-01722 | 문자열을 숫자로 변환하는 SQL 문을 실행하려고 했지만 실패했습니다.                                        |
| STORAGE_ERROR       | ORA-06500 | 메모리가 부족하거나 메모리가 손상되었습니다.                                                             |
| PROGRAM_ERROR       | ORA-06501 | 내부 문제가 발생했기 때문에 일반적인 "Oracle 지원팀에 문의" 메시지입니다.                                |
| VALUE_ERROR         | ORA-06502 | 작업을 수행하려고 했는데 숫자 또는 문자 데이터의 변환, 잘림 또는 잘못된 제약 조건에 오류가 발생했습니다. |
| CURSOR_ALREADY_OPEN | ORA-06511 | 이미 열려 있는 커서를 열려고 했습니다. |

## 구문
프로시저와 함수 모두에서 명명된 시스템 예외의 구문을 살펴보겠습니다.

### 프로시저 구문
프로시저에서 명명된 시스템 예외의 구문은 다음과 같습니다.
```sql
CREATE [OR REPLACE] PROCEDURE procedure_name
   [ (parameter [,parameter]) ]
IS
   [declaration_section]

BEGIN
   executable_section

EXCEPTION
   WHEN exception_name1 THEN
      [statements]

   WHEN exception_name2 THEN
      [statements]

   WHEN exception_name_n THEN
      [statements]

   WHEN OTHERS THEN
      [statements]

END [procedure_name];
```

### 함수 구문
함수에서 명명된 시스템 예외의 구문은 다음과 같습니다.
```sql
CREATE [OR REPLACE] FUNCTION function_name
   [ (parameter [,parameter]) ]
   RETURN return_datatype
IS | AS
   [declaration_section]

BEGIN
   executable_section

EXCEPTION
   WHEN exception_name1 THEN
      [statements]

   WHEN exception_name2 THEN
      [statements]

   WHEN exception_name_n THEN
      [statements]

   WHEN OTHERS THEN
      [statements]

END [function_name];
```

---
## 예제
다음은 명명된 시스템 예외를 사용하는 프로시저의 예입니다.
```sql
CREATE OR REPLACE PROCEDURE add_new_supplier
   (supplier_id_in IN NUMBER, supplier_name_in IN VARCHAR2)
IS

BEGIN
   INSERT INTO suppliers (supplier_id, supplier_name )
   VALUES ( supplier_id_in, supplier_name_in );

EXCEPTION
   WHEN DUP_VAL_ON_INDEX THEN
      raise_application_error (-20001,'You have tried to insert a duplicate supplier_id.');

   WHEN OTHERS THEN
      raise_application_error (-20002,'An error has occurred inserting a supplier.');

END;
```
이 예제에서는 DUP_VAL_ON_INDEX라는 명명된 시스템 예외를 트래핑하고 있습니다. 또한 나머지 모든 예외를 트래핑하기 위해 WHEN OTHERS 절을 사용하고 있습니다.

---
**[< 이전](CURSOR_FOR_LOOP.md) / [다음 : Named Programmer-Defined Exception >](Named_Programmer-Defined_Exceptions.md)**