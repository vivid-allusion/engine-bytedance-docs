---
title: "groupBitOr"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitor-function"
---

<span id="130f6ca6"></span>
# groupBitOr
Apply `OR` bit-wise to a sequence of numbers.
**Syntax**
```SQL
groupBitOr(expr)
```

**Parameters**
`Expression` – An expression that results in a `UInt*` type.
**Return value**
`UInt*` type Value.
**Example**
Test data:
```Plain
binary     decimal
00101100 = 44
00011100 = 28
00001101 = 13
01010101 = 85
```

Search:
```SQL
SELECT groupBitOr(num) FROM t 
```

`num` is a column that contains test data.
As a result:
```Plain
binary     decimal
01111101 = 125
```
