# Oracle / PLSQL : EXIT 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **EXIT 문**을 사용하는 방법을 설명합니다.

## 설명
Oracle에서 EXIT 문은 LOOP 문을 종료하는 데 가장 일반적으로 사용됩니다.

## 구문
Oracle/PLSQL에서 EXIT 문의 구문은 다음과 같습니다.
```sql
EXIT [WHEN boolean_condition];
```
### 매개변수 및 인수
#### **boolean_condition**
- 선택 사항입니다. 루프를 종료하는 조건입니다.

---
## 예제
Oracle/PLSQL의 EXIT 예제를 살펴보겠습니다.
```sql
LOOP
   monthly_value := daily_value * 31;
   EXIT WHEN monthly_value > 4000;
END LOOP;
```
이 예제에서는 monthly_value이 4000을 초과하면 LOOP가 종료됩니다.

---
**[< 이전](FOR_LOOP.md) / [다음 : LOOP >](LOOP.md)**