---
title: "groupBitAnd"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitand-function"
---

<span id="025af4ec"></span>
# groupBitAnd
Apply bitwise `AND` to the number sequence.
**Syntax**
```SQL
groupBitAnd(expr)
```

**Parameters**
`expr` – An expression resulting in a `UInt*` type.
**Return value**
A value of `UInt*` type.
**Example**
Attributable event name:
```Plain
binary     decimal
00101100 = 44
00011100 = 28
00001101 = 13
01010101 = 85
```

Search:
```SQL
SELECT groupBitAnd(num) FROM t 
```

`num` is the column that contains test data.
As a result:
```Plain
binary     decimal
00000100 = 4
```
