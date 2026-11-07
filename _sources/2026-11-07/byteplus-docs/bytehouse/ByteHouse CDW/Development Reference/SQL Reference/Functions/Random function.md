---
title: "Random function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-random"
---

<span id="07760514"></span>
### rand

Returns a pseudo\-random UInt32 Number, uniformly distributed among all UInt32 Type numbers.

Use a linear congruential generator.

**Syntax**

```SQL
rand([x])
```


**Param**


* `x`— The result of the Expression can be any supported Data type. The Return Value will be discarded, But if the function is called multiple times in a Search, the Expression itself can be used to bypass common subexpression elimination. Optional Param.


**Return value**


* Pseudo\-random UInt32 number. Type: UInt32


**Example**

```SQL
SELECT rand(), rand(number) FROM numbers(2);
```


```Plain
┌─rand()─────┬─rand(number)─┐
│ 3882830473 │ 2236253349   │
│ 4122795699 │ 3720179576   │
└────────────┴──────────────┘
```


<span id="5d2242d9"></span>
### rand64

Returns a pseudo\-random UInt64 number, which is uniformly distributed among all UInt64 type numbers.

Uses a linear congruential generator.

**Syntax**

```SQL
rand64([x])
```


**Param**


* `x`— The result of the expression is any supported data type. The result will be discarded, but if the function is called multiple times in a query, the expression itself can be used to bypass common subexpression elimination. Optional parameter.


**Return value**


* A pseudo\-random UInt64 number. Type: UInt64


**Example**

```SQL
SELECT rand64(), rand64(number) FROM numbers(2);
```


```Plain
┌─rand64()────────────┬─rand64(number)───────┐
│ 4216084906413806748 │ 17404981640646529534 │
│ 874879808660605772  │ 941470430861381566   │
└─────────────────────┴──────────────────────┘
```


<span id="2f5ec952"></span>
### randConstant

Generates a column with a random value.

**Syntax**

```SQL
randConstant([x])
```


**Param**


* `x` \- The expression result can be any supported data type. The result will be discarded, but if this function is called multiple times in a query, the expression itself can be used to circumvent common subexpression elimination. Optional Param.


**Return value**


* Pseudo\-random number. Type: UInt32.


**Example**

```SQL
SELECT rand(), rand(1), rand(number), randConstant(), randConstant(1), randConstant(number)
FROM numbers(3)
```


```Plain
┌─rand()─────┬─rand(1)────┬─rand(number)─┬─randConstant()─┬─randConstant(1)─┬─randConstant(number)─┐
│ 1617218167 │ 3030783952 │ 3660442590   │ 3335999329     │ 1508515848      │ 1880875990           │
│ 432450540  │ 2987789840 │ 653572307    │ 3335999329     │ 1508515848      │ 1880875990           │
│ 3698169875 │ 79826010   │ 458167070    │ 3335999329     │ 1508515848      │ 1880875990           │
└────────────┴────────────┴──────────────┴────────────────┴─────────────────┴──────────────────────┘
```
