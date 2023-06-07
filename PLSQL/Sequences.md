# Oracle / PLSQL : 시퀀스 (자동 번호)

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 시퀀스를 만들고 삭제하는 방법을 설명합니다.

## 설명
Oracle에서는 시퀀스를 사용하여 자동 번호 필드를 만들 수 있습니다. 시퀀스는 숫자 시퀀스를 생성하는 데 사용되는 Oracle의 객체입니다. 기본 키 역할을 할 고유 번호를 생성해야 할 때 유용할 수 있습니다.

---
## 시퀀스 생성
Oracle에서 자동 번호 필드를 처리하기 위해 시퀀스를 생성할 수 있습니다.

### 구문
Oracle에서 시퀀스를 생성하는 구문은 다음과 같습니다.

```sql
CREATE SEQUENCE sequence_name
  MINVALUE value
  MAXVALUE value
  START WITH value
  INCREMENT BY value
  CACHE value;
```

#### **sequence_name**
- 생성하려는 시퀀스의 이름입니다.

### 예제
Oracle에서 시퀀스를 만드는 방법의 예를 살펴보겠습니다.

```sql
CREATE SEQUENCE supplier_seq
  MINVALUE 1
  MAXVALUE 999999999999999999999999999
  START WITH 1
  INCREMENT BY 1
  CACHE 20;
```

이렇게 하면 supplier_seq라는 시퀀스 객체가 생성됩니다. 이 객체가 사용할 첫 번째 시퀀스 번호는 1이고 이후의 각 숫자는 1씩 증가합니다(2,3,4,...). 성능을 위해 최대 20개의 값을 캐시합니다.

MAXVALUE 옵션을 생략하면 시퀀스가 자동으로 기본값으로 설정됩니다.

```sql
MAXVALUE 999999999999999999999999999
```

다음과 같이 CREATE SEQUENCE 명령을 단순화할 수 있습니다.

```sql
CREATE SEQUENCE supplier_seq
  MINVALUE 1
  START WITH 1
  INCREMENT BY 1
  CACHE 20;
```

이제 자동 번호 필드를 시뮬레이션하기 위해 시퀀스 객체를 만들었으므로 이 시퀀스 객체에서 값을 검색하는 방법을 살펴보겠습니다. 시퀀스 순서에서 다음 값을 검색하려면 nextval을 사용해야 합니다.

```sql
supplier_seq.NEXTVAL;
```

이것은 supplier_seq에서 다음 값을 검색합니다. nextval 문은 SQL 문에서 사용해야 합니다.

```sql
INSERT INTO suppliers
(supplier_id, supplier_name)
VALUES
(supplier_seq.NEXTVAL, 'Kraft Foods');
```

이 INSERT 문은 suppliers 테이블에 새 레코드를 삽입합니다. supplier_id 필드에는 supplier_seq 시퀀스에서 다음 번호가 할당됩니다. supplier_name 필드는 Kraft Foods로 설정됩니다.

---
## 시퀀스 삭제
Oracle에서 시퀀스를 생성한 후에는 데이터베이스에서 시퀀스를 제거해야 할 수도 있습니다.

### 구문
Oracle에서 시퀀스를 삭제하는 구문은 다음과 같습니다.

```sql
DROP SEQUENCE sequence_name;
```

#### **sequence_name**
- 삭제하려는 시퀀스의 이름입니다.

### 예제
Oracle에서 시퀀스를 삭제하는 방법의 예를 살펴보겠습니다.

```sql
DROP SEQUENCE supplier_seq;
```

이 예제에서는 supplier_seq라는 시퀀스를 삭제합니다.

---
## 자주 묻는 질문
시퀀스에 대한 일반적인 질문 중 하나는 다음과 같습니다.

- 질문 : 시퀀스를 생성할 때 캐시 및 노캐시 옵션은 무엇을 의미하나요? 예를 들어 캐시가 20인 시퀀스를 다음과 같이 만들 수 있습니다.

```sql
CREATE SEQUENCE supplier_seq
  MINVALUE 1
  START WITH 1
  INCREMENT BY 1
  CACHE 20;
```

또는 노캐시 옵션을 사용하여 동일한 시퀀스를 만들 수도 있습니다.

```sql
CREATE SEQUENCE supplier_seq
  MINVALUE 1
  START WITH 1
  INCREMENT BY 1
  NOCACHE;
```

- 답변 : 시퀀스와 관련하여 캐시 옵션은 빠른 액세스를 위해 메모리에 저장할 시퀀스 값의 수를 지정합니다.

캐시를 사용하여 시퀀스를 생성할 때의 단점은 시스템 장애가 발생하면 사용되지 않은 캐시된 모든 시퀀스 값이 "손실"된다는 것입니다. 이로 인해 할당된 시퀀스 값에 "갭"이 발생합니다. 시스템이 다시 가동되면 Oracle은 소위 "손실된" 시퀀스 값을 무시하고 시퀀스에서 중단된 지점부터 새로운 번호를 캐시합니다.

>팁 : 손실된 시퀀스 값을 복구하려면 언제든지 ALTER SEQUENCE 명령을 실행하여 카운터를 올바른 값으로 재설정할 수 있습니다.

노캐시는 시퀀스 값이 메모리에 저장되지 않음을 의미합니다. 이 옵션을 사용하면 성능이 약간 저하될 수 있지만 할당된 시퀀스 값에 공백이 발생하지 않습니다.

---

- 질문 : Oracle 시퀀스에서 LASTVALUE 값을 설정하려면 어떻게 해야 하나요?

- 답변 : ALTER SEQUENCE 명령을 실행하여 Oracle 시퀀스에 대한 LASTVALUE를 변경할 수 있습니다.

Oracle 시퀀스에서 사용한 마지막 값이 100이고 다음 값으로 225를 제공하도록 시퀀스를 재설정하려는 경우입니다. 다음 명령을 실행합니다.

```sql
ALTER SEQUENCE seq_name
INCREMENT BY 124;

SELECT seq_name.nextval FROM dual;

ALTER SEQUENCE seq_name
INCREMENT BY 1;
```

이제 시퀀스에서 제공할 다음 값은 225가 됩니다.

---
**[< 이전](Declaring_Variables.md) / [다음 : Functions >](Functions.md)**