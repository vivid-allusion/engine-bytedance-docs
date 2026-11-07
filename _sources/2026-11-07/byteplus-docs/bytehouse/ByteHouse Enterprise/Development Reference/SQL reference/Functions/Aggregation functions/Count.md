---
title: "Count"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/count-function"
---

<span id="count"></span>
# count
Calculate the number of lines or non-empty values.
ClickHouse supports the following `count` syntax:

* `count(expr)` or `COUNT(DISTINCT expr)`.
* `count()` or `COUNT(*)`. The `count()` syntax is specific to ClickHouse.

**Param**
This function can accept the following parameters:

* Zero parameters.
* An expression.

**Return value**

* If the function is called without parameters, it calculates the number of rows.
* If an expression is passed, the function counts the number of times this expression returns a non-null result. If the expression returns a value of type Nullable, the `count` result is still not `Nullable`. If the expression returns `NULL` for all rows, the function returns 0.

In both cases, the return type is UInt64.
**Details**
ClickHouse supports the syntax `COUNT(DISTINCT ...)`, and the behavior of this structure depends on the count_distinct_implementation settings. It defines the uniq* functions used to execute the operation. The default value is uniqExact function.
`SELECT count() FROM table` This search has not been optimized because the number of entries in the table is not stored separately. It selects a small column from the table and calculates the number of its values.
**Example**
Example 1:
```sql
SELECT count() FROM t
```

```text
┌─count()─┐
│       5 │
└─────────┘
```

Example 2:
```sql
SELECT name, value FROM system.settings WHERE name = 'count_distinct_implementation'
```

```text
┌─name──────────────────────────┬─value─────┐
│ count_distinct_implementation │ uniqExact │
└───────────────────────────────┴───────────┘
```

```sql
SELECT count(DISTINCT num) FROM t
```

```text
┌─uniqExact(num)─┐
│              3 │
└────────────────┘
```

This example shows that `count(DISTINCT num)` is run by setting value uniqExact in the count_disti`uniqExact in the count_distinct_implementation` settings.
