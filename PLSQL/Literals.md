# Oracle / PLSQL : 리터럴

이 Oracle 튜토리얼에서는 Oracle에서 리터럴(텍스트, 정수 및 숫자)을 사용하는 방법을 예제와 함께 설명합니다.

## 설명
Oracle에서 리터럴은 상수와 동일합니다. 텍스트 리터럴, 정수 리터럴, 숫자, 날짜/시간 리터럴 등 네 가지 유형의 리터럴에 대해 알아보겠습니다.

---
## 문자 리터럴
텍스트 리터럴은 항상 작은따옴표(')로 묶습니다.
```sql
'Hewlett Packard'
'28-MAY-03'
```

---
## 정수 리터럴
정수 리터럴은 최대 38자리까지 가능합니다. 정수 리터럴은 양수 또는 음수일 수 있습니다. 부호를 지정하지 않으면 양수로 가정합니다. 다음은 유효한 정수 리터럴의 몇 가지 예입니다.
```sql
23
+23
-23
```

---
## 숫자 리터럴
숫자 리터럴은 최대 38자리까지 입력할 수 있습니다. 숫자 리터럴은 양수 또는 음수일 수 있습니다. 부호를 지정하지 않으면 양수로 가정합니다. 다음은 유효한 숫자 리터럴의 몇 가지 예입니다.
```sql
25
+25
-25
25e-04
25.607
```

---
## 날짜/시간 리터럴
날짜와 시간은 작은따옴표(')로 묶습니다.
```sql
'2015-04-30'
'2015-04-30 08:13:24'
```
날짜/시간 값을 다룰 때는 TO_DATE 함수를 사용하여 리터럴을 날짜로 변환할 수 있습니다.
```sql
SELECT TO_DATE('2015/04/30', 'yyyy/mm/dd')
FROM dual;
```

이 예제에서는 `'2015/04/30'`이라는 리터럴 값을 날짜로 변환합니다.

---
**[< 이전](Comments.md) / [다음 : Declaring Variables >](Declaring_Variables.md)**