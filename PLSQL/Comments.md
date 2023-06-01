# Oracle / PLSQL : SQL 내 주석
이 Oracle 튜토리얼에서는 구문과 예제를 통해 Oracle/PLSQL에서 SQL 문 내에서 주석을 사용하는 방법을 설명합니다.

## 설명
Oracle에서 SQL 문 안에 주석을 넣을 수 있다는 사실을 알고 계셨나요? 이러한 주석은 한 줄에 표시되거나 여러 줄에 걸쳐 표시될 수 있습니다. 이를 수행하는 방법을 살펴보겠습니다.

## 구문
Oracle/PLSQL에서 SQL 문 내에 주석을 만드는 데 사용할 수 있는 구문에는 두 가지가 있습니다.

### `--` 기호 사용
`--` 기호를 사용하여 Oracle에서 SQL 주석을 만드는 구문은 다음과 같습니다.
```sql
-- comment goes here
```
Oracle에서 `--` 기호로 시작하는 주석은 SQL 문에서 줄 바꿈이 있는 줄 끝에 있어야 합니다. 이 주석 방법은 SQL 내에서 한 줄에 걸쳐서만 사용할 수 있으며 줄 끝에 있어야 합니다.

### `/*` 및 `*/` 기호 사용
Oracle에서 `/*` 및 `*/` 기호를 사용하여 SQL 주석을 만드는 구문은 다음과 같습니다.
```sql
/* comment goes here */
```
Oracle에서 주석은 `/*` 기호로 시작하고 `*/`로 끝나는 주석으로, SQL 문의 어느 곳에나 사용할 수 있습니다. 이 주석 방법은 SQL 내에서 여러 줄에 걸쳐 사용할 수 있습니다.

---
## 예제 - 한 줄에 주석 달기
Oracle/PLSQL의 SQL 문에서 한 줄에 SQL 주석을 만들 수 있습니다.

한 줄에 SQL 주석을 표시하는 SQL 주석 예제를 살펴보겠습니다.

```sql
SELECT suppliers.supplier_id
/* Author: TechOnTheNet.com */
FROM suppliers;
```

다음은 줄 중간에 표시되는 SQL 주석입니다.

```sql
SELECT  /* Author: TechOnTheNet.com */  suppliers.supplier_id
FROM suppliers;
```

다음은 줄 끝에 표시되는 SQL 주석입니다.

```sql
SELECT suppliers.supplier_id  /* Author: TechOnTheNet.com */
FROM suppliers;
```

또는

```sql
SELECT suppliers.supplier_id  -- Author: TechOnTheNet.com
FROM suppliers;
```

---
## 예제 - 여러 줄에 주석 달기
Oracle에서는 SQL 문에서 여러 줄에 걸쳐 있는 SQL 주석을 만들 수 있습니다.
```sql
SELECT suppliers.supplier_id
/*
 * Author: TechOnTheNet.com
 * Purpose: To show a comment that spans multiple lines in your SQL statement.
 */
FROM suppliers;
```
이 SQL 주석은 Oracle에서 여러 줄에 걸쳐 있으며, 이 예제에서는 4줄에 걸쳐 있습니다.

Oracle에서는 이 구문을 사용하여 여러 줄에 걸쳐 있는 SQL 주석을 만들 수도 있습니다.
```sql
SELECT suppliers.supplier_id /* Author: TechOnTheNet.com
Purpose: To show a comment that spans multiple lines in your SQL statement. */
FROM suppliers;
```
Oracle/PLSQL은 `/*` 기호 뒤에 오는 모든 것이 주석으로 간주하며, 이는 SQL 문 내에서 여러 줄에 걸쳐 있더라도 `*/` 기호에 도달하기 전까지는 주석으로 간주합니다. 따라서 이 예제에서는 SQL 주석이 두 줄에 걸쳐 있습니다.

---
**[< 이전](Find_Users_Logged_In.md) / [다음 : Literals >](Literals.md)**