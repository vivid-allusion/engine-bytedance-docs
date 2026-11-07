---
title: "Conditional Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/conditional-function"
---

<span id="if"></span>
## if
Control the conditional branches. Unlike most systems, ClickHouse always evaluates the two expressions `then` and `else`.
Syntax
SELECT if(cond, then, else)
If the calculation result of the condition `cond` is non-zero, it returns the result of the expression `then` and skips the result of the expression `else` (if it exists). If `cond` is zero or `NULL`, it skips the result of the `then` expression and returns the result of the `else` expression (if it exists).
Parameters

* `cond` – The result of the condition can be zero or non-zero. The type is UInt8, Nullable(UInt8), or NULL.
* `then` - Expression returned if the condition is satisfied.
* `else` - Expression returned if the condition is not satisfied.

Return value
This function executes `then` and `else` expressions and returns their results, depending on whether the `cond` ultimately equals zero.
Example
Search:
SELECT if(1, plus(2, 2), plus(2, 6))
As a result:
```plaintext
┌─plus(2, 2)─┐
│          4 │
└────────────┘
```

Search:
```SQL
SELECT if(0, plus(2, 2), plus(2, 6))
```

As a result:
```plaintext
┌─plus(2, 6)─┐
│          8 │
└────────────┘
```


* `Then` and `else` must have the lowest common type.

Example:
Given table `LEFT_RIGHT`:
```SQL
SELECT *FROM LEFT_RIGHT 
┌─left─┬─right─┐ 
│ ᴺᵁᴸᴸ │ 4     │ 
│ 1    │ 3     │ 
│ 2    │ 2     │ 
│ 3    │ 1     │ 
│ 4    │ ᴺᵁᴸᴸ  │ 
└──────┴───────┘
```

The following query compares the values of `left` and `right`:
```SQL
SELECT left, right, if(left < right, 'left is smaller than right', 'right is greater or equal than left') 
AS is_smaller 
FROM LEFT_RIGHT 
WHERE isNotNull(left) AND isNotNull(right) 
┌─left─┬─right─┬─is_smaller──────────────────────────┐ 
│ 1    │ 3     │ left is smaller than right.         │ 
│ 2    │ 2     │ right is greater or equal than left │ 
│ 3    │ 1     │ right is greater or equal than left │ 
└──────┴───────┴─────────────────────────────────────┘
```

:::warning
In this example, 'NULL' values were not used, please check the [Conditionale NULL values](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/functions/conditional-functions.md) part.
:::
<span id="三元运算符"></span>
## Ternary Operator
Identical to the `if` function.
Syntax: `cond ?` `then : else` if `cond is not` If `= 0` then return `then`, if `cond = 0` return `else`.

* `cond` must be of `UInt8` type, `then` and `else` must share the lowest common type.

<span id="multiif"></span>
## `then` and `else` can be `NULL`multiIf
Enables you to write [CASE](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/operators/index.md) operators more compactly in queries.
```plaintext
multiIf(cond_1, then_1, cond_2, then_2...else)
```

Parameters:

* `cond_N` — Condition under which the function returns `then_N`.
* `then_N` — the result of the function at runtime.
* `else` — the result of the function when no conditions are met.

The function takes `2N + 1` parameters.
Return value
The function returns either «then_N» or «else», depending on the `cond_N` condition.
Example
Reusing the table `LEFT_RIGHT`.
```SQL
SELECT left, right, multiIf(left < right, 'left is smaller', left > right, 'left is greater', left = right, 'Both equal', 'Null value') 
AS result FROM LEFT_RIGHT 
┌─left─┬─right─┬─result──────────┐ 
│ ᴺᵁᴸᴸ │ 4     │ Null value      │ 
│ 1    │ 3     │ left is smaller │ 
│ 2    │ 2     │ Both equal      │ 
│ 3    │ 1     │ left is greater │ 
│ 4    │ ᴺᵁᴸᴸ  │ Null value      │ 
└──────┴───────┴─────────────────┘
```

<span id="直接使用条件结果-using-conditional-results-directly"></span>
## Use conditional results directly
Conditional results are always `0`, `1`, or `NULL`. Thus, you can directly use conditional results like this.
```SQL
SELECT left < right AS is_small FROM LEFT_RIGHT 
┌─is_small─┐ 
│ ᴺᵁᴸᴸ     │ 
│ 1        │ 
│ 0        │ 
│ 0        │ 
│ ᴺᵁᴸᴸ     │
└──────────┘
```

SELECT left < right AS is_small FROM LEFT_RIGHT ┌─is_small─┐ │ ᴺᵁᴸᴸ │ │ 1 │ │ 0 │ │ 0 │ │ ᴺᵁᴸᴸ │ └──────────┘
<span id="条件中的null值"></span>
## NULL values in conditions
When the condition contains `NULL` values, the result will also be `NULL`.
```SQL
SELECTNULL< 1, 2 < NULL, NULL < NULL, NULL = NULL 
┌─less(NULL, 1)─┬─less(2, NULL)─┬─less(NULL, NULL)─┬─equals(NULL, NULL)─┐ 
│ ᴺᵁᴸᴸ          │ ᴺᵁᴸᴸ          │ ᴺᵁᴸᴸ             │ ᴺᵁᴸᴸ               │ 
└───────────────┴───────────────┴──────────────────┴────────────────────┘
```

Hence, if the type is `Nullable`, you should carefully construct your query.
This example illustrates that point.
```SQL
SELECT left, right, multiIf(left < right, 'left is smaller', left > right, 'right is smaller', 'Both equal') 
AS faulty_result 
FROM LEFT_RIGHT 
┌─left─┬─right─┬─faulty_result────┐ 
│ ᴺᵁᴸᴸ │ 4     │ Both equal       │ 
│ 1    │ 3     │ left is smaller  │ 
│ 2    │ 2     │ Both equal       │ 
│ 3    │ 1     │ right is smaller │ 
│ 4    │ ᴺᵁᴸᴸ  │ Both equal       │ 
└──────┴───────┴──────────────────┘
```
