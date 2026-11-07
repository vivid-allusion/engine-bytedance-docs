---
title: "groupArray"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grouparray-function"
---

**syntax**
```SQL
groupArray(x)
```

or
```SQL
groupArray(max_size)(x)
```

Create an array with a parameter value.
Values can be added to the array in any (uncertain) order.
The second usage (with `max_size` parameter) limits the size of the result array to `max_size` items. For example, `groupArray (1) (x)` is equivalent to `[any (x)]`.
In some cases, you can still rely on the execution order. This applies to SELECT (query) from scenarios using an `ORDER BY` sub-query.
