# SQL : AVG 함수

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL **AVG 함수**를 사용하는 방법을 설명합니다.

## 설명
SQL AVG 함수는 SELECT 문에서 식의 평균을 반환하는 데 사용됩니다.

## 구문
SQL에서 AVG 함수의 구문은 다음과 같습니다.
```SQL
SELECT AVG(aggregate_expression)
FROM tables
[WHERE conditions];
```
또는 하나 이상의 열을 기준으로 결과를 그룹화할 때 MIN 함수의 구문은 다음과 같습니다.
```SQL
SELECT expression1, expression2, ... expression_n,
       AVG(aggregate_expression)
FROM tables
[WHERE conditions]
GROUP BY expression1, expression2, ... expression_n;
```
### 매개변수 및 인수
#### **expression1, expression2, ... expression_n
- AVG 함수 내에 캡슐화되지 않은 표현식은 SQL 문 끝에 있는 GROUP BY 절에 포함되어야 합니다.
#### **aggregate_expression
- 평균을 구할 열 또는 표현식입니다.
#### **tables
- 레코드를 검색하려는 테이블입니다. FROM 절에 테이블이 하나 이상 나열되어 있어야 합니다.
#### **WHERE conditions(WHERE 조건)
- 선택 사항입니다. 레코드를 선택하려면 반드시 충족해야 하는 조건입니다.

---
## 예제 - 단일 표현식 사용
예를 들어 의류 카테고리에 있는 모든 제품의 평균 비용이 얼마인지 알고 싶을 수 있습니다.
```SQL
SELECT AVG(cost) AS "Average Cost"
FROM products
WHERE category = 'Clothing';
```
이 SQL AVG 함수 예제에서는 AVG(cost) 식의 [별칭](ALIASES.md)을 "Average Cost"로 지정했습니다. 결과적으로 결과 집합이 반환될 때 "Average Cost"가 필드 이름으로 표시됩니다.

---
## 예제 - SQL DISTINCT 사용
AVG 함수 내에서 SQL [DISTINCT 절](DISTINCT.md)을 사용할 수 있습니다. 예를 들어, 아래 SELECT 문은 카테고리가 Clothing인 고유 비용 값의 합산 평균 비용을 반환합니다.
```SQL
SELECT AVG(DISTINCT cost) AS "Average Cost"
FROM products
WHERE category = 'Clothing';
```
비용 값이 $25인 두 개의 비용 값이 있는 경우, 이 값 중 하나만 AVG 함수 계산에 사용됩니다.

---
## 예제 - 수식 사용
AVG 함수에 포함된 표현식은 단일 필드일 필요는 없습니다. 수식을 사용할 수도 있습니다. 예를 들어 제품의 평균 수익이 필요할 수 있습니다. 평균 수익은 sale_price에서 cost를 뺀 값으로 계산됩니다.
```SQL
SELECT AVG(sale_price - cost) AS "Average Profit"
FROM products;
```
AVG 함수 내에서 수학적 연산을 수행할 수도 있습니다. 예를 들어 평균 커미션을 sale_price의 10%로 결정할 수 있습니다.
```SQL
SELECT AVG(sale_price * 0.10) AS "Average Commission"
FROM products;
```

---
## 예제 - SQL GROUP BY 사용
경우에 따라 AVG 함수와 함께 SQL [GROUP BY 절](GROUP_BY.md)을 사용해야 할 수도 있습니다.

예를 들어 AVG 함수를 사용하여 부서 이름과 관련 부서의 평균 매출을 반환할 수도 있습니다.
```SQL
SELECT department, AVG(sales) AS "Average Sales"
FROM order_details
WHERE department > 10
GROUP BY department;
```
[SELECT 문](SELECT.md)에 AVG 함수에 캡슐화되지 않은 열 하나를 나열했으므로 [GROUP BY 절](GROUP_BY.md)을 사용해야 합니다. 따라서 부서 필드는 GROUP BY 섹션에 나열되어야 합니다.

---
**[< 이전](MIN.md) / [다음 : HAVING >](HAVING.md)**