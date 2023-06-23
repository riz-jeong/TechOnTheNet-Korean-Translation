# Oracle / PLSQL : REPEAT UNTIL LOOP

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **REPEAT UNTIL LOOP**를 사용하는 방법을 설명합니다.

## 설명
Oracle에는 REPEAT UNTIL LOOP가 없지만 LOOP 문을 사용하여 에뮬레이션할 수 있습니다.

## 구문
Oracle/PLSQL에서 REPEAT UNTIL LOOP를 에뮬레이트하는 구문은 다음과 같습니다.
```sql
LOOP

   {...statements...}

   EXIT [ WHEN boolean_condition ];

END LOOP;
```
### 매개변수 및 인수
#### **statements**
- 루프를 통과할 때마다 실행할 코드 문입니다.
#### **boolean_condition**
- 선택 사항입니다. 루프를 종료하는 조건입니다.

## 참고
- 반복문을 몇 번 실행할지 모르는 경우 에뮬레이트된 REPEAT UNTIL LOOP를 사용할 수 있습니다.
- REPEAT UNTIL LOOP는 특정 조건이 충족되면 종료됩니다.

---
## 예제
Oracle/PLSQL에서 REPEAT UNTIL LOOP를 에뮬레이트하는 방법의 예를 살펴보겠습니다.
```sql
LOOP
   monthly_value := daily_value * 31;
   EXIT WHEN monthly_value > 4000;
END LOOP;
```
이 예제에서는 monthly_value가 4000보다 클 때까지 루프를 반복하고 싶으므로 EXIT WHEN 문을 사용합니다.
```sql
EXIT WHEN monthly_value > 4000;
```
이제 monthly_value이 4000을 초과할 때까지 LOOP가 반복됩니다.

---
**[< 이전](LOOP.md) / [다음 : GOTO >](GOTO.md)**