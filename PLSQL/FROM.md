# Oracle / PLSQL : FROM 절

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle/PLSQL에서 **FROM 절**을 사용하는 방법을 설명합니다.

## 설명
Oracle/PLSQL FROM 절은 Oracle 쿼리에 필요한 테이블 및 모든 조인 정보를 나열하는 데 사용됩니다.

## 구문
Oracle/PLSQL에서 FROM 절의 구문은 다음과 같습니다:
```SQL
FROM table1
[ { INNER JOIN
  | LEFT [OUTER] JOIN
  | RIGHT [OUTER] JOIN
  | FULL [OUTER] JOIN } table2
ON table1.column1 = table2.column1 ]
```
### 매개변수 및 인수
#### **table1 and table2**
- 다음은 SQL 문에 사용된 테이블입니다. 두 테이블은 table1.column1 = table2.column1을 기준으로 조인됩니다.

## 참고
- Oracle/PLSQL의 FROM 절에 하나 이상의 테이블이 나열되어야 합니다.
- FROM 절에 두 개 이상의 테이블이 나열되어 있는 경우 이러한 테이블은 일반적으로 INNER 또는 OUTER JOIN을 사용하여 FROM 절에서 조인됩니다. WHERE 절의 이전 구문을 사용하여 테이블을 조인할 수도 있지만, 새로운 표준을 사용하고 FROM 절에 조인 정보를 포함하는 것이 좋습니다. [자세한 내용은 Oracle 조인을 참조하십시오.](JOINS.md)

---
## 예제 - 하나의 테이블
Oracle FROM 절의 구문을 설명하기는 어렵기 때문에 몇 가지 예를 살펴보겠습니다.

먼저 테이블이 하나뿐인 경우에 FROM 절을 사용하는 방법부터 살펴보겠습니다.

예를 들어
```SQL
SELECT *
FROM homes
WHERE bathrooms >= 2
ORDER BY home_type ASC;
```
이 Oracle FROM 절 예제에서는 FROM 절을 사용하여 homes라는 테이블을 나열했습니다. 하나의 테이블만 사용하므로 조인이 수행되지 않습니다.

---
## 예제 - INNER JOIN이 있는 두 테이블
두 개의 테이블과 [INNER JOIN](JOINS.md)을 사용하여 FROM 절을 사용하는 방법을 살펴보겠습니다.

예를 들어
```SQL
SELECT homes.home_id, customers.last_name, customers.first_name
FROM customers
INNER JOIN homes
ON customers.customer_id = homes.customer_id
ORDER BY home_id;
```
이 Oracle FROM 절 예제에서는 FROM 절을 사용하여 customers와 homes라는 두 테이블을 나열합니다. 그리고 FROM 절을 사용하여 두 테이블의 customer_id 열을 기반으로 고객 테이블과 homes 테이블 간에 INNER JOIN을 지정하고 있습니다.

---
## 예제 - OUTER JOIN이 있는 두 테이블
[OUTER JOIN](JOINS.md)을 사용하여 두 테이블을 조인할 때 FROM 절을 사용하는 방법을 살펴보겠습니다. 이 경우 LEFT OUTER JOIN을 살펴보겠습니다.

예를 들어
```SQL
SELECT customers.customer_id, contacts.last_name, contacts.first_name
FROM customers
LEFT OUTER JOIN contacts
ON customers.customer_id = contacts.contact_id
WHERE customers.last_name = 'Smith';
```
이 Oracle FROM 절 예제에서는 FROM 절을 사용하여 customers과 contacts라는 두 테이블을 나열합니다. 그리고 FROM 절을 사용하여 두 테이블의 customer_id 열을 기반으로 customers 및 contacts 테이블 간에 LEFT OUTER JOIN을 지정하고 있습니다.

---
**[< 이전](SELECT.md) / [다음 : Comparison Operators >](Comparison_Operators.md)**