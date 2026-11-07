---
title: "initializeAggregation"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/initializeaggregation-function"
---

Initialize the aggregation for your input rows. For functions with a suffix `State`.
Use it to test or handle columns of `AggregateFunction` and `AggregationMergeTree` types.
**Syntax**
```sql
initializeAggregation (aggregate_function, column_1, column_2)
```

**Parameters**
`aggregate_function` — Name of the aggregation function. The state of this function — currently being created. String type.
`column_n` — Column to be converted into the function's parameter. String type.
**Return value**
Returns the aggregated result of the input line. The return type will be the same as the return type of the function used as the first argument in `initializeAgregation`.
For example, for functions with suffix `State`, the return type will be `AggregateFunction`.
**Example**
Query:
```sql
SELECT uniqMerge(state) FROM (SELECT initializeAggregation('uniqState', number % 3) AS state FROM system.numbers LIMIT 10000);
```

Result:
```SQL
┌─uniqMerge(state)─┐
│ 3                │
└──────────────────┘
```
