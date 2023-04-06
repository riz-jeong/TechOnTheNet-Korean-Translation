# SQL : 주석

이 SQL 튜토리얼에서는 구문과 예제를 통해 SQL 문 내에서 주석을 사용하는 방법을 설명합니다.

## 설명
SQL에서는 다른 언어와 마찬가지로 코드에 주석을 달 수 있습니다. 주석은 한 줄에 표시하거나 여러 줄에 걸쳐 표시할 수 있습니다. SQL 문에 주석을 다는 방법을 살펴보겠습니다.

---
## 구문
SQL에서 댓글을 작성하는 데 사용할 수 있는 구문은 두 가지입니다.

### `--` 기호 사용
`--` 기호를 사용하여 SQL에서 주석을 만드는 구문은 다음과 같습니다.
```SQL
-- comment goes here
```
`--` 기호로 시작하는 주석은 SQL 문에서 줄 바꿈이 있는 줄 끝에 있어야 합니다. 이 주석 방법은 SQL 내에서 한 줄에 걸쳐서만 사용할 수 있으며 줄 끝에 있어야 합니다.

### `/*` 및 `*/` 기호 사용
`/*` 및 `*/` 기호를 사용하여 SQL에서 주석을 만드는 구문은 다음과 같습니다.
```SQL
/* comment goes here */
```
`/*` 기호로 시작하고 `*/`로 끝나는 주석은 SQL 문의 어느 곳에나 사용할 수 있습니다. 이 주석 방법은 SQL 내에서 여러 줄에 걸쳐 사용할 수 있습니다.

---
## 예제 - 한 줄에 주석 달기
SQL에서 한 줄로 된 주석을 만드는 방법을 보여주는 예제를 살펴보겠습니다.

다음은 SQL에서 한 줄에 표시되는 주석입니다.
```SQL
SELECT websites.site_name
/* Author: TechOnTheNet.com */
FROM websites;
```
다음은 SQL에서 줄 중간에 표시되는 주석입니다.
```SQL
SELECT  /* Author: TechOnTheNet.com */  websites.site_name
FROM websites;
```
다음은 SQL에서 줄 끝에 표시되는 주석입니다.
```SQL
SELECT websites.site_name  /* Author: TechOnTheNet.com */
FROM websites;
```
혹은
```SQL
SELECT websites.site_name  -- Author: TechOnTheNet.com
FROM websites;
```

---
## 예제 - 여러 줄에 주석 달기
SQL 문에서 여러 줄에 걸친 주석을 만들 수도 있습니다.
```SQL
SELECT websites.site_name
/*
 * Author: TechOnTheNet.com
 * Purpose: To show a comment that spans multiple lines in your SQL statement.
 */
FROM websites;
```
이 주석은 SQL에서 여러 줄에 걸쳐 있으며, 이 예제에서는 4줄에 걸쳐 있습니다.

이 구문을 사용하여 여러 줄에 걸쳐 있는 주석을 만들 수도 있습니다.
```SQL
SELECT websites.site_name /* Author: TechOnTheNet.com
Purpose: To show a comment that spans multiple lines in your SQL statement. */
FROM websites;
```
SQL은 `/*` 기호 뒤에 있는 모든 것이 주석이라고 가정하며, 이는 SQL 문 내에서 여러 줄에 걸쳐 있더라도 `*/` 기호에 도달하기 전까지는 주석으로 간주합니다. 따라서 이 예제에서는 주석이 두 줄에 걸쳐 있습니다.

---
**[< 이전](Indexes.md) / [다음 : LITERALS >](Literals.md)**