---
title: "Logical comparison function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-logical"
---

<span id="c88d96d3"></span>
### **and**

Calculate the logical conjunction between two or more values. Corresponds to the logical AND operator.

**Syntax**

```SQL
and(val1, val2...)
```


**Param**


* `val1, val2, ...`— A list of at least two values. Int, UInt, Float, or Nullable.


**Return value**


* `0`, if there is at least one zero value param.

* `NULL`, if there are no zero\-parameters and there is at least one `NULL` parameter.

* `1`, in other cases.


Type: UInt8 or Nullable(UInt8).

**Example**

```SQL
SELECT and(0, 1, -2);
```


```Plain
┌─and(0, 1, -2)─┐
│ 0             │
└───────────────┘
```


and `NULL`:

```SQL
SELECT and(NULL, 1, 10, -2);
```


```Plain
┌─and(NULL, 1, 10, -2)─┐
│ ᴺᵁᴸᴸ                 │
└──────────────────────┘
```


<span id="bc0080cd"></span>
### or

Calculates the logical OR result between two or more values. Corresponds to the logical OR operator.

**Syntax**

```SQL
or(val1, val2...)
```


**Parameter**


* `val1, val2, ...`— A list with at least two values. Type, UInt, Float, or Nullable.


**Return value**


* `1`, if there is at least one non\-zero value.

* `0`, if there are only zero values.

* `NULL`, if there are only zero values and `NULL`.


Type: UInt8 or Nullable(UInt8).

**Example**

```SQL
SELECT or(1, 0, 0, 2, NULL);
```


```Plain
┌─or(1, 0, 0, 2, NULL)─┐
│ 1                    │
└──────────────────────┘
```


<span id="343db1ac"></span>
### xor

Calculate the logical exclusive OR result between two or more values. For two or more values, the function calculates the first two using `XOR`, then uses the result with the next value to perform `XOR`, and so on.

**Syntax**

```SQL
xor(val1, val2...)
```


**Parameter**


* `val1, val2, ...`— A list including at least two values. Int, UInt, Float, or Nullable.


**Return Value**


* `1`, for two values: if one of the values is zero and the other is non\-zero.

* `0`, for two values: if both values are either zero or non\-zero simultaneously.

* `NULL`, if there is at least one `NULL` value.


Type: UInt8 or Nullable(UInt8).

**Example**

```SQL
SELECT xor(0, 1, 1);
```


```Plain
┌─xor(0, 1, 1)─┐
│ 0            │
└──────────────┘
```


And `NULL`:

```SQL
SELECT xor(NULL, 0);
```


```Plain
┌─xor(NULL, 0)─┐
│ ᴺᵁᴸᴸ         │
└──────────────┘
```
