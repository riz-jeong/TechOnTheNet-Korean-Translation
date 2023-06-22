# Oracle / PLSQL : LOOP 문

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **LOOP 문**을 사용하는 방법을 설명합니다.

## 설명
Oracle에서는 반복문을 몇 번 실행할지 확실하지 않고 반복문을 적어도 한 번은 실행해야 할 때 LOOP 문을 사용합니다.

## 구문
Oracle/PLSQL에서 LOOP 문의 구문은 다음과 같습니다.
```sql
LOOP
   {...statements...}
END LOOP;
```
### 매개변수 및 인수
#### **statements**
- 루프를 통과할 때마다 실행할 코드 문입니다.

## 참고
- 반복문을 몇 번 실행할지 확실하지 않은 경우 LOOP 문을 사용합니다.
- LOOP 문은 EXIT 문으로 종료하거나 TRUE로 평가되는 EXIT WHEN 문을 만나면 종료할 수 있습니다.

---
## 예제
Oracle의 LOOP 예제를 살펴보겠습니다.
```sql
LOOP
   monthly_value := daily_value * 31;
   EXIT WHEN monthly_value > 4000;
END LOOP;
```
이 LOOP 예제에서는 monthly_value가 4000을 초과하면 LOOP가 종료됩니다.

---
**[< 이전](EXIT.md) / [다음 : REPEAT UNTIL LOOP >](REPEAT_UNTIL_LOOP.md)**