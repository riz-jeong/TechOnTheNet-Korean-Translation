# SQL : MAX 함수
이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **MAX 함수**를 사용하는 방법을 설명합니다.

## 설명
SQL MAX 함수는 SELECT 문에서 식의 최대값을 반환하는 데 사용됩니다.

## 구문
SQL에서 MAX 함수의 구문은 다음과 같습니다.
```SQL
SELECT MAX(aggregate_expression)
FROM tables
[WHERE conditions];
```
또는 하나 이상의 열을 기준으로 결과를 그룹화할 때 MAX 함수의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n,
       MAX(aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n**
- MAX 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_expression**
- 최대값이 반환되는 열 또는 표현식입니다.
#### **tables**
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)**
- 선택 사항입니다. 레코드를 선택하려면 반드시 충족해야 하는 조건입니다.

---
## 예제 - 단일 표현식 사용
SQL MAX 함수를 사용하는 가장 간단한 방법은 MAX 값을 계산하는 단일 필드를 반환하는 것입니다.

예를 들어 모든 직원의 최대 salary를 알고 싶을 수 있습니다.
```SQL
SELECT MAX(salary) AS "Highest salary"
FROM employees;
```
이 SQL MAX 함수 예제에서는 MAX(salary) 필드의 [별칭](ALIASES.md)을 "Highest salary"로 지정했습니다. 결과적으로 결과 집합이 반환될 때 "Highest salary"가 필드 이름으로 표시됩니다.

---
## 예제 - SQL GROUP BY 절 사용
경우에 따라 SQL MAX 함수와 함께 SQL [GROUP BY 절](GROUP_BY.md)을 사용해야 할 수도 있습니다.

예를 들어 SQL MAX 함수를 사용하여 각 department의 이름과 해당 department의 최대 salary를 반환할 수도 있습니다.
```SQL
SELECT department, MAX(salary) AS "Highest salary"
FROM employees
GROUP BY department;
```
SQL [SELECT 문](SELECT.md)에 MAX 함수로 캡슐화되지 않은 열 하나를 나열했으므로 SQL [GROUP BY 절](GROUP_BY.md)을 사용해야 합니다. 따라서 부서 필드는 GROUP BY 섹션에 나열되어야 합니다.

---
## 자주 묻는 질문
- 질문 : 테이블에서 몇 가지 정보를 추출하려고 합니다. 간단하게 설명하기 위해 report_history 테이블에 user_name, report_job_id, report_name, report_run_date의 4개 열이 있다고 가정해 보겠습니다.

Oracle에서 보고서가 실행될 때마다 위의 정보가 기록된 레코드가 이 테이블에 기록됩니다. 제가 하고자 하는 것은 이 테이블에서 각 개별 보고서가 마지막으로 실행된 시점과 마지막으로 실행한 사람을 가져오는 것입니다.

내 초기 쿼리입니다.
```SQL
SELECT report_name, MAX(report_run_date)
FROM report_history
GROUP BY report_name
```
는 정상적으로 실행됩니다. 그러나 보고서를 실행한 사용자의 이름은 제공하지 않습니다.

선택 목록과 그룹별 절에 user_name을 추가하면 각 보고서에 대해 여러 줄이 반환되며, 결과에는 각 사용자가 해당 보고서를 마지막으로 실행한 시간이 표시됩니다. (예: User1은 Report 1을 01-JUL-03에 실행했고, User2는 Report 1을 01-AUG-03에 실행했습니다). 그런 건 필요 없습니다... 특정 보고서를 마지막으로 실행한 사람이 누구인지 알고 싶을 뿐입니다.

어떤 제안이 있나요?

- 답변 : 여기서부터 상황이 조금 복잡해집니다. 아래의 SQL SELECT 문은 원하는 결과를 반환합니다.
```SQL
SELECT rh.user_name, rh.report_name, rh.report_run_date
FROM report_history rh,
  (SELECT MAX(report_run_date) AS maxdate, report_name
   FROM report_history
   GROUP BY report_name) maxresults
WHERE rh.report_name = maxresults.report_name
AND rh.report_run_date= maxresults.maxdate;
```
잠시 시간을 내어 저희가 한 일에 대해 설명해 드리겠습니다.

먼저 report_history 테이블의 첫 번째 인스턴스에 별칭을 rh로 지정했습니다.

둘째, FROM 절에 두 가지 구성 요소를 포함시켰습니다. 첫 번째는 report_history라는 테이블(별칭은 rh)입니다. 두 번째는 select 문입니다.
```SQL
(SELECT MAX(report_run_date) AS maxdate, report_name
 FROM report_history
 GROUP BY report_name) maxresults
```
max(report_run_date)의 별칭을 maxdate로 지정하고 전체 결과 집합의 별칭을 maxresults로 지정했습니다.

이제 FROM 절 내에 이 select 문을 만들었으므로 Oracle은 이러한 결과를 원래 report_history 테이블에 대해 조인할 수 있습니다. 따라서 report_name 및 report_run_date 필드를 rh 및 maxresults라는 테이블 간에 조인했습니다. 이렇게 하면 report_name, max(report_run_date) 및 user_name을 검색할 수 있습니다.

---
- 질문 : SQL 쿼리에 대한 도움이 필요합니다. Oracle에 order_no, customer, amount 필드가 있는 orders이라는 테이블이 있습니다.

총 주문 금액이 가장 높은 고객을 반환하는 쿼리가 필요합니다.

- 답변 : 다음 SQL은 orders 테이블에서 총 금액이 가장 높은 고객을 반환해야 합니다.
```SQL
SELECT query1.*
FROM (SELECT customer, SUM(orders.amount) AS total_amt
      FROM orders
      GROUP BY orders.customer) query1,

     (SELECT MAX(query2.total_amt) AS highest_amt
      FROM (SELECT customer, SUM(orders.amount) AS total_amt
            FROM orders
            GROUP BY orders.customer) query2) query3
WHERE query1.total_amt = query3.highest_amt;
```
이 SQL SELECT 문은 각 고객의 총 주문을 요약한 다음 총 주문이 가장 많은 고객을 반환합니다. 이 구문은 Oracle에 최적화되어 있으며 다른 데이터베이스 기술에서는 작동하지 않을 수 있습니다.

---
- 질문 : Oracle 데이터베이스에서 몇 가지 정보를 검색하려고 합니다. Name과 Score라는 두 개의 필드가 있는 Scoring이라는 테이블이 있습니다. 제가 얻고 싶은 것은 테이블에서 가장 높은 점수와 선수의 이름입니다.

- 답변 : 다음 SQL SELECT 문이 작동합니다.
```SQL
SELECT Name, Score
FROM Scoring
WHERE Score = (SELECT MAX(Score) FROM Scoring);
```

---
- 질문 : SQL 쿼리에 대한 도움이 필요합니다. Oracle에 OrderNo, Customer_id, Order_Date, Amount와 같은 필드가 있는 cust_order라는 테이블이 있습니다.

주문 수가 가장 많은 customer_id를 찾고 싶습니다.

다음 쿼리로 시도해 보았습니다.
```SQL
SELECT MAX(COUNT(*))
FROM CUST_ORDER
GROUP BY CUSTOMER_ID;
```
이렇게 하면 최대 카운트가 나오지만 CUSTOMER_ID를 얻을 수 없습니다. 도와주실 수 있나요?

- 답변 : 다음 SQL SELECT 문은 cust_order 테이블에서 주문 수가 가장 많은 고객을 반환해야 합니다.
```SQL
SELECT query1.*
FROM (SELECT Customer_id, Count(*) AS order_count
      FROM cust_order
      GROUP BY cust_order.Customer_id) query1,

     (SELECT max(query2.order_count) AS highest_count
      FROM (SELECT Customer_id, Count(*) AS order_count
            FROM cust_order
            GROUP BY cust_order.Customer_id) query2) query3
WHERE query1.order_count = query3.highest_count;
```
이 SQL SELECT 문은 각 고객의 총 주문을 합산한 다음 주문 수가 가장 많은 고객을 반환합니다. 이 구문은 Oracle에 최적화되어 있으며 다른 데이터베이스 기술에서는 작동하지 않을 수 있습니다.

---
- 질문 : 부서 30에서 최대 급여를 받는 직원을 가져오려고 하는데 직원의 전체 정보를 표시해야 합니다. 다음 쿼리를 시도했지만 30번 부서와 80번 부서의 결과가 모두 반환됩니다.
```SQL
SELECT *
FROM employees
WHERE salary = (SELECT MAX(salary)
                FROM employees
                WHERE department_id=30);
```

- 답변 : 작성한 SQL SELECT 문은 먼저 부서 30의 최대 급여를 결정한 다음 이 급여를 받는 모든 직원을 선택합니다. 이 경우 동일한 급여를 받는 직원이 2명(부서 30에 1명, 부서 80에 1명)이어야 합니다. 부서 30의 직원만 반환하도록 쿼리 결과를 구체화해야 합니다.

이 SQL SELECT 문을 사용해 보세요.
```SQL
SELECT *
FROM employees
WHERE department_id=30
AND salary = (SELECT MAX(salary)
              FROM employees
              WHERE department_id=30);
```
이렇게 하면 급여가 가장 높은 30번 부서의 직원에 대한 직원 정보만 반환됩니다.

---
**[< 이전](SUM.md) / [다음 : MIN >](MIN.md)**