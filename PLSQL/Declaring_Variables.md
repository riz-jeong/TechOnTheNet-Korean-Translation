# Oracle / PLSQL : 변수 선언

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle/PLSQL에서 변수를 선언하는 방법을 설명합니다.

## Oracle에서 변수는 무엇인가요?
Oracle/PLSQL에서 변수는 프로그래머가 코드를 실행하는 동안 데이터를 임시로 저장할 수 있도록 해줍니다.

## 구문
Oracle에서 변수를 선언하는 구문은 다음과 같습니다.
```sql
variable_name [CONSTANT] datatype [NOT NULL] [:= | DEFAULT initial_value]
```
### 매개변수 및 인수
#### **variable_name**
- 변수에 할당할 이름입니다.
#### **CONSTANT**
- 선택 사항입니다. 지정하면 변수 값은 상수이며 변경할 수 없습니다.
#### **datatype**
- 변수에 할당할 데이터 형식입니다.

---
## 예제 - 변수 선언하기
다음은 Oracle에서 LDescription이라는 변수를 선언하는 방법의 예입니다.
```sql
LDescription varchar2(40);
```
그런 다음 나중에 다음과 같이 LDescription 변수의 값을 설정하거나 변경할 수 있습니다.
```sql
LDescription := 'techonthenet.com Example';
```

---
## 예제 - 상수가 아닌 초기값으로 변수 선언하기
다음은 Oracle에서 변수를 선언하고 초기 값을 지정하는 방법의 예입니다. 이는 나중에 변수 값을 변경할 수 있다는 점에서 상수와 다릅니다.
```sql
LType varchar2(40) := 'techonthenet.com Example';
```
나중에 다음과 같이 변수 값을 변경할 수 있습니다.
```sql
LType := 'My value has changed';
```

---
## 예제 - 상수 선언하기
다음은 Oracle에서 상수를 선언하는 방법의 예입니다. 상수의 값은 변경할 수 없습니다.
```sql
LTotal CONSTANT numeric(8,1) := 8363934.1;
```

---
**[< 이전](Literals.md) / [다음 : Sequences >](Sequences.md)**