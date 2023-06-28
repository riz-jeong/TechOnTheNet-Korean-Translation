# Oracle / PLSQL : CURSOR FOR LOOP

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 CURSOR FOR LOOP를 사용하는 방법을 설명합니다.

## 설명
커서 내의 모든 레코드를 가져와서 처리하려는 경우 CURSOR FOR LOOP를 사용할 수 있습니다. 커서 내의 모든 레코드를 가져오면 CURSOR FOR LOOP가 종료됩니다.

## 구문
Oracle/PLSQL에서 CURSOR FOR LOOP의 구문은 다음과 같습니다.
```sql
FOR record_index in cursor_name
LOOP
   {...statements...}
END LOOP;
```
### 매개변수 및 인수
#### **record_index**
- 레코드의 색인입니다.
#### **cursor_name**
- 레코드를 가져오려는 커서의 이름입니다.
#### **statements**
- 각 패스를 실행할 코드 문은 CURSOR FOR LOOP를 통과합니다.

---
## 예제
다음은 CURSOR FOR LOOP를 사용하는 함수의 예입니다.
```sql
CREATE OR REPLACE Function TotalIncome
   ( name_in IN varchar2 )
   RETURN varchar2
IS
   total_val number(6);

   cursor c1 is
     SELECT monthly_income
     FROM employees
     WHERE name = name_in;

BEGIN

   total_val := 0;

   FOR employee_rec in c1
   LOOP
      total_val := total_val + employee_rec.monthly_income;
   END LOOP;

   RETURN total_val;

END;
```
이 예제에서는 c1이라는 커서를 만들었습니다. 커서 c1에서 모든 레코드를 가져온 후 커서 FOR 루프가 종료됩니다.

---
**[< 이전](GOTO.md) / [다음 : Named System Exceptions >](Named_System_Exceptions.md)**