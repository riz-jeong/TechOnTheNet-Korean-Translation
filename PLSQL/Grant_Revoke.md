# Oracle / PLSQL : 권한 부여/제거

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle에서 권한을 부여하고 제거하는 방법을 설명합니다.

## 설명
Oracle에서 다양한 데이터베이스 개체에 대한 권한을 부여하고 제거할 수 있습니다. 먼저 테이블에 대한 권한을 부여하고 제거하는 방법을 살펴본 다음 Oracle의 함수 및 프로시저에 대한 권한을 부여하고 제거하는 방법을 살펴보겠습니다.

---
## 테이블에 대한 권한 부여
사용자에게 테이블에 다양한 권한을 부여할 수 있습니다. 이러한 권한은 SELECT, INSERT, UPDATE, DELETE, REFERENCES, ALTER, INDEX 또는 ALL의 모든 조합이 될 수 있습니다.

### 구문
Oracle에서 테이블에 권한을 부여하는 구문은 다음과 같습니다.
```sql
GRANT privileges ON object TO user;
```
#### **privileges**
- 할당할 권한입니다. 다음 값 중 하나가 될 수 있습니다.

| 권한       | 설명                                                             |
| :--------- | :--------------------------------------------------------------- |
| SELECT     | 테이블에서 SELECT 문을 수행할 수 있는 권한입니다.                |
| INSERT     | 테이블에서 INSERT 문을 수행할 수 있는 권한입니다.                |
| UPDATE     | 테이블에서 UPDATE 문을 수행할 수 있습니다.                       |
| DELETE     | 테이블에서 DELETE 문을 수행할 수 있습니다.                       |
| REFERENCES | 테이블을 참조하는 제약 조건을 생성하는 기능입니다.               |
| ALTER      | 테이블 정의를 변경하기 위해 ALTER TABLE 문을 수행하는 기능.      |
| INDEX      | CREATE INDEX 문을 사용하여 테이블에 인덱스를 생성할 수 있습니다. |
| ALL        | 테이블에 대한 모든 권한.                                         |

#### **object**
- 권한을 부여할 데이터베이스 오브젝트의 이름입니다. 테이블에 대한 권한을 부여하는 경우 테이블 이름이 됩니다.
#### **user**
- 이 권한을 부여받을 사용자의 이름입니다.

### 예제
Oracle에서 테이블에 권한을 부여하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

예를 들어 suppliers라는 테이블에 대한 SELECT, INSERT, UPDATE 및 DELETE 권한을 smithj라는 사용자 이름에 부여하려는 경우 다음 GRANT 문을 실행합니다.
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON suppliers TO smithj;
```
ALL 키워드를 사용하여 smithj라는 사용자에 대해 모든 권한을 부여하도록 지정할 수도 있습니다.
```sql
GRANT ALL ON suppliers TO smithj;
```
모든 사용자에게 테이블에 대한 SELECT 액세스 권한만 부여하려는 경우 공개 키워드로 권한을 부여할 수 있습니다.
```sql
GRANT SELECT ON suppliers TO public;
```

---
## 테이블에 대한 권한 제거
권한을 부여한 후에는 이러한 권한의 일부 또는 전부를 제거해야 할 수 있습니다. 이렇게 하려면 제거 명령을 실행하면 됩니다. SELECT, INSERT, UPDATE, DELETE, REFERENCES, ALTER, INDEX 또는 ALL의 모든 조합을 제거할 수 있습니다.

### 구문
Oracle에서 테이블에 대한 권한을 제거하는 구문은 다음과 같습니다.
```sql
REVOKE privileges ON object FROM user;
```

#### **privileges**
- 해지할 권한입니다. 다음 값 중 하나를 사용할 수 있습니다.

| 권한       | 설명                                                             |
| :--------- | :--------------------------------------------------------------- |
| SELECT     | 테이블에서 SELECT 문을 수행할 수 있는 권한입니다.                |
| INSERT     | 테이블에서 INSERT 문을 수행할 수 있는 권한입니다.                |
| UPDATE     | 테이블에서 UPDATE 문을 수행할 수 있습니다.                       |
| DELETE     | 테이블에서 DELETE 문을 수행할 수 있습니다.                       |
| REFERENCES | 테이블을 참조하는 제약 조건을 생성하는 기능입니다.               |
| ALTER      | 테이블 정의를 변경하기 위해 ALTER TABLE 문을 수행하는 기능.      |
| INDEX      | CREATE INDEX 문을 사용하여 테이블에 인덱스를 생성할 수 있습니다. |
| ALL        | 테이블에 대한 모든 권한.                                         |

#### **object**
- 권한을 제거할 데이터베이스 오브젝트의 이름입니다. 테이블에 대한 권한을 제거하는 경우 테이블 이름이 됩니다.
#### **사용자**
- 이 권한을 제거할 사용자의 이름입니다.

### 예제
Oracle에서 테이블에 대한 권한을 해지하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

예를 들어, anderson이라는 사용자로부터 suppliers라는 테이블에 대한 DELETE 권한을 해지하려는 경우 다음 REVOKE 문을 실행합니다.
```sql
REVOKE DELETE ON suppliers FROM anderson;
```
anderson이라는 사용자의 테이블에 대한 모든 권한을 해지하려면 다음과 같이 ALL 키워드를 사용할 수 있습니다:
```sql
REVOKE ALL ON suppliers FROM anderson;
```
suppliers 테이블에 대해 공개(모든 사용자)에게 ALL 권한을 부여한 경우 이러한 권한을 제거하려면 다음 REVOKE 문을 실행하면 됩니다.
```sql
REVOKE ALL ON suppliers FROM public;
```

---
## 함수/프로시저에 대한 권한 부여
함수/프로시저를 다룰 때 사용자에게 이러한 함수/프로시저를 실행할 수 있는 권한을 부여할 수 있습니다.

### 구문
Oracle에서 함수/프로시저에 EXECUTE 권한을 부여하는 구문은 다음과 같습니다.
```sql
GRANT EXECUTE ON object TO user;
```
#### **EXECUTE**
- 함수/프로시저를 컴파일할 수 있는 기능입니다. 함수/프로시저를 직접 실행할 수 있는 기능입니다.
#### **object**
- 권한을 부여할 데이터베이스 오브젝트의 이름입니다. 함수/프로시저에 EXECUTE 권한을 부여하는 경우 함수 이름 또는 프로시저 이름이 됩니다.
#### **user**
- EXECUTE 권한을 부여받을 사용자의 이름입니다.

### 예제
Oracle에서 함수/프로시저에 EXECUTE 권한을 부여하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

예를 들어 Find_Value라는 함수가 있고 smithj라는 사용자에게 EXECUTE 액세스 권한을 부여하려는 경우 다음 GRANT 문을 실행합니다.
```sql
GRANT EXECUTE ON Find_Value TO smithj;
```
모든 사용자에게 이 함수를 실행할 수 있는 권한을 부여하려면 다음 GRANT 문을 실행합니다.
```sql
GRANT EXECUTE ON Find_Value TO public;
```

---
## 함수/프로시저에 대한 권한 제거
함수나 프로시저에 EXECUTE 권한을 부여한 후에는 사용자로부터 해당 권한을 제거해야 할 수 있습니다. 이렇게 하려면 REVOKE 명령을 실행하면 됩니다.

### 구문
Oracle에서 함수/프로시저에 대한 권한을 제거하는 구문은 다음과 같습니다.
```sql
REVOKE EXECUTE ON object FROM user;
```
#### **EXECUTE**
- 함수/프로시저를 컴파일할 수 있는 기능입니다. 함수/프로시저를 직접 실행할 수 있는 기능입니다.
#### **object**
- 권한을 제거할 데이터베이스 오브젝트의 이름입니다. 함수/프로시저에 대한 EXECUTE 권한을 제거하는 경우 함수 이름 또는 프로시저 이름이 됩니다.
#### **user**
- EXECUTE 권한을 제거할 사용자의 이름입니다.

### 예제
Oracle에서 함수/프로시저에 대한 EXECUTE 권한을 제거하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

anderson이라는 사용자로부터 Find_Value라는 함수에 대한 EXECUTE 권한을 제거하려는 경우 다음 REVOKE 문을 실행합니다.
```sql
REVOKE 실행 ON Find_Value FROM anderson;
```
Find_Value라는 함수에 대해 공개(모든 사용자)에게 EXECUTE 권한을 부여한 경우 이러한 EXECUTE 권한을 제거하려면 다음 REVOKE 문을 실행하면 됩니다.
```sql
REVOKE EXECUTE ON Find_Value FROM public;
```

---
**[< 이전](Indexes.md) / [다음 : Synonyms >](Synonyms.md)**