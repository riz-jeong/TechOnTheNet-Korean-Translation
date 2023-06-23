# Oracle / PLSQL : GOTO 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **GOTO 문**을 사용하는 방법을 설명합니다.

## 설명
GOTO 문은 코드가 GOTO 문 뒤에 있는 레이블로 분기되도록 합니다.

## 구문
Oracle/PLSQL의 GOTO 문 구문은 GOTO 문과 레이블 선언의 두 부분으로 구성됩니다.

### GOTO 문
GOTO 문은 GOTO 키워드와 label_name으로 구성됩니다.
```sql
GOTO label_name;
```

### 레이블 선언
레이블 선언은 << >>로 캡슐화된 label_name과 그 뒤에 실행할 하나 이상의 문으로 구성됩니다.
```sql
<<label_name>>
 {...statements...}
```

## 참고
- label_name은 코드 범위 내에서 고유해야 합니다.
- 레이블 선언 뒤에 실행할 문이 하나 이상 있어야 합니다.

---
## 예제
GOTO 문을 사용하는 Oracle 예제를 살펴보겠습니다.
```sql
CREATE OR REPLACE Function FindCourse
   ( name_in IN varchar2 )
   RETURN number
IS
   cnumber number;

   CURSOR c1
   IS
     SELECT MAX(course_number)
     FROM courses_tbl
     WHERE course_name = name_in;

BEGIN

   open c1;
   fetch c1 into cnumber;

   IF c1%notfound then
      GOTO default_number;

   ELSE
      GOTO increment_number;
   END IF;

<<default_number>>
   cnumber := 0;

<<increment_number>>
   cnumber := cnumber + 1;

   close c1;

RETURN cnumber;

END;
```
이 GOTO 예제에서는 두 개의 GOTO 문을 만들었습니다. 첫 번째 문은 default_number, 두 번째 문은 increment_number라고 합니다.

---
**[< 이전](REPEAT_UNTIL_LOOP.md) / [다음 : CURSOR FOR LOOP >](CURSOR_FOR_LOOP.md)**