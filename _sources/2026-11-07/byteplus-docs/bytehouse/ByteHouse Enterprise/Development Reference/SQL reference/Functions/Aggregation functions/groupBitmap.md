---
title: "groupBitmap"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupbitmap-function"
---

<span id="bd57a3d1"></span>
# groupBitmap
Carry on bitmap or aggregate calculations from a column of unsigned integers, returning a value of `UInt64` Type. If a suffix `State` is added, then a bitmap object is returned.
**Example**
```SQL
groupBitmap(expr)
```

**Param**
`expr` – Expression that results is `UInt*` Type.
**Return value**
A value of `UInt64` Type.
**Example**
Attributable event name:
```Plain
UserID
1
1
2
3
```

Search:
```SQL
SELECT groupBitmap(UserID) as num FROM t 
```

As a result:
```Plain
num
3
```
