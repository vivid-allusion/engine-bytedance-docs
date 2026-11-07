---
title: "groupArraySample"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grouparraysample-function"
---

<span id="24c9676f"></span>
# groupArraySample
Build a sampling array of parameter values. The size of the result array is limited to `max_size` elements. Parameter values are randomly selected and added to the array.
**Grammar**
```SQL
groupArraySample(max_size[, seed])(x)
```

**Param**

* `max_size` — Maximum length of the result array. UInt64。
* `Seed` — Seed for the random number generator. Optional. UInt64。 Default: `123456`.
* `x` — Parameter (column name or expression).

**Return value**

* Randomly selects an array composed of the `x` values.

Type: Array.
**Example**
Sample table `colors`:
```Plain
┌─id─┬─color──┐
│  1 │ red    │
│  2 │ blue   │
│  3 │ green  │
│  4 │ white  │
│  5 │ orange │
└────┴────────┘
```

Use column names as parameters for search:
```SQL
SELECT groupArraySample(3)(color) as newcolors FROM colors; 
```

As a result:
```Plain
┌─newcolors──────────────────┐
│ ['red','orange','green']   │
└────────────────────────────┘
```

Search using column names and different (random numbers) seeds:
```SQL
SELECT groupArraySample(3, 987654321)(color) as newcolors FROM colors; 
```

As a result:
```Plain
┌─newcolors──────────────────┐
│ ['red','orange','green']   │
└────────────────────────────┘
```

Search using expressions as parameters:
```SQL
SELECT groupArraySample(3)(concat('light-', color)) as newcolors FROM colors; 
```

As a result:
```Plain
┌─newcolors───────────────────────────────────┐
│ ['light-blue','light-orange','light-green'] │
└─────────────────────────────────────────────┘
```
