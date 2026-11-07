---
title: "Unique Key table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/unique-key-table"
---

ByteHouse CDW’s CnchMergeTree table engine supports setting a unique key (UNIQUE KEY) upon table creation, creating a unique key table. This article introduces the capabilities and usage examples of the unique key table.

<span id="e57ee866"></span>
# Capability overview

The unique key table refers to a CnchMergeTree table specified with a unique key (UNIQUE KEY), featuring the following characteristics:


* User configures a unique key through UNIQUE KEY, supporting upsert update writes semantics, and automatically returns the latest value for each unique key during queries.

* While ensuring real\-time update capabilities, it still maintains high query performance.

* The unique key (UNIQUE KEY) supports multiple fields and expressions.

* The unique key table supports various deduplication granularities, such as partition\-level deduplication and bucket deduplication.

* Supports custom version fields and automatically ignores them when writing to a lower version.

* Supports real\-time data deletion based on UNIQUE KEY.

* Supports partial column updates based on UNIQUE KEY.


<span id="faee518f"></span>
## Comparison of capabilities between tables with unique keys and tables without unique keys


|Contrast Items |Unique Key Table |Non\-unique Key Table |
|---|---|---|
|Unique Key Constraint |Guarantees |Does not guarantee |
|[Update statement (UPDATE)](https://docs.byteplus.com/docs/bytehouse/update-statement) |Support project |Not supported sync update<br><br>Asynchronous updates can be carried out using the alter statement |
|[DELETE statement (DELETE)](https://docs.byteplus.com/docs/bytehouse/delete-statement) |Support project |Not supported sync delete<br><br>Asynchronous deletes can be carried out using the alter statement |
|[Partial column update](https://docs.byteplus.com/docs/bytehouse/partial-column-update) |Support project |Not supported |
|UPSERT /[INSERT THROW](https://docs.byteplus.com/docs/bytehouse/insert-statement#16a2fc23)/[INSERT IGNORE](https://docs.byteplus.com/docs/bytehouse/insert-statement#2c3c55f2) |Support<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using a table with unique keys for insert operations, it defaults to upsert semantics, i.e., retains the latest value for each unique key.</div><br> |Not supported |


<span id="f750d2e0"></span>
## Types supported by unique keys


|Common Unique Key Field Types |Other Unique Key Field Types |
|---|---|
|String, UInt8, UInt16, UInt32, UInt64, Int8, Int16, Int32, Int64 |Decimal32, Decimal64, Date, Date32, DateTime, DateTime64, Time |



1. Unique Key supports using nullable key, which requires adding `settings allow_nullable_key = 1` when use this feature. Additionally, the embedded data type of `Nullable` must be one of the aforementioned data types supported by Unique Key, such as `Nullable(UInt32)`.

2. If you want to use a field type that is not supported as a unique key field, you can try using `sipHash128()` on the corresponding field type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>sipHash128</code> is a fast hash function with a low collision rate, and no hash collisions have been encountered in practice.</div>


<span id="77a3ecde"></span>
# Deduplication granularity: partition\-level unique & bucket unique

The default ByteHouse unique key table provides partition\-level uniqueness for deduplication. When the columns needed for cluster by are a subset of the columns needed for the unique key field, the deduplication granularity can be optimized to bucket uniqueness. Different deduplication granularities can limit the volume of data awaiting deduplication at the metadata level, thereby meeting different user writing demands:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When writing to a unique key table, it is necessary to find the original location of each record via the unique key. Thus, the more duplicate existing data rows there are, the lower the writing rps; typically, with 50,000,000 existing data rows, the writing rps is 20,000.</div>



|Contrast Items |Partition\-level unique + non\-bucket duplication optimization |Partition\-level uniqueness optimization plus bucket deduplication |
|---|---|---|
|Deduplication description |Partition\-level deduplication, new data will be deduplicated against all existing data in the corresponding partition. |Partition\-level bucket deduplication, new data will be deduplicated against existing data in the same bucket within the corresponding partition. |
|Example of deduplicating inventory data |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a641ab59e95945f6bf59ff1cacac2fb6~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Deduplication granularity at partition level<br><br>* New data's partition = 2020\-10\-29 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/221312e57c144212a7a3b00aa58124dd~tplv-goo7wpa0wc-image.image) </span><br><br>**The required columns for 'cluster by' are a subset of those required for the unique key field**<br><br>In the legend:<br><br><br>* Deduplication granularity at the bucket level<br><br>* The quantity of buckets is 5<br><br>* The partition for newly written data is 2020\-10\-29<br><br>* The bucket for newly written data is 0 |


<span id="72116d3e"></span>
# Principle of data deletion/update

Unique key tables use a Delete\-and\-Insert strategy. When new update data arrives, it finds the original location of each record using the unique key, marks the record as deleted, and then writes the latest data as a new record into a new data file. During reading, according to the delete mark, the old version of the data that has been deleted is filtered out, thereby retrieving the latest values of the unique key.

For example, in the following example, the table is uniquely partitioned with PK as partition key, UK as unique key, and delete bitmap as the delete marker column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e444a0fe4aed472980bba32fcc6c2fbb~tplv-goo7wpa0wc-image.image) </span>

Records in the delete bitmap column marked as 1 are identified as deleted, and after incremental data writing, the latest data is:

```SQL
2020-10-29，1，m
*2020-10-29，2，n
*2020-10-30，1，z
*2020-10-30，2，k
```


<span id="7c359e7b"></span>
# Usage restrictions

Unique key tables, due to their deduplication feature, have the following usage restrictions for efficient data writing according to the quantity of data and the number of Unique Keys:


* Suggestion: Do not set more than 5 fields in the Unique Key. If multiple fields combine to form a unique key, the sipHash64 hash of these can be used as the unique key.

* Suggestion: Control the data quantity of the deduplication granularity to less than a hundred million.


<span id="9f9c628a"></span>
# Examples

Below are two typical usage examples, you can find more examples at [Best practice for ByteHouse Unique Key tables](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables).

<span id="04b51ee7"></span>
## Partition\-level unique example

```SQL
CREATE TABLE t1
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO t1 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men's wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men's wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men's wear', 1, 100);

-- Writing data with the same key enables data update (with upsert semantics).
INSERT INTO t1 VALUES
('2020-10-29 23:50:00', 10002, 'Beijing', 'men's wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men's wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men's wear', 1, 100),
('2020-10-30 00:00:05', 10001, 'Beijing', 'men's wear', 1, 100),
('2020-10-30 00:00:05', 10002, 'Beijing', 'men's wear', 2, 200);

-- Queries automatically return the latest data for each key.
select * from t1 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category───┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men's wear │      5 │     500 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men's wear │      4 │     400 │
│ 2020-10-29 23:50:00 │      10003 │ Beijing │ men's wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men's wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10001 │ Beijing │ men's wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10002 │ Beijing │ men's wear │      2 │     200 │
└─────────────────────┴────────────┴─────────┴────────────┴────────┴─────────┘
```


<span id="5394e7c7"></span>
## Partition\-level unique + bucket unique example

When the volume of data in a partition with a unique key table reaches a certain scale, it affects the writing efficiency. At this point, using cluster by to distribute the partition\-level data volume to different buckets can achieve a partition\-level unique effect when the columns required by cluster by are all contained in the unique key, meanwhile enjoying the optimization of bucket uniqueness.

```SQL
CREATE TABLE t2
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
CLUSTER BY product_id INTO 10 BUCKETS
UNIQUE KEY product_id;

INSERT INTO t2 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men's wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men's wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men's wear', 1, 100);

-- Writing data with the same key enables data update (with upsert semantics).
INSERT INTO t2 VALUES
('2020-10-29 23:50:00', 10002, 'Beijing', 'men's wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men's wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men's wear', 1, 100),
('2020-10-30 00:00:05', 10001, 'Beijing', 'men's wear', 1, 100),
('2020-10-30 00:00:05', 10002, 'Beijing', 'men's wear', 2, 200);

-- Queries automatically return the latest data for each key.
select * from t2 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category───┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men's wear │      5 │     500 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men's wear │      4 │     400 │
│ 2020-10-29 23:50:00 │      10003 │ Beijing │ men's wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men's wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10001 │ Beijing │ men's wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10002 │ Beijing │ men's wear │      2 │     200 │
└─────────────────────┴────────────┴─────────┴────────────┴────────┴─────────┘
```
