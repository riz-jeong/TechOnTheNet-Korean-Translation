# SQL : 인덱스

이 SQL 튜토리얼에서는 구문과 예제를 통해 인덱스를 생성하고 삭제하는 방법을 설명합니다.

## SQL에서 인덱스란 무엇인가요?
인덱스는 레코드를 더 빠르게 검색할 수 있도록 하는 성능 조정 방법입니다. 인덱스는 인덱싱된 열에 나타나는 각 값에 대한 항목을 생성합니다. 각 인덱스 이름은 데이터베이스에서 고유해야 합니다.

---
## 인덱스 생성
CREATE INDEX 문을 사용하여 SQL에서 인덱스를 생성할 수 있습니다.

### 구문
SQL에서 인덱스를 만드는 구문은 다음과 같습니다.
```SQL
CREATE [UNIQUE] INDEX index_name
  ON table_name (column1, column2, ... column_n);
```
#### **UNIQUE**
- UNIQUE 수정자는 인덱싱된 열의 값 조합이 고유해야 함을 나타냅니다.
#### **index_name**
- 인덱스에 할당할 이름입니다.
#### **table_name**
- 인덱스를 생성할 테이블의 이름입니다.
#### **column1, column2, ... column_n**
- 인덱스에 사용할 열입니다.

### 예제
SQL에서 인덱스를 만드는 방법의 예를 살펴보겠습니다.
```SQL
CREATE INDEX websites_idx
  ON websites (site_name);
```
이 예제에서는 websites 테이블에 websites_idx라는 인덱스를 만들었습니다. 이 인덱스는 site_name 필드라는 하나의 필드로만 구성됩니다.

아래 예제에서와 같이 둘 이상의 필드가 있는 인덱스를 만들 수도 있습니다.
```SQL
CREATE INDEX websites_idx
  ON websites (site_name, server);
```
이렇게 하면 site_name과 서버라는 두 개의 열로 구성된 websites_idx라는 인덱스가 생성됩니다.

고유 인덱스

기본 키와 마찬가지로 고유 키를 사용하면 각 레코드에 대해 고유해야 하는 하나의 열 또는 열 조합을 선택할 수 있습니다. 테이블에 기본 키는 하나만 가질 수 있지만 테이블에 고유 인덱스는 필요한 만큼 많이 만들 수 있습니다.

테이블에 고유 인덱스를 생성하려면 CREATE INDEX 문에 UNIQUE 키워드를 지정해야 합니다.
```SQL
CREATE UNIQUE INDEX websites_idx
  ON websites (site_name);
```
이 예제에서는 site_name 필드에 고유 인덱스를 생성하여 이 필드에 항상 중복되지 않는 고유한 값을 포함하도록 합니다. 기본 키에 포함되지 않은 열에 고유 값이 필요한 경우 데이터베이스 내에서 무결성을 강화할 수 있는 좋은 방법입니다.

---
## 인덱스 삭제
DROP INDEX 문을 사용하여 SQL에서 인덱스를 삭제할 수 있습니다.

### 구문
Oracle, PostgreSQL의 경우

```SQL
DROP INDEX index_name;
```

MySQL, MariaDB의 경우

```SQL
DROP INDEX index_name
  ON table_name;
```

SQL Server의 경우

```SQL
DROP INDEX table_name.index_name;
```

#### **index_name**
- 삭제할 인덱스의 이름입니다.
#### **table_name**
- 인덱스가 속한 테이블의 이름입니다.

### 예제
웹사이트 테이블에서 websites_idx라는 인덱스를 삭제하는 방법의 예를 살펴보겠습니다.

Oracle의 경우

```SQL
DROP INDEX websites_idx;
```
각 인덱스 이름은 데이터베이스 내에서 고유해야 하므로 Oracle의 DROP INDEX 문에서 websites 테이블을 지정할 필요가 없습니다.

MySQL, MariaDB의 경우

```SQL
DROP INDEX websites_idx
  ON websites;
```

SQL Server의 경우

```SQL
DROP INDEX websites.websites_idx;
```

보시다시피 각 데이터베이스는 구문에 고유한 차이가 있습니다. 올바른 DROP INDEX 명령을 사용해야 합니다.

---
**[< 이전](LOCAL_TEMP.md) / [다음 : COMMENTS >](Comments.md)**