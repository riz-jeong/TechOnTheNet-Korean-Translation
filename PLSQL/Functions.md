# Oracle / PLSQL : 함수

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle/PLSQL에서 함수를 만들고 제거하는 방법을 설명합니다.

---
## 함수 생성
다른 언어에서와 마찬가지로 Oracle에서도 자신만의 함수를 만들 수 있습니다.

### 구문
Oracle에서 함수를 만드는 구문은 다음과 같습니다.
```sql
CREATE [OR REPLACE] FUNCTION function_name
   [ (parameter [,parameter]) ]

   RETURN return_datatype

IS | AS

   [declaration_section]

BEGIN
   executable_section

[EXCEPTION
   exception_section]

END [function_name];
```
프로시저나 함수를 만들 때 매개변수를 정의할 수 있습니다. 선언할 수 있는 매개변수에는 세 가지 유형이 있습니다.
1. **IN** - 프로시저 또는 함수에서 매개 변수를 참조할 수 있습니다. 프로시저 또는 함수에서 매개변수 값을 덮어쓸 수 없습니다.
2. **OUT** - 프로시저나 함수에서 매개 변수를 참조할 수 없지만 프로시저나 함수에서 매개 변수 값을 덮어쓸 수 있습니다.
3. **IN OUT** - 프로시저 또는 함수에서 매개변수를 참조할 수 있으며 프로시저 또는 함수에서 매개변수 값을 덮어쓸 수 있습니다.

### 예제
Oracle에서 함수를 만드는 방법의 예를 살펴보겠습니다.
```sql
CREATE OR REPLACE Function FindCourse
   ( name_in IN varchar2 )
   RETURN number
IS
   cnumber number;

   cursor c1 is
   SELECT course_number
     FROM courses_tbl
     WHERE course_name = name_in;

BEGIN

   open c1;
   fetch c1 into cnumber;

   if c1%notfound then
      cnumber := 9999;
   end if;

   close c1;

RETURN cnumber;

EXCEPTION
WHEN OTHERS THEN
   raise_application_error(-20001,'An error was encountered - '||SQLCODE||' -ERROR- '||SQLERRM);
END;
```
이 함수는 FindCourse라고 합니다. 이 함수에는 name_in이라는 매개변수가 하나 있으며 숫자를 반환합니다. 이 함수는 코스 이름을 기준으로 일치하는 항목을 찾으면 코스 번호를 반환합니다. 그렇지 않으면 99999를 반환합니다.

그런 다음 다음과 같이 SQL 문에서 새 함수를 참조할 수 있습니다.
```sql
SELECT course_name, FindCourse(course_name) AS course_id
FROM courses
WHERE subject = 'Mathematics';
```

---
## 함수 제거
Oracle에서 함수를 생성한 후에는 데이터베이스에서 함수를 제거해야 할 수도 있습니다.

### 구문
Oracle에서 함수를 삭제하는 구문은 다음과 같습니다.
```sql
DROP FUNCTION function_name;
```
#### **function_name**
- 삭제하려는 함수의 이름입니다.

### 예제
Oracle에서 함수를 삭제하는 방법의 예를 살펴보겠습니다.
```sql
DROP FUNCTION FindCourse;
```
이 예제에서는 FindCourse 함수를 삭제합니다.

---
**[< 이전](Sequences.md) / [다음 : Procedures >](Procedures.md)**