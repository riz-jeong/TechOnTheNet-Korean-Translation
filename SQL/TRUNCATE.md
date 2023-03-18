# SQL : TRUNCATE TABLE 문

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **TRUNCATE TABLE 문**을 사용하는 방법을 설명합니다.

## 설명
SQL TRUNCATE TABLE 문은 테이블에서 모든 레코드를 제거하는 데 사용됩니다. 이 문은 WHERE 절이 없는 DELETE 문과 동일한 기능을 수행합니다.

>경고: 일부 데이터베이스에서는 TRUNCATE TABLE 문을 롤백할 수 없습니다.

## 구문
SQL에서 TRUNCATE TABLE 문의 구문은 다음과 같습니다.
```SQL
TRUNCATE TABLE table_name;
```
### 매개변수 및 인수
#### table_name
- 잘라내려는 테이블입니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/truncate_ddl.php)**

---
## 예제
테이블을 삭제하고 다시 만드는 대신 테이블을 잘라내도록 선택할 수 있습니다. 테이블을 잘라내는 것이 더 빠를 수 있으며 테이블의 인덱스, 트리거 및 종속성에는 영향을 미치지 않습니다. 또한 롤백에 대해 걱정할 필요가 없는 경우 테이블에서 레코드를 빠르게 지울 수 있는 방법이기도 합니다.

SQL에서 TRUNCATE TABLE 문을 사용하는 방법에 대한 예를 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다.

| supplier_id | supplier_name     | city             | state      |
| :---------- | :---------------- | :--------------- | :--------- |
| 100         | Microsoft         | Redmond          | Washington |
| 200         | Google            | Mountain View    | California |
| 300         | Oracle            | Redwood City     | California |
| 400         | Kimberly-Clark    | Irving           | Texas      |
| 500         | Tyson Foods       | Springdale       | Arkansas   |
| 600         | SC Johnson        | Racine           | Wisconsin  |
| 700         | Dole Food Company | Westlake Village | California |
| 800         | Flowers Foods     | Thomasville      | Georgia    |
| 900         | Electronic Arts   | Redwood City     | California |

다음 TRUNCATE TABLE 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/truncate_try_sql.php)**
```SQL
TRUNCATE TABLE suppliers;
```
그런 다음 suppliers 테이블에서 데이터를 다시 선택합니다.
```SQL
SELECT * FROM suppliers;
```
다음은 표시되는 결과입니다.

| supplier_id | supplier_name | city | state |
| :---------- | :------------ | :--- | :---- |
|             |               |      |       |

이 예제에서는 공급업체라는 테이블을 잘라내고 해당 테이블에서 모든 레코드를 제거합니다. 이는 SQL에서 다음 DELETE 문과 동일합니다. **[Try it](https://www.techonthenet.com/sql/truncate_try_sql.php)**
```SQL
DELETE FROM suppliers;
```
이 두 문 모두 suppliers 테이블의 모든 데이터가 삭제됩니다. 이 둘의 주요 차이점은 원하는 경우 DELETE 문을 롤백할 수 있지만 모든 SQL 데이터베이스에서 TRUNCATE TABLE 문을 롤백하지 못할 수도 있다는 점입니다.

테이블 이름 앞에 데이터베이스 이름을 접두사로 붙여야 하는 경우 다음과 같이 TRUNCATE TABLE 문을 다시 작성할 수 있습니다.

```SQL
TRUNCATE TABLE totn.suppliers;
```

이 예제에서는 totn이라는 데이터베이스에서 suppliers라는 테이블을 잘라냅니다.

---
**[< 이전](DELETE.md) / [다음 : TRUNCATE >](EXISTS.md)**