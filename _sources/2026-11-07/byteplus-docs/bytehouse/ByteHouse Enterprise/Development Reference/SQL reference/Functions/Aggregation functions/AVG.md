---
title: "AVG"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/avg-function"
---

<span id="avg"></span>
# avg
Calculate the arithmetic average.
**Syntax**
```sql
avg(x)
```

**Param**

* `x` — Enter a value, must be `Integer`, `Float`, or `Decimal`.

**Return value**

* The arithmetic average, always of Float64 type.
* If the input parameter `x` is empty, return `NaN`.

**Example**
Search:
```sql
SELECT avg(x) FROM values('x Int8', 0, 1, 2, 3, 4, 5);
```

As a result:
```text
┌─avg(x)─┐
│    2.5 │
└────────┘
```

**Example**
Create a temporary table:
Search:
```sql
CREATE table test (t UInt8) ENGINE = Memory;
```

Calculate the arithmetic average value:
Search:
```Plain
SELECT avg(t) FROM test;
```

As a result:
```text
┌─avg(x)─┐
│    nan │
└────────┘
```

<span id="avgweighted"></span>
# avgWeighted
Calculate [the weighted arithmetic average value](https://en.wikipedia.org/wiki/Weighted_arithmetic_mean).
**Grammar**
```sql
avgWeighted(x, weight)
```

**Param**

* `x` — Value.
* `weight` — Weighted value.

`x` and `weight` must be `Integer`, `Float`, or `Decimal`, but they can differ.
**Return value**

* `NaN`. If all weights are zero or if the provided weight parameter is empty.
* Weighted average value.

Type: always Float64.
**Example**
Search:
```sql
SELECT avgWeighted(x, w)
FROM values('x Int8, w Int8', (4, 1), (1, 0), (10, 2))
```

As a result:
```text
┌─avgWeighted(x, weight)─┐
│                      8 │
└────────────────────────┘
```

**Example**
Search:
```sql
SELECT avgWeighted(x, w)
FROM values('x Int8, w Int8', (0, 0), (1, 0), (10, 0))
```

As a result:
```text
┌─avgWeighted(x, weight)─┐
│                    nan │
└────────────────────────┘
```

**Example**
Search:
```sql
CREATE table test (t UInt8) ENGINE = Memory;
SELECT avgWeighted(t) FROM test
```

As a result:
```text
┌─avgWeighted(x, weight)─┐
│                    nan │
└────────────────────────┘
```
