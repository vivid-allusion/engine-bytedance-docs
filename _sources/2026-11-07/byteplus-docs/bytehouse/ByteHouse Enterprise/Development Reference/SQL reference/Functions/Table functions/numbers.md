---
title: "numbers"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/numbers-function"
---

`numbers(N)` – Returns a table containing a single 'number' column (UInt64) that includes integers from 0 to N-1.
`numbers(N, M)` - Returns a table containing a single 'number' column (UInt64) with integers from N to (N+M-1).
Similar to `system.numbers` table, which can be used for tests and generating consecutive values, `numbers(N, M)` is more efficient compared with `system.numbers`.
The following queries are equivalent:
```sql
SELECT * FROM numbers(10);
SELECT * FROM numbers(0, 10);
SELECT * FROM system.numbers LIMIT 10;
```

Example:
```sql
-- Generate a date sequence from January 1st, 2010 to December 31st, 2010
select toDate('2010-01-01') + number as d FROM numbers(365);
```
