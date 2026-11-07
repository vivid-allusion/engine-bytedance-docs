---
title: "Comparison function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-comparison"
---

<span id="ecda0744"></span>
### greatest

Returns the maximum between a and b.

**Syntax**

```SQL
greatest(a, b)
```


**Param**


* `a,b` \- The two values to compare


**Return Value**


* The larger value between a and b.


**Example**

```SQL
SELECT greatest(1, 2)
```


```Plain
┌─greatest(1, 2)─┐
│ 2              │
└────────────────┘
```


```SQL
SELECT greatest(toDate('2019-01-01'), toDate('2019-01-02'))
```


```Plain
┌─greatest(toDate('2019-01-01'), toDate('2019-01-02'))─┐
│ 2019-01-02                                           │
└──────────────────────────────────────────────────────┘
```


<span id="e6e6dc0a"></span>
### notEquals

The operators notEquals, a != b, and a <\> b

**Syntax**

```SQL
notEquals(a, b)
a!=b
a<>b
```


**Param**


* `a, b` \- the two values to compare


**Return value**


* UInt8


**Example**

```SQL
SELECT notEquals(1, 1), 1!=1, 1<>1
```


```Plain
┌─notEquals(1, 1)─┬─notEquals(1, 1)─┬─notEquals(1, 1)─┐
│ 0               │ 0               │ 0               │
└─────────────────┴─────────────────┴─────────────────┘
```


```SQL
SELECT notEquals(1, 2), 1!=2, 1<>2
```


```Plain
┌─notEquals(1, 2)─┬─notEquals(1, 2)─┬─notEquals(1, 2)─┐
│ 1               │ 1               │ 1               │
└─────────────────┴─────────────────┴─────────────────┘
```
