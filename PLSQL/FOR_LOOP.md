# Oracle / PLSQL : FOR LOOP
이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 **FOR LOOP**를 사용하는 방법을 설명합니다.

## 설명
Oracle에서 FOR LOOP를 사용하면 정해진 횟수 동안 코드를 반복적으로 실행할 수 있습니다.

## 구문
Oracle/PLSQL에서 FOR 루프의 구문은 다음과 같습니다.
```sql
FOR loop_counter IN [REVERSE] lowest_number..highest_number
LOOP
   {...statements...}
END LOOP;
```
### 매개변수 및 인수
#### **loop_counter**
- 루프 카운터 변수입니다.
#### **REVERSE**
- 선택 사항입니다. 지정하면 루프 카운터가 역으로 카운트됩니다.
#### **lowest_number**
- loop_counter의 시작 값입니다.
#### **highest_number**
- loop_counter의 종료 값입니다.
#### **statements**
- 루프를 통과할 때마다 실행할 코드 문입니다.

## 참고
- 루프 본문을 정해진 횟수만큼 실행하려는 경우 FOR LOOP를 사용합니다.
- REVERSE를 지정하면 가장 높은 번호가 loop_counter의 시작 값이 되고 가장 낮은 번호가 loop_counter의 끝 값이 됩니다.

---
## 예제
Oracle에서 FOR LOOP를 사용하는 방법의 예를 살펴보겠습니다.
```sql
FOR Lcntr IN 1..20
LOOP
   LCalc := Lcntr * 31;
END LOOP;
```
이 FOR LOOP 예제는 20번 반복됩니다. Lcntr이라는 카운터는 1에서 시작하여 20에서 끝납니다.

REVERSE 수정자를 사용하여 FOR LOOP를 역순으로 실행할 수 있습니다.
```sql
FOR Lcntr IN REVERSE 1..15
LOOP
   LCalc := Lcntr * 31;
END LOOP;
```
이 FOR LOOP 예제는 15번 반복됩니다. 그러나 REVERSE가 지정되었으므로 Lcntr이라는 카운터는 15에서 시작하여 1에서 종료됩니다(거꾸로 반복).

---
**[< 이전](WHILE_LOOP.md) / [다음 : EXIT >](EXIT.md)**