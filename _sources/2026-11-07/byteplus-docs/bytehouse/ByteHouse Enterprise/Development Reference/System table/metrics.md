---
title: "metrics"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/metrics"
---

The system table `metrics` include those that can be calculated instantly or have a current value. For example, the number of queries processed simultaneously or the current replica latency. This table is always up to date. You can find all supported metrics in the source file [src/Common/CurrentMetrics.cpp](https://github.com/ClickHouse/ClickHouse/blob/master/src/Common/CurrentMetrics.cpp).

<span id="16f63042"></span>
## Column name


|**Name** |**Data type** |**Description of field meanings** |
|---|---|---|
|metric |String |Metric name. |
|value |Int64 |Metric value. |
|description |String |Metric description. |


<span id="f5899634"></span>
## **Example**

```SQL
SELECT * FROM system.metrics LIMIT 10 
```


```SQL
┌─metric───────────────────────────────┬─value─┬─description────────────────────────────────────────────────────────────┐
│ Query                                │     1 │ Number of executing queries                                            │
│ Merge                                │     0 │ Number of executing background merges                                  │
│ PartMutation                         │     0 │ Number of mutations (ALTER DELETE/UPDATE)                              │
│ ReplicatedFetch                      │     0 │ Number of data parts being fetched from replicas                       │
│ ReplicatedSend                       │     0 │ Number of data parts being sent to replicas                            │
│ ReplicatedChecks                     │     0 │ Number of data parts checking for consistency                          │
│ BackgroundMergesAndMutationsPoolTask │     0 │ Number of active merges and mutations in an associated background pool │
│ BackgroundFetchesPoolTask            │     0 │ Number of active fetches in an associated background pool              │
│ BackgroundCommonPoolTask             │     0 │ Number of active tasks in an associated background pool                │
│ BackgroundMovePoolTask               │     0 │ Number of active tasks in BackgroundProcessingPool for moves           │
└──────────────────────────────────────┴───────┴────────────────────────────────────────────────────────────────────────┘
```
