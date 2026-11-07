---
title: "TopK"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/topk-function"
---

<span id="topk"></span>
# topK
Returns an array of the most frequently occurring values in a specified column, approximately. The generated array is sorted in descending order by the approximate frequency of values, not by the values themselves.
Implements a [space-saving filter](http://www.l2f.inesc-id.pt/~fmmb/wiki/uploads/Work/misnis.ref0a.pdf) algorithm, using a reduce-and-combine-based algorithm, inspired by [parallel space-saving](https://arxiv.org/pdf/1401.0702.pdf).
**Syntax**
```sql
topK(N)(x)
```

This function does not guarantee results. In some cases, an error might occur, and values that are not the most frequent may be returned.
We recommend using `N < 10` values. The larger the `N`, the lower the performance. Maximum `N = 65536`.
**Param**

* `N` — the number of elements to return.

If this parameter is omitted, the default value of 10 is used.
**Param**

* `x` – the value to calculate frequency.

**Example**
Take the [OnTime](https://clickhouse.com/docs/getting-started/example-datasets/ontime) dataset for example, select the three most frequent from the `AirlineID` column.
```sql
SELECT topK(3)(AirlineID) AS res
FROM ontime
```

```text
┌─res─────────────────┐
│ [19393,19790,19805] │
└─────────────────────┘
```

<span id="topkweighted"></span>
# topKWeighted
Similar to `topK` but requires an additional integer parameter - `weight`. Each input is counted multiple times toward frequency calculation based on the `weight`.
**Syntax**
```sql
topKWeighted(N)(x, weight)
```

**Param**

* `N` — Number of elements to return.

**Param**

* `x` – Value to calculate frequency.
* `weight` — Weight. UInt8 Type.

**Return value**
Returns an array of values with the maximum approximate weight sum.
**Example**
Search:
```sql
SELECT topKWeighted(10)(number, number) FROM numbers(1000) 
```

As a result:
```text
┌─topKWeighted(10)(number, number)──────────┐
│ [999,998,997,996,995,994,993,992,991,990] │
└───────────────────────────────────────────┘
```
