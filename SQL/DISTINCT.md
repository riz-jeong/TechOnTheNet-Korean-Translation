# SQL: DISTINCT 절

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **DISTINCT 절**을 사용하는 방법을 설명합니다.

## 설명
SQL DISTINCT 절은 SELECT 문의 결과 집합에서 중복을 제거하는 데 사용됩니다.

## 구문
SQL에서 DISTINCT 절의 구문은 다음과 같습니다.
```SQL
SELECT DISTINCT expressions
FROM tables
[WHERE conditions];
```
### 매개변수 및 인수
#### **expressions(표현식)**
- 검색하려는 열 또는 계산입니다.
#### **tables(테이블)**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하기 위해 충족해야 하는 조건입니다.

## 참고
- DISTINCT 절에 하나의 표현식만 제공된 경우 쿼리는 해당 표현식에 대한 고유 값을 반환합니다.
- DISTINCT 절에 둘 이상의 표현식이 제공되면 쿼리는 나열된 표현식에 대한 고유한 조합을 검색합니다.
- SQL에서 DISTINCT 절은 NULL 값을 무시하지 않습니다. 따라서 SQL 문에서 DISTINCT 절을 사용하면 결과 집합에 NULL이 고유 값으로 포함됩니다.

---
## DDL/DML 예제
튜토리얼을 따라 하려면 테이블을 생성하는 DDL과 데이터를 채우는 DML을 받으세요. 그런 다음 자신의 데이터베이스에서 예제를 사용해 보세요!

**[DDL/DML 받기](https://www.techonthenet.com/sql/distinct_ddl.php)**

---
## 예제 - 열에서 고유 값 찾기
DISTINCT 절을 사용하여 테이블의 한 열 내에서 고유 값을 찾는 방법을 살펴보겠습니다.

이 예제에서는 다음과 같은 데이터가 있는 suppliers라는 테이블이 있습니다.

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

suppliers 테이블에서 모든 고유 state를 찾아보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/distinct_try_sql.php)**
```SQL
SELECT DISTINCT state
FROM suppliers
ORDER BY state;
```
6개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| state      |
| :--------- |
| Arkansas   |
| California |
| Georgia    |
| Texas      |
| Washington |
| Wisconsin  |

이 예제에서는 suppliers 테이블에서 모든 고유한 state 값을 반환하고 결과 집합에서 중복된 값을 제거합니다. 보시다시피 California 주는 결과 집합에 네 번이 아니라 한 번만 나타납니다.

---
## 예제 - 여러 열에서 고유 값 찾기
다음으로, SELECT 문에서 두 개 이상의 필드에서 중복을 제거하기 위해 SQL DISTINCT 절을 사용하는 방법을 살펴보겠습니다.

이전 예제의 동일한 suppliers 테이블을 사용하여 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/distinct_try_sql.php)**
```SQL
SELECT DISTINCT city, state
FROM suppliers
ORDER BY city, state;
```
8개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| city             | state      |
| :--------------- | :--------- |
| Irving           | Texas      |
| Mountain View    | California |
| Racine           | Wisconsin  |
| Redmond          | Washington |
| Redwood City     | California |
| Springdale       | Arkansas   |
| Thomasville      | Georgia    |
| Westlake Village | California |

이 예제에서는 각각의 고유한 city 및 state 조합을 반환합니다. 이 경우 DISTINCT 키워드 뒤에 나열된 각 필드에 DISTINCT가 적용됩니다. 보시다시피, California주 Redwood City는 결과 집합에 두 번이 아니라 한 번만 나타납니다.

---
## 예제 - DISTINCT 절이 NULL 값을 처리하는 방법
마지막으로, DISTINCT 절은 SQL에서 NULL을 고유 값으로 간주하나요? 대답은 '예'입니다. 이에 대해 더 자세히 살펴보겠습니다.

이 예제에는 다음과 같은 데이터가 있는 products라는 테이블이 있습니다.

| product_id | product_name | category_id |
| :--------- | :----------- | :---------- |
| 1          | Pear         | 50          |
| 2          | Banana       | 50          |
| 3          | Orange       | 50          |
| 4          | Apple        | 50          |
| 5          | Bread        | 75          |
| 6          | Sliced Ham   | 25          |
| 7          | Kleenex      | NULL        |

이제 category_id 필드에서 NULL 값이 포함된 고유 값을 선택해 보겠습니다. 다음 SQL 문을 입력합니다. **[Try it](https://www.techonthenet.com/sql/distinct_try_sql.php)**
```SQL
SELECT DISTINCT category_id
FROM products
ORDER BY category_id;
```
4개의 레코드가 선택됩니다. 아래가 표시되는 결과입니다.

| category_id |
| :---------- |
| NULL        |
| 25          |
| 50          |
| 75          |

이 예제에서 쿼리는 category_id 열에 있는 고유 값을 반환합니다. 결과 집합의 첫 번째 행에서 볼 수 있듯이, NULL은 DISTINCT 절에서 반환되는 고유 값입니다.

---
**[< 이전](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/AND_OR.md) / [다음 : IN >](https://github.com/riz-jeong/TechOnTheNet-Korean-Translation/blob/main/SQL/IN.md)**