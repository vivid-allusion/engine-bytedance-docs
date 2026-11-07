---
title: "groupBitXor"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitxor-function"
---

<span id="6cf69c8b"></span>
# groupBitXor
Apply `XOR` bit-wise on the number sequence.
**Syntax**
```SQL
groupBitXor(expr)
```

**Parameters**
`expr` – Expression that results in a `UInt*` type.
**Return value**
`UInt*` type value.
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
SELECT groupBitXor(num) FROM t 
```

`num` is the column that contains Attributable event name.
As a result:
```Plain
binary     decimal
01101000 = 104
```
