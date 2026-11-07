---
title: "arrayJoin function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/arrayjoin-function"
---

This is a very useful function.
Normal functions do not change the number of rows in the result set but calculate the values in each row (map). Aggregate functions compress multiple rows into one row (fold or reduce). The 'arrayJoin' function takes each row and expands them into multiple rows (unfold).
This function takes an array as a parameter and copies that row in the result set for each array element. In addition to the values in the column where this function is applied, simply copy all the values in the column; they are replaced by the corresponding array values.
Queries can use multiple `arrayJoin` functions. In this case, the transformation is performed multiple times.
Please note the ARRAY JOIN syntax in SELECT queries, which offers a wider range of possibilities.
Example:
SELECT arrayJoin([1, 2, 3] AS src) AS dst, 'Hello', src
```plaintext
┌─dst─┬─\'Hello\'─┬─src─────┐
│   1 │ Hello     │ [1,2,3] │
│   2 │ Hello     │ [1,2,3] │
│   3 │ Hello     │ [1,2,3] │
└─────┴───────────┴─────────┘
```
