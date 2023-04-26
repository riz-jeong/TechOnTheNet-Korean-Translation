# Oracle / PLSQL : 하위 쿼리

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **하위 쿼리**를 사용하는 방법을 설명합니다.

## Oracle에서 하위 쿼리란 무엇인가요?
Oracle에서 하위 쿼리는 쿼리 내의 쿼리입니다. SQL 문 내에 하위 쿼리를 만들 수 있습니다. 이러한 하위 쿼리는 WHERE 절, FROM 절, SELECT 절에 위치할 수 있습니다.

---
## WHERE 절
대부분의 경우 하위 쿼리는 WHERE 절에서 찾을 수 있습니다. 이러한 하위 쿼리를 중첩 하위 쿼리라고도 합니다.
```sql
SELECT * 
FROM all_tables tabs
WHERE tabs.table_name IN (SELECT cols.table_name
                          FROM all_tab_columns cols
                          WHERE cols.column_name = 'SUPPLIER_ID');
```

>제한 사항 : 오라클은 WHERE 절에서 최대 255개의 하위 쿼리 수준을 허용합니다.

---
## FROM 절
FROM 절에서도 하위 쿼리를 찾을 수 있습니다. 이를 인라인 뷰라고 합니다.
```sql
SELECT suppliers.name, subquery1.total_amt
FROM suppliers,
 (SELECT supplier_id, SUM(orders.amount) AS total_amt
  FROM orders
  GROUP BY supplier_id) subquery1
WHERE subquery1.supplier_id = suppliers.supplier_id;
```
이 예제에서는 다음과 같이 FROM 절에 하위 쿼리를 만들었습니다.
```sql
(SELECT supplier_id, SUM(orders.amount) AS total_amt
 FROM orders
 GROUP BY supplier_id) subquery1
```
이 하위 쿼리는 subquery1이라는 이름으로 별칭이 지정되었습니다. 이 하위 쿼리 또는 해당 필드를 참조하는 데 사용되는 이름입니다.

>제한 사항 : Oracle에서는 FROM 절에 하위 쿼리를 무제한으로 허용합니다.

---
## SELECT 절
SELECT 절에서도 하위 쿼리를 찾을 수 있습니다.
```sql
SELECT tbls.owner, tbls.table_name,
  (SELECT COUNT(column_name) AS total_columns
   FROM all_tab_columns cols
   WHERE cols.owner = tbls.owner
   AND cols.table_name = tbls.table_name) subquery2
FROM all_tables tbls;
```
이 예제에서는 SELECT 절에 다음과 같이 하위 쿼리를 만들었습니다.
```sql
(SELECT COUNT(column_name) AS total_columns
 FROM all_tab_columns cols
 WHERE cols.owner = tbls.owner
 AND cols.table_name = tbls.table_name) subquery2
```
하위 쿼리의 별칭이 subquery2로 지정되었습니다. 이 하위 쿼리 또는 해당 필드를 참조하는 데 사용되는 이름입니다.

선택 절에 하위 쿼리를 배치하는 요령은 하위 쿼리가 단일 값을 반환해야 한다는 것입니다. 따라서 하위 쿼리에는 일반적으로 [SUM 함수](SUM.md), [COUNT 함수](COUNT.md), [MIN 함수](MIN.md), [MAX 함수](MAX.md)와 같은 집계 함수가 사용됩니다.

---
**[< 이전](MINUS.md) / [다음 : PIVOT >](PIVOT.md)**