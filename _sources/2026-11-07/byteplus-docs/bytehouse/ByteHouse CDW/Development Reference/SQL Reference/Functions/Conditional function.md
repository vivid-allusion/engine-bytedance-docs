---
title: "Conditional function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-conditional"
---

<span id="7716c3d5"></span>
### multiIf

Allows you to write the CASE operator more compactly in a query.

**Syntax**

```SQL
multiIf(cond_1, then_1, cond_2, then_2, ..., else)
```


**Parameters:** 


* `cond_N`— The condition `then_N` that the function returns.

* `then_N`— The result when the function runs.

* `else`— The result of the function if no conditions are satisfied.


The function accepts `2N+1` parameters.

**Return value** The function's result based on conditions

Return one of the values `then_N` or. `elsecond_N`

**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionMultiIf (id UInt8, left Nullable(UInt8), right Nullable(UInt8)) ENGINE=CnchMergeTree ORDER BY id;
INSERT INTO test.functionMultiIf VALUES (1,NULL,4),(2,1,3),(3,2,2),(4,3,1),(5,4,NULL);
SELECTleft,right,
    multiIf(left < right, 'left is smaller', left > right, 'left is greater', left = right, 'Both equal', 'Null value') AS resultFROM test.functionMultiIf
```


```Plain
┌─left─┬─right─┬─result──────────┐
│ ᴺᵁᴸᴸ │ 4     │ Null value      │
│ 1    │ 3     │ left is smaller │
│ 2    │ 2     │ Both equal      │
│ 3    │ 1     │ left is greater │
│ 4    │ ᴺᵁᴸᴸ  │ Null value      │
└──────┴───────┴─────────────────┘
```
