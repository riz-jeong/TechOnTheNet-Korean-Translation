# Oracle / PLSQL : IF-THEN-ELSE 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **IF-THEN-ELSE 문**을 사용하는 방법을 설명합니다.

## 설명
Oracle에서 IF-THEN-ELSE 문은 조건이 TRUE일 때 코드를 실행하거나 조건이 FALSE로 평가되는 경우 다른 코드를 실행하는 데 사용됩니다.

## 구문
IF-THEN-ELSE 문에는 다양한 구문이 있습니다.

### 구문 (IF-THEN)
Oracle/PLSQL에서 IF-THEN의 구문은 다음과 같습니다.
```sql
IF condition THEN
   {...statements to execute when condition is TRUE...}
END IF;
```
조건이 TRUE일 때만 문을 실행하려는 경우 IF-THEN 구문을 사용합니다.

### 구문 (IF-THEN-ELSE)
Oracle/PLSQL에서 IF-THEN-ELSE의 구문은 다음과 같습니다.
```sql
IF condition THEN
   {...statements to execute when condition is TRUE...}

ELSE
   {...statements to execute when condition is FALSE...}

END IF;
```
조건이 TRUE일 때 한 문 집합을 실행하거나 조건이 FALSE일 때 다른 문 집합을 실행하려는 경우 IF-THEN-ELSE 구문을 사용합니다.

### 구문 (IF-THEN-ELSIF)
Oracle/PLSQL에서 IF-THEN-ELSIF의 구문은 다음과 같습니다.
```sql
IF condition1 THEN
   {...statements to execute when condition1 is TRUE...}

ELSIF condition2 THEN
   {...statements to execute when condition1 is FALSE and condition2 is TRUE...}

END IF;
```
condition1이 TRUE일 때 한 문 집합을 실행하거나 condition2가 TRUE일 때 다른 문 집합을 실행하려는 경우 IF-THEN-ELSIF 구문을 사용할 수 있습니다.

### 구문 (IF-THEN-ELSIF-ELSE)
Oracle/PLSQL에서 IF-THEN-ELSIF-ELSE의 구문은 다음과 같습니다.
```sql
IF condition1 THEN
   {...statements to execute when condition1 is TRUE...}

ELSIF condition2 THEN
   {...statements to execute when condition1 is FALSE and condition2 is TRUE...}

ELSE
   {...statements to execute when both condition1 and condition2 are FALSE...}

END IF;
```
condition1이 TRUE일 때 한 문 집합을 실행하고, condition2가 TRUE일 때 다른 문 집합을 실행하거나, 이전 조건이 모두 FALSE일 때 다른 문 집합을 실행하려는 경우 IF-THEN-ELSIF-ELSE 구문을 사용할 수 있습니다.

## 참고
- 조건이 TRUE로 확인되면 IF-THEN-ELSE 문은 해당 코드를 실행하고 조건을 더 이상 평가하지 않습니다.
- 조건이 충족되지 않으면 IF-THEN-ELSE 문의 ELSE 부분이 실행됩니다.
- ELSIF 및 ELSE 부분은 선택 사항이라는 점에 유의하세요.

---
## 예제
다음은 Oracle 함수에서 IF-THEN-ELSE 문을 사용하는 예입니다.
```sql
CREATE OR REPLACE Function IncomeLevel
   ( name_in IN varchar2 )
   RETURN varchar2
IS
   monthly_value number(6);
   ILevel varchar2(20);

   cursor c1 is
     SELECT monthly_income
     FROM employees
     WHERE name = name_in;

BEGIN

   open c1;
   fetch c1 into monthly_value;
   close c1;

   IF monthly_value <= 4000 THEN
      ILevel := 'Low Income';

   ELSIF monthly_value > 4000 and monthly_value <= 7000 THEN
      ILevel := 'Avg Income';

   ELSIF monthly_value > 7000 and monthly_value <= 15000 THEN
      ILevel := 'Moderate Income';

   ELSE
      ILevel := 'High Income';

   END IF;

   RETURN ILevel;

END;
```
이 IF-THEN-ELSE 문 예제에서는 IncomeLevel이라는 함수를 만들었습니다. 이 함수에는 name_in이라는 매개변수가 하나 있으며 varchar2를 반환합니다. 이 함수는 직원의 이름을 기준으로 소득 수준을 반환합니다.

---
**[< 이전](Procedures.md) / [다음 : WHILE LOOP >](WHILE_LOOP.md)**