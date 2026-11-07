---
title: "ANY"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/any-function"
---

<span id="any"></span>
# any
Choose the first encountered value.
Queries can be executed in any order, and even in a different order each time. Therefore, the result of this function is indeterminate. 
To obtain definite results, you can use the 'Min' or 'Max' function instead of 'any'.
In some cases, it is possible to rely on the execution order. This applies to the case where a SELECT from a subquery using ORDER BY is used.
When a `SELECT` query contains a `GROUP BY` clause or at least one aggregate function, ClickHouse (compared to MySQL) requires all expressions `SELECT`, `HAVING`, and `ORDER BY` clauses to be calculated from keys or aggregate functions. In other words, every column selected from the table must be used within a key or an aggregate function. To achieve behavior similar to that of MySQL, you can place other columns in the `any` aggregate function. 
<span id="anyheavy"></span>
# anyHeavy
Select a frequently occurring value using the [heavy hitters](http://www.cs.umd.edu/~samir/498/karp.pdf) algorithm. If a value appears in more than half of the execution threads of the search, then return this value. Usually, the result is indeterminate.
```sql
anyHeavy(column)
```

**Parameter**

* `column` – The column name。

**Example**
Use the [OnTime](https://clickhouse.com/docs/zh/getting-started/example-datasets/ontime) dataset and select any frequently occurring value in the `AirlineID` column.
Search:
```sql
SELECT anyHeavy(AirlineID) AS res
FROM ontime;
```

Result:
```text
┌───res─┐
│ 19690 │
└───────┘
```

<span id="anylast"></span>
## anyLast
Select the last encountered value.
The result is as uncertain as the any function.
