---
title: "Bit Operation Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bit-operation-function"
---

<span id="1f58f201"></span>
### bitTest

Take any integer and convert it to [binary form].

**Syntax**

```SQL
SELECT bitTest(number, index)
```


**Param**


* `number` – Integer.

* `index` – Position of the bit.


**Return Value**

Returns the bit value at the specified position.

Type: `UInt8`.

**Example**

For instance, in the binary number system, the number 43 is 101011.

```SQL
SELECT bitTest(43, 1);
```


As a result:

```Plain
┌─bitTest(43, 1)─┐
│ 1              │
└────────────────┘
```


Another example:

```SQL
SELECT bitTest(43, 2);
```


As a result:

```Plain
┌─bitTest(43, 2)─┐
│ 0              │
└────────────────┘
```


<span id="926a88b6"></span>
### bitTestAll

Returns the AND Operation result for all bits at the given location. From right to left, counting starts from 0.

Association of bitwise operations:

0 and 0 = 0

0 and 1 = 0

1 and 0 = 0

1 and 1 = 1

**Syntax**

```SQL
SELECT bitTestAll(number, index1, index2, index3, index4, ...)
```


**Parameter**


* `number` – integer.

* `index1`, `index2`, `index3`, `index4` – positions of digits. For example, for the set of positions ( `index1`, `index2`, `index3`, `index4`) it's true if and only if all positions are true ( `index1`⋀ `index2`⋀ `index3`⋀ `index4`).


**Return value**

Returns the result of the logical connective.

Type: `UInt8`.

**Example:** 

For example, the number 43 in the binary number system is 101011.

```SQL
SELECT bitTestAll(43, 0, 1, 3, 5);
```


Result:

```Plain
┌─bitTestAll(43, 0, 1, 3, 5)─┐
│ 1                          │
└────────────────────────────┘
```


Another example:

```SQL
SELECT bitTestAll(43, 0, 1, 3, 5, 2);
```


Result:

```Plain
┌─bitTestAll(43, 0, 1, 3, 5, 2)─┐
│ 0                             │
└───────────────────────────────┘
```


<span id="d00f15d2"></span>
### bitTestAny

Returns the result of the logical OR (or operator) for all bits at the given position. From right to left, counting starts from 0.

Disjunction in bitwise operations:

0 or 0 = 0

0 or 1 = 1

1 or 0 = 1

1 or 1 = 1

**Grammar**

```SQL
SELECT bitTestAny(number, index1, index2, index3, index4, ...)
```


**Param**


* `Number` – Integer.

* `Index1`, `Index2`, `Index3`, `Index4` – Position of digits.


**Return value**

Returns the result of the logical decomposition.

Type: `UInt8`.

**Example:** 

For instance, the number 43 in the binary digit system is 101011.

```SQL
SELECT bitTestAny(43, 0, 2);
```


As a result:

```Plain
┌─bitTestAny(43, 0, 2)─┐
│ 1                    │
└──────────────────────┘
```


Another example:

```SQL
SELECT bitTestAny(43, 4, 2);
```


As a result:

```Plain
┌─bitTestAny(43, 4, 2)─┐
│ 0                    │
└──────────────────────┘
```
