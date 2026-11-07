---
title: "argMax/argMin"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/argMax-argMin-function"
---

<span id="835bf5a9"></span>
# argMax
Calculate the `arg` value corresponding to the maximum `val`.
**Syntax**
```SQL
argMax(arg, val)
```

**Parameter**

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

Result:
```Plain
┌─argMax(user, salary)─┬─argMax(tuple(user, salary), salary)─┐
│ director             │ ('director',5000)                   │
└──────────────────────┴─────────────────────────────────────┘
```

<span id="1122111f"></span>
# argMin
Syntax: `argMin(arg, val)` or `argMin(tuple(arg, val))`
Calculate the arg value corresponding to the minimum val.`arg value corresponding to the minimum val`.
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

As a result
```Plain
┌─argMin(user, salary)─┬─argMin(tuple(user, salary), salary)─┐
│ worker               │ ('worker',1000)                     │
└──────────────────────┴─────────────────────────────────────┘
```
