# Oracle / PLSQL : WHILE LOOP

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **WHILE LOOP**를 사용하는 방법을 설명합니다.

## 설명
Oracle에서는 루프 본문을 몇 번 실행할지 확실하지 않고 루프 본문이 한 번도 실행되지 않을 수 있는 경우 WHILE LOOP를 사용합니다.

## 구문
Oracle/PLSQL에서 WHILE LOOP의 구문은 다음과 같습니다.
```sql
WHILE condition
LOOP
   {...statements...}
END LOOP;
```
### 매개변수 및 인수
#### **condition(조건)**
- 조건은 루프를 통과할 때마다 테스트됩니다. 조건이 TRUE로 평가되면 루프 본문이 실행됩니다. 조건이 FALSE로 평가되면 루프가 종료됩니다.
#### **statements**
- 루프를 통과할 때마다 실행할 코드 문입니다.

## 참고
- 루프 본문을 몇 번 실행할지 확실하지 않은 경우 WHILE LOOP 문을 사용할 수 있습니다.
- WHILE 조건은 루프에 들어가기 전에 평가되므로 루프 본문이 한 번도 실행되지 않을 수 있습니다.

---
## 예제
Oracle의 WHILE LOOP 예제를 살펴보겠습니다.
```sql
WHILE monthly_value <= 4000
LOOP
   monthly_value := daily_value * 31;
END LOOP;
```
이 WHILE LOOP 예제에서는 다음과 같이 지정된 대로 monthly_value가 4000을 초과하면 루프가 종료됩니다.
```sql
WHILE monthly_value <= 4000
```
monthly_value <= 4000인 동안 WHILE 루프는 계속됩니다. 그리고 monthly_value가 4000을 초과하면 루프가 종료됩니다.

---
**[< 이전](IF-THEN-ELSE.md) / [다음 : FOR LOOP >](FOR_LOOP.md)**