---
title: "groupUniqArray"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/groupuniqarray-function"
---

<span id="de32764e"></span>
# groupUniqArray
**Grammar**
```SQL
groupUniqArray(x)或groupUniqArray(max_size)(x)
```

Create an array from different parameter values. Memory consumption is the same as the uniqExact function.
The second version (with `max_size` param) limits the size of the result array to `max_size` items. For example, `groupUniqArray(1)(x)` is equivalent to `[any(x)]`.
