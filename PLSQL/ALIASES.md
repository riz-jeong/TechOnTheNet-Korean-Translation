# Oracle / PLSQL : 별칭

이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle **ALIASES** (열 또는 테이블의 임시 이름)를 사용하는 방법을 설명합니다.

## 설명
Oracle ALIASES는 열 또는 테이블의 임시 이름을 만드는 데 사용할 수 있습니다.

- 열 ALIASES는 결과 집합의 열 제목을 읽기 쉽게 만드는 데 사용됩니다.
- 테이블 ALIASES는 읽기 쉽도록 SQL을 줄이거나 자체 조인을 수행할 때 사용됩니다. (예: FROM 절에 동일한 테이블을 두 번 이상 나열하는 경우)

## 구문
Oracle/PLSQL에서 열에 ALIASES를 지정하는 구문은 다음과 같습니다.
```SQL
column_name AS alias_name
```
OR

Oracle/PLSQL에서 테이블에 ALIASES를 지정하는 구문은 다음과 같습니다.
```SQL
table_name alias_name
```
### 매개변수 및 인수
#### **column_name**
- 별칭을 지정하려는 열의 원래 이름입니다.
#### **table_name**
- 별칭을 지정하려는 테이블의 원래 이름입니다.
#### **alias_name**
- 할당할 임시 이름입니다.

## 참고
- alias_name에 공백이 포함된 경우, 공백을 따옴표로 묶어야 합니다.
- 열 이름을 별칭으로 지정할 때는 공백을 사용할 수 있습니다. 그러나 일반적으로 테이블 이름에 별칭을 지정할 때 공백을 사용하는 것은 좋지 않습니다.
- alias_name은 SQL 문의 범위 내에서만 유효합니다.

---
## 예제 - 열에 별칭 지정
일반적으로 별칭은 결과 집합의 열 제목을 더 읽기 쉽게 만드는 데 사용됩니다. 예를 들어 필드를 서로 연결할 때 결과에 별칭을 지정할 수 있습니다.
```SQL
SELECT contact_id, first_name || last_name AS NAME
FROM contacts
WHERE last_name = 'Anderson';
```
이 예제에서는 두 번째 열(즉, first_name 및 last_name [연결](CONCAT2.md))의 별칭을 NAME으로 지정했습니다. 결과적으로 결과 집합이 반환될 때 두 번째 열의 제목으로 NAME이 표시됩니다. 별칭 이름에 공백이 포함되지 않았으므로 별칭 이름을 따옴표로 묶을 필요가 없습니다.

그러나 이 예제를 다음과 같이 따옴표로 묶어 작성해도 무방했을 것입니다.
```SQL
SELECT contact_id, first_name || last_name AS "NAME"
FROM contacts
WHERE last_name = 'Anderson';
```
다음으로, alias_name을 따옴표로 묶어야 하는 예제를 살펴보겠습니다.
```SQL
SELECT contact_id, first_name || last_name AS "CONTACT NAME"
FROM contacts
WHERE last_name = 'Anderson';
```
이 예제에서는 두 번째 열(즉, 첫 번째 이름과 마지막 이름이 [연결](CONCAT2.md))의 별칭을 "CONTACT NAME"으로 지정했습니다. 이 alias_name에는 공백이 있으므로 "CONTACT NAME"은 따옴표로 묶어야 합니다.

---
## 예제 - 테이블에 별칭 지정
테이블에 별칭을 만드는 이유는 FROM 절에 동일한 테이블 이름을 두 번 이상 나열하려는 경우(예: 자체 조인) 또는 SQL 문을 더 짧고 읽기 쉽게 만들기 위해 테이블 이름을 줄이려는 경우입니다.

Oracle/PLSQL에서 테이블 이름을 별칭으로 지정하는 방법의 예를 살펴보겠습니다.
```SQL
SELECT p.product_id, p.product_name, categories.category_name
FROM products p
INNER JOIN categories
ON p.category_id = categories.category_id
ORDER BY p.product_name ASC, categories.category_name ASC;
```
이 예제에서는 p라는 products 테이블의 별칭을 만들었습니다. 이제 이 SQL 문 내에서 products 테이블을 p로 참조할 수 있습니다.

테이블 별칭을 만들 때 FROM 절에 나열된 모든 테이블에 대해 별칭을 만들 필요는 없습니다. 일부 또는 모든 테이블에 별칭을 만들도록 선택할 수 있습니다.

예를 들어 위의 예제를 수정하여 categories 테이블에 대한 별칭도 만들 수 있습니다.
```SQL
SELECT p.product_id, p.product_name, c.category_name
FROM products p
INNER JOIN categories c
ON p.category_id = c.category_id
ORDER BY p.product_name ASC, c.category_name ASC;
```
이제 categories 테이블의 별칭이 c로 지정되고 products 테이블의 별칭이 p로 지정되었습니다.

---
**[< 이전](NOT.md) / [다음 : JOINS >](JOINS.md)**