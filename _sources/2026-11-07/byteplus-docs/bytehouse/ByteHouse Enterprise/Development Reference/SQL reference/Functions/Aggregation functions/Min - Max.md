---
title: "Min/Max"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/min-max-function"
---

<span id="64fd37e7"></span>
# argMax
Calculate the `arg` value corresponding to the maximum `val`.
**Syntax**
```SQL
argMax(arg, val)
```

**Param**

* `arg` — Argument.
* `val` — Value.

**Return value**

* The `arg` value corresponding to the maximum `val`.

Type: Match the `arg` type.
**Example**
Input table:
```Plain
┌─user─────┬─salary─┐
│ director │   5000 │
│ manager  │   3000 │
│ worker   │   1000 │
└──────────┴────────┘
```

Search:
```SQL
SELECT argMax(user, salary), argMax(tuple(user, salary), salary) FROM salary;
```

As a result:
```Plain
┌─argMax(user, salary)─┬─argMax(tuple(user, salary), salary)─┐
│ director             │ ('director',5000)                   │
└──────────────────────┴─────────────────────────────────────┘
```

<span id="9ba69714"></span>
# argMin
Syntax: `argMin(arg, val)` or `argMin(tuple(arg, val))`
Calculate the `val` with the lowest corresponding `arg` value.
**Example:**
Input table:
```Plain
┌─user─────┬─salary─┐
│ director │   5000 │
│ manager  │   3000 │
│ worker   │   1000 │
└──────────┴────────┘
```

Search:
```SQL
SELECT argMin(user, salary), argMin(tuple(user, salary), salary) FROM salary;
```

As a result:
```Plain
┌─argMin(user, salary)─┬─argMin(tuple(user, salary), salary)─┐
│ worker               │ ('worker',1000)                     │
└──────────────────────┴─────────────────────────────────────┘
```

<span id="01af26a0"></span>
# Max
Calculate Maximum.
<span id="min"></span>
# Min
Calculate Low.
