---
title: "HaUniqueMergeTree"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hauniquemergetree"
---

The HaUniqueMergeTree, a unique key engine developed by ByteHouse, retains ClickHouse's efficient query performance while supporting primary key updates. It addresses the pain point of the community edition ClickHouse's inability to support efficient update operations, simplifying the development of real-time analytics applications for businesses.
<span id="引擎优势"></span>
# Engine Advantages

1. Users configure the unique key through UNIQUE KEY, providing upsert update semantics, and the queries automatically return the latest value for each unique key. (Compared to the community's ReplacingMergeTree, which requires waiting for a Merge to complete after data import to see deduplicated data, the HaUniqueMergeTree deduplicates immediately after data import).
2. Performance: The single Shard write throughput can generally reach 50,000+ rows/s. For scenarios with massive data, it is recommended to govern data sources and import into different partitions in parallel to achieve linear speed growth.
3. Primary keys support multiple fields and expressions.
4. Supports both partition-level uniqueness and table-level uniqueness modes.
5. Supports custom version fields, automatically ignoring data written with a lower version.
6. Multi-replica deployment, ensuring data reliability through master-slave asynchronous replication.
7. Supports real-time data deletion based on UNIQUE KEY.

<span id="建表示例"></span>
# Table creation example
<span id="sql-建表"></span>
## SQL table creation
<span id="建表语法"></span>
### Table creation syntax
```sql
CREATE TABLE [IF NOT EXISTS] [db.]table_name [ON CLUSTER cluster]
(
    name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1] [TTL expr1],
    name2 [type2] [DEFAULT|MATERIALIZED|ALIAS expr2] [TTL expr2],
    ...
) ENGINE = HaUniqueMergeTree(shard, replica, version_column) -- The default value is '/clickhouse/bytehouse/databasename.tablename/{shard}','{replica}'
PARTITION BY toYYYYMM(EventDate)
ORDER BY expr
[PARTITION BY expr]
UNIQUE KEY expr
[SAMPLE BY expr]
[TTL expr
    [DELETE|TO DISK 'xxx'|TO VOLUME 'xxx' [, ...] ]
    [WHERE conditions]
    [GROUP BY key_expr [SET v1 = aggr_func(v1) [, v2 = aggr_func(v2) ...]] ] ]
[SETTINGS name=value, ...]
```


* Unique Key settings: Supports multiple fields (but does not support Nullable or complex types like Map, Array), and also supports expressions, such as: `UNIQUE KEY (product_id, sipHash64(city))`

:::warning
It is recommended to set no more than five unique keys to avoid potential performance impacts:

1. In scenarios using a memory index, it will occupy a significant amount of memory;
2. This will prolong the serialization and deserialization time of the stored data objects.
:::

* version_column (version field): Select a field as a basis for version control, used for updates based on version, see example 2 for usage. When designing table structures, it is recommended to prioritize partition values as versions to reduce memory usage.

Other field settings, such as `Order By`, `Partition By`, follow the same rules as other engines in the MergeTree family.
<span id="settings"></span>
### Settings options

| | | | | \
|**Parameter Name** |Common Fields |**Default Value** |**Description** |
|---|---|---|---|
| | | | | \
|partition_level_unique_keys |Yes |1 |0: UNIQUE KEY table-level uniqueness |\
| | | |1: UNIQUE KEY partition-level uniqueness |\
| | | |Recommended selection: Prefer partition-level uniqueness (i.e., the default value). If the business semantics requires table granularity uniqueness, consider reducing the number of partitions by setting shorter TTLs and using coarser granularity of partitions (e.g., monthly partitioning). |
| | | | | \
|enable_unique_partial_update |Yes |0 |Allows partial column updates to be written (requires support of new engine version). |
| | | | | \
|enable_disk_based_unique_key_index |Yes |1 |0：in-memory mode。 In this mode, the system maintains an in-memory key index for each unique table, therefore, the supported data volume is limited by memory. |\
| | | |1：disk-based mode。 In this mode, there is no limit on the amount of data, but performance is 10-30% lower than the in-memory mode (the more frequent the data insertion, the greater the decrease in import speed). |\
| | | |Recommendation: It is advised to select in-memory mode when the overall data volume is less than 100 million records per cluster shard; otherwise, choose the disk-based mode. |

<span id="使用示例"></span>
# Usage examples
<span id="668fb72f"></span>
## Example 1: Partition-level unique keys
Assuming the table schema is as follows:
```SQL
-- The engine by default guarantees the uniqueness of the unique key within the partition.
-- Note: The UNIQUE KEY does not support the Nullable type. 
CREATE TABLE t1
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = HaUniqueMergeTree('/clickhouse/default/t1/{shard}', '{replica}')
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;
```

Insert data. At this point, writing data with the same key can realize updates (upsert semantics).
```SQL
INSERT INTO t1 VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

INSERT INTO t1 VALUES
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100),
('2020-10-30 00:00:05', 10001, 'Beijing', 'men wear', 1, 100),
('2020-10-30 00:00:05', 10002, 'Beijing', 'men wear', 2, 200);
```

Queries automatically return the latest data for each key:
```SQL

select * from t1 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing │ men wear │      5 │     500 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men wear │      4 │     400 │
│ 2020-10-29 23:50:00 │      10003 │ Beijing │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10001 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10002 │ Beijing │ men wear │      2 │     200 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘


```

UNIQUE KEY can also include multiple fields and expressions, such as the following with two fields: product_id, sipHash64(city):
```SQL
-- The UNIQUE KEY can contain multiple fields and expressions.
CREATE TABLE t1m
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = HaUniqueMergeTree('/clickhouse/default/t1m/{shard}', '{replica}')
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY (product_id, sipHash64(city));

INSERT INTO t1m VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100),
('2020-10-29 23:50:00', 10002, 'Shanghai', 'men wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100);

select * from t1m;
┌──────────event_time─┬─product_id─┬─city─────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10001 │ Beijing  │ men wear │      5 │     500 │
│ 2020-10-29 23:40:00 │      10002 │ Beijing  │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10003 │ Beijing  │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing  │ men wear │      1 │     100 │
│ 2020-10-29 23:50:00 │      10002 │ Shanghai │ men wear │      4 │     400 │
└─────────────────────┴────────────┴──────────┴──────────┴────────┴─────────┘
```

<span id="例1：表级别唯一键"></span>
## Example 2: Table-level Unique Key
Assuming the table schema is as follows:
```sql
CREATE TABLE t2
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = HaUniqueMergeTree('xxxxxxx')
PARTITION BY toDate(event_time) --Partition field
ORDER BY (city, category) --Order field
UNIQUE KEY product_id --Unique key
SETTINGS partition_level_unique_keys = 0; --Set table-level uniqueness
```

Insert the following test data sequentially:
```sql
INSERT INTO t2 (event_time, product_id, city, category, amount, revenue) VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

INSERT INTO t2 (event_time, product_id, city, category, amount, revenue) VALUES
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 4, 400),
('2020-10-29 23:50:00', 10003, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100),
('2020-10-30 00:00:05', 10001, 'Beijing', 'men wear', 1, 100),
('2020-10-30 00:00:05', 10002, 'Beijing', 'men wear', 2, 200);
```

As seen, the three products 10001, 10002, and 10003 have been updated to the latest data, and both 10001 and 10002 have been updated from the 2020-10-29 partition to the 2020-10-30 partition.
```sql
select * from t2 order by toDate(event_time), product_id;
┌──────event_time─┬product_id─┬─city──┬category─┬amount─┬revenue─┐
│ 2020-10-29 23:50:00 │      10003 │ Beijing │ men wear │      2 │     200 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10001 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-30 00:00:05 │      10002 │ Beijing │ men wear │      2 │     200 │
└─────────────┴───────┴─────┴──────┴─────┴─────┘
```

<span id="例2：版本字段使用"></span>
## Example 3: Using a Custom Version Field
By default, data written later with the same unique key will overwrite existing data. This may lead to the following problems

* When tracing upstream data, old data may overwrite new data, resulting in a regression in the data results obtained.
* In a Lambda architecture, if offline and real-time tasks write to the same partition simultaneously, which data is retained depends on the order of task execution.

To solve the above problems, HaUniqueMergeTree allows specifying a field in the table as the version field. The engine ensures that when writing data with the same key, it only overwrites if the data version is >= the existing version. The version field supports all UInt types and Data/DateTime, and cannot be Nullable.
:::tip
Limits when using the version field:

* If an integer is needed as a version field, it is recommended to use a UInt64 compatible unsigned integer.
* Date and Datetime types are supported as version fields.
* Float, Decimal, DateTime64, and other floating-point types are not supported as version fields.
:::
Assume the schema is as follows:
```sql
CREATE TABLE t3
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = HaUniqueMergeTree('/clickhouse/default/t3/{shard}', '{replica}', event_time) --event_time为版本字段
PARTITION BY toDate(event_time) --Partition field
ORDER BY (city, category) --Order field
UNIQUE KEY product_id; --Unique key
```

Insert the following data in sequence:
```sql
INSERT INTO t3 (event_time, product_id, city, category, amount, revenue) VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:50:00', 10001, 'Beijing', 'men wear', 8, 800),
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 5, 500);
```

The result keeps the last two records.
```sql
select * from t3 order by toDate(event_time), product_id;
┌──────event_time─┬product_id─┬─city──┬category─┬amount─┬revenue─┐
│ 2020-10-29 23:50:00 │      10001 │ Beijing │ men wear │      8 │     800 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men wear │      5 │     500 │
└─────────────┴───────┴─────┴──────┴─────┴─────┘
```

If the first two records are re-imported at this time.
```sql
INSERT INTO t3 (event_time, product_id, city, category, amount, revenue) VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200);
```

Since the version < the existing version, the write operation automatically skips. The versions of 10001 and 10002 have not been rolled back.
```sql
select * from t3 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 23:50:00 │      10001 │ Beijing │ men wear │      8 │     800 │
│ 2020-10-29 23:50:00 │      10002 │ Beijing │ men wear │      5 │     500 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```

<span id="ccef3f4e"></span>
## Example 4: Using partition values as versions
Consider the following requirement scenario in a Lambda architecture:

* Tables are partitioned by day, requiring deduplication at the table granularity based on a specific field.
* Real-time tasks write to the T+0 partition, which may update some data from the T+N partition to the T+0 partition.
* Offline tasks rewrite the T+1 partition daily.
* The latest data for each key must be read from its latest partition.

We can use the partition field (date) as a version field to implement this scenario; however, this requires storing an additional date field. Since all data under a partition share the same date, this approach obviously results in a waste of resources.
To optimize this scenario, HaUniqueMergeTree supports using the partition expression directly as a version. When the engine detects the version field is a partition field, it automatically reads the version from metadata, avoiding extra data read and write.
```SQL
-- Create a unique table partitioned by day with uniqueness at the table level, using the partitioning field as the version.
CREATE TABLE t4  
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = HaUniqueMergeTree('/clickhouse/default/t4/{shard}', '{replica}', toDate(event_time))
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id
SETTINGS partition_level_unique_keys = 0;

-- Write real-time task data on October 29th.
INSERT INTO t4 VALUES
('2020-10-29 10:00:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 10:00:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 10:10:00', 10001, 'Beijing', 'men wear', 8, 800),
('2020-10-29 10:10:00', 10002, 'Beijing', 'men wear', 5, 500);
-- Write real-time task data on October 30th, updating 10002 to the October 30th partition.
INSERT INTO t4 VALUES
('2020-10-30 08:00:00', 10002, 'Beijing', 'men wear', 10, 1000),
('2020-10-30 08:00:00', 10003, 'Beijing', 'men wear', 3, 300);
-- An offline task on October 30th overwrites the data on October 29th.
INSERT INTO t4 VALUES
('2020-10-29 10:10:00', 10001, 'Beijing', 'men wear', 7, 700),
('2020-10-29 10:10:00', 10002, 'Beijing', 'men wear', 5, 500);
-- 离The offline task will only overwrite the data of 10001. The latest data of 10002 in the October 30th partition will be retained.
select * from t4 order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category─┬─amount─┬─revenue─┐
│ 2020-10-29 10:10:00 │      10001 │ Beijing │ men wear │      7 │     700 │
│ 2020-10-30 08:00:00 │      10002 │ Beijing │ men wear │     10 │    1000 │
│ 2020-10-30 08:00:00 │      10003 │ Beijing │ men wear │      3 │     300 │
└─────────────────────┴────────────┴─────────┴──────────┴────────┴─────────┘
```

<span id="6848d178"></span>
## Example 5: Use of the Delete Field.
In some application scenarios, users wish to add a field during INSERT to indicate deletion, thus extending the INSERT semantics.
In the HaUniqueMergeTree engine, each table is equipped with a reserved field `_delete_flag_`, which can be specified during INSERT / INSERT SELECT operations. Its type is `UInt8`, where 0 indicates data writing, and non-zero indicates data deletion.
It is important to note that the `_delete_flag_` field can only be specified during INSERT / INSERT SELECT or when creating a materialized view. It cannot be specified during CREATE TABLE, nor can the field be queried.
:::warning
The delete row function can be applied to distributed tables whose underlying table is HaUniqueMergeTree, provided the distributed table is configured with the parameter **remote_table_is_ha_unique = 1.**
:::
Usage examples are as follows:
Assuming the schema is as follows:
```sql
CREATE TABLE t1
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64,
)
ENGINE = HaUniqueMergeTree(xxxx)
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id; --Unique key
```

Import the following data:
> Note: It is necessary to select a single node and insert into a local table to use the delete flag for data deletion.

```sql
INSERT INTO t1_local (event_time, product_id, city, category, amount, revenue, _delete_flag_) VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500, 0),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200, 0),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100, 0),
('2020-10-29 23:50:00', 10001, 'Beijing', 'men wear', 4, 400, 5),
('2020-10-29 23:50:00', 10002, 'Beijing', 'men wear', 2, 200, 1),
('2020-10-29 23:50:00', 10004, 'Beijing', 'men wear', 1, 100, 0);
```

The query result includes a newly added row and two deleted old rows:
```sql
select * from t1 order by toDate(event_time), product_id;
┌──────event_time─┬─product_id┬─city──┬─category┬amount─┬revenue─┐
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear │      1 │     100 │
│ 2020-10-29 23:50:00 │      10004 │ Beijing │ men wear │      1 │     100 │
└─────────────┴───────┴─────┴──────┴─────┴─────┘
```

The method for batch deletion of multiple rows based on a specific WHERE condition is as follows:
```sql
insert into `t1_local` (*, _delete_flag_) select *, 1 as _delete_flag_ from `t1_local` where product_id=10001;
```

<span id="例4：部分列更新（beta）"></span>
## Example 6: Partial column update
**Usage conditions:**

1. **Currently, only partial column update functionality is supported.**
2. **Table-level uniqueness** is not supported for partial column updates, only partition-level uniqueness is supported.
3. If importing data with Kafka, it is necessary to enable the switch **enable_unique_partial_update = 1.** for unique tables.
4. Operations can be performed on distributed tables backed by HaUniqueMergeTree, provided that the distributed tables are configured with the parameter **remote_table_is_ha_unique = 1.**

**Row update mode: Default values are used to fill in missing columns.**
**Partial column update mode: Existing values in default columns are retained if available; otherwise, default values are used.**

1. After specifying the variable **enable_unique_partial_update = 1** for unique tables, partial column update mode is allowed, which is otherwise disabled by default.
2. Partial column write mode is effective only when the unique table has the partial column update feature enabled; otherwise, it is equivalent to row update mode.
   1. For interactive writing, unique tables default to partial column update mode, switching to row update mode after setting the session variable **enable_unique_partial_update** = 0. The default value for the parameter **enable_unique_partial_update** is 1.
   2. For Kafka real-time writes, a new parameter **enable_unique_partial_update** is added to the Kafka table (default value is 1). '1' implies that Kafka consumption uses a partial column update mode, and '0' means using row update mode.
3. Default value of the type
   1. Numerical type: 0
   2. String type: ''
   3. Nullable type: null
   4. Map type (with special update rules, see below **5. Column Update Rules - Map Type**): {}
   5. Array type: []
4. During partial column update write mode, if the table contains a version field
   1. If the write version < current version, ignore the write row
   2. If the write version >= current version, apply column update rules
   3. When writing without a specified version, the version field defaults to a preset value.
5. Column Update Rules
   1. Method One: Differentiate update column rules based on function-column _update_columns_ (of type String).
      1. The contents in _update_columns_ are the columns to be updated, separated by commas. The engine does not process special characters like spaces, tabs, and newlines around the column names when parsing, and it does not support regular expressions.
      2. **When _update_columns_ is empty, it indicates an update of all columns.**
      3. For non-Map types: Writing a non-default value indicates an update, and updating to a default value is not allowed.
      4. For Map types: When **partial_update_enable_merge_map = true**, update existing keys and write new keys; if false, replace the value directly.

```Plain Text
  <div lmkr="1" list="indent2" text-indent="true">      <pre class="language-sql"><code><p><span class="hljs-keyword" from="code-block" >CREATE</span><span class="" from="code-block" > </span><span class="hljs-keyword" from="code-block" >TABLE</span><span class="" from="code-block" > t1 (</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  k Int32,</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  c1 Int32,</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  c2 Nullable(Float64),</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  c3 Nullable(String),</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  c4 Nullable(Int64),</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  m1 Map(String, Int32),</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >  a1 </span><span class="hljs-keyword" from="code-block" >Array</span><span class="" from="code-block" >(String))</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >ENGINE </span><span class="hljs-operator" from="code-block" >=</span><span class="" from="code-block" > HaUniqueMergeTree(</span><span class="hljs-string" from="code-block" >'/clickhouse/default/t1/{shard}'</span><span class="" from="code-block" >, </span><span class="hljs-string" from="code-block" >'{replica}'</span><span class="" from="code-block" >)</span><span class="" from="code-block" >
  </span></p><p><span class="hljs-keyword" from="code-block" >UNIQUE</span><span class="" from="code-block" > KEY k </span><span class="hljs-keyword" from="code-block" >ORDER</span><span class="" from="code-block" > </span><span class="hljs-keyword" from="code-block" >BY</span><span class="" from="code-block" > k SETTINGS enable_unique_partial_update </span><span class="hljs-operator" from="code-block" >=</span><span class="" from="code-block" > </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >, </span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >partial_update_enable_specify_update_columns </span><span class="hljs-operator" from="code-block" >=</span><span class="" from="code-block" > </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >,</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >partial_update_enable_merge_map </span><span class="hljs-operator" from="code-block" >=</span><span class="" from="code-block" > </span><span class="hljs-number" from="code-block" >0</span><span class="" from="code-block" >;</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >
  </span></p><p><span class="hljs-keyword" from="code-block" >SET</span><span class="" from="code-block" > enable_unique_partial_update </span><span class="hljs-operator" from="code-block" >=</span><span class="" from="code-block" > </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >;</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >
  </span></p><p><span class="hljs-keyword" from="code-block" >INSERT</span><span class="" from="code-block" > </span><span class="hljs-keyword" from="code-block" >INTO</span><span class="" from="code-block" > t1 (k, c1, c2, m1, a1) </span><span class="hljs-keyword" from="code-block" >VALUES</span><span class="" from="code-block" > (</span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >10</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >3.14</span><span class="" from="code-block" >, {</span><span class="hljs-string" from="code-block" >'k1'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >}, [</span><span class="hljs-string" from="code-block" >'hello'</span><span class="" from="code-block" >]);</span><span class="" from="code-block" >
  </span></p><p><span class="hljs-comment" from="code-block" >-- During the parsing process, _update_columns_ will be filled with 'k,c1,c2,m1,a1'</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >│ </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >10</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >3.14</span><span class="" from="code-block" > │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {</span><span class="hljs-string" from="code-block" >'k1'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >} │ [</span><span class="hljs-string" from="code-block" >'hello'</span><span class="" from="code-block" >] │</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >└───┴────┴──────┴──────┴──────┴──────────┴───────────┘</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >
  </span></p><p><span class="hljs-keyword" from="code-block" >INSERT</span><span class="" from="code-block" > </span><span class="hljs-keyword" from="code-block" >INTO</span><span class="" from="code-block" > t1 (k, c1, c2, m1, a1, _update_columns_) </span><span class="hljs-keyword" from="code-block" >VALUES</span><span class="" from="code-block" > (</span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >20</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >31.4</span><span class="" from="code-block" >, {</span><span class="hljs-string" from="code-block" >'k2'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >2</span><span class="" from="code-block" >}, [</span><span class="hljs-string" from="code-block" >'world'</span><span class="" from="code-block" >], </span><span class="hljs-string" from="code-block" >'k,c1,m1,a1'</span><span class="" from="code-block" >);</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >│ </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >20</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >3.14</span><span class="" from="code-block" > │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {</span><span class="hljs-string" from="code-block" >'k2'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >2</span><span class="" from="code-block" >} │ [</span><span class="hljs-string" from="code-block" >'world'</span><span class="" from="code-block" >] │</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >└───┴────┴──────┴──────┴──────┴──────────┴───────────┘</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >
  </span></p><p><span class="hljs-keyword" from="code-block" >INSERT</span><span class="" from="code-block" > </span><span class="hljs-keyword" from="code-block" >INTO</span><span class="" from="code-block" > t1 (k, c1, c3, m1) </span><span class="hljs-keyword" from="code-block" >VALUES</span><span class="" from="code-block" > (</span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >0</span><span class="" from="code-block" >, </span><span class="hljs-string" from="code-block" >'foo'</span><span class="" from="code-block" >, {</span><span class="hljs-string" from="code-block" >'k3'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >3</span><span class="" from="code-block" >});</span><span class="" from="code-block" >
  </span></p><p><span class="hljs-comment" from="code-block" >-- During the parsing process, _update_columns_ will be filled with 'k,c1,c3,m1'</span><span class="" from="code-block" >
  </span></p><p><span class="hljs-comment" from="code-block" >-- This equals with INSERT INTO t1 (k, c1, c3, m1, _update_columns_) VALUES (1, 0, 'foo', {'k2':2}, 'k, c1, c3, m1');</span><span class="" from="code-block" >
  </span></p><p><span class="hljs-comment" from="code-block" >-- c1 will be forcefully updated to 0, c3 will be forcefully updated to 'foo', and m1 will be forcefully updated to 'k3':3</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >┌─k─┬─c1─┬───c2─┬─c3──┬───c4─┬─m1───────┬─a1────────┐</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >│ </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" > │  </span><span class="hljs-number" from="code-block" >0</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >3.14</span><span class="" from="code-block" > │ foo │ ᴺᵁᴸᴸ │ {</span><span class="hljs-string" from="code-block" >'k3'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >3</span><span class="" from="code-block" >} │ [</span><span class="hljs-string" from="code-block" >'world'</span><span class="" from="code-block" >] │</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >└───┴────┴──────┴─────┴──────┴──────────┴───────────┘</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >
  </span></p><p><span class="hljs-keyword" from="code-block" >INSERT</span><span class="" from="code-block" > </span><span class="hljs-keyword" from="code-block" >INTO</span><span class="" from="code-block" > t1 (k, c1, c2, c3, c4, m1, a1, _update_columns_) </span><span class="hljs-keyword" from="code-block" >VALUES</span><span class="" from="code-block" > (</span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >10</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >31.4</span><span class="" from="code-block" >, </span><span class="hljs-string" from="code-block" >'goo'</span><span class="" from="code-block" >, </span><span class="hljs-number" from="code-block" >15</span><span class="" from="code-block" >, {</span><span class="hljs-string" from="code-block" >'k4'</span><span class="" from="code-block" >: </span><span class="hljs-number" from="code-block" >4</span><span class="" from="code-block" >}, [</span><span class="hljs-string" from="code-block" >'hello'</span><span class="" from="code-block" >, </span><span class="hljs-string" from="code-block" >'world'</span><span class="" from="code-block" >], </span><span class="hljs-string" from="code-block" >''</span><span class="" from="code-block" >);</span><span class="" from="code-block" >
  </span></p><p><span class="hljs-comment" from="code-block" >-- When _update_columns_ is empty, it meand updating all column</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >┌─k─┬─c1─┬───c2─┬─c3──┬─c4─┬─m1───────┬─a1────────────────┐</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >│ </span><span class="hljs-number" from="code-block" >1</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >10</span><span class="" from="code-block" > │ </span><span class="hljs-number" from="code-block" >31.4</span><span class="" from="code-block" > │ goo │ </span><span class="hljs-number" from="code-block" >15</span><span class="" from="code-block" > │ {</span><span class="hljs-string" from="code-block" >'k4'</span><span class="" from="code-block" >:</span><span class="hljs-number" from="code-block" >4</span><span class="" from="code-block" >} │ [</span><span class="hljs-string" from="code-block" >'hello'</span><span class="" from="code-block" >,</span><span class="hljs-string" from="code-block" >'world'</span><span class="" from="code-block" >] │</span><span class="" from="code-block" >
  </span></p><p><span class="" from="code-block" >└───┴────┴──────┴─────┴────┴──────────┴───────────────────┘</span><span class="" from="code-block" >
  </span></p></code></pre>      </div>
```


   2. Method Two: Differentiate update column rules based on default values by type.
      1. For non-Map types: Writing a non-default value indicates an update, and updating to a default value is not allowed.
      2. For Map types: When **partial_update_enable_merge_map = true**, update existing keys and write new keys; if false, replace the value directly.

```sql
CREATE TABLE t1 (
   
  k Int32,
   
  c1 Int32,
   
  c2 Nullable(Float64),
   
  c3 Nullable(String),
   
  c4 Nullable(Int64),
   
  m1 Map(String, Int32),
   
  a1 Array(String)) 
   
ENGINE = HaUniqueMergeTree('/clickhouse/default/t1/{shard}', '{replica}')
   
UNIQUE KEY k ORDER BY k SETTINGS enable_unique_partial_update = 1, 
   
partial_update_enable_specify_update_columns = 0,
   
partial_update_enable_merge_map = 1;
   

   
SET enable_unique_partial_update = 1;
   

   
INSERT INTO t1 (k, c1, c2, m1, a1) VALUES (1, 10, 3.14, {'k1':1}, ['hello']);
   
┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐
   
│ 1 │ 10 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k1':1} │ ['hello'] │
   
└───┴────┴──────┴──────┴──────┴──────────┴───────────┘
   

   
INSERT INTO t1 (k, c1, c3, m1) VALUES (1, 0, 'foo', {'k2':2});
   
-- For the unspecified fields
   
-- - c1 is of a non-composite type, but the written value is the default value, so the old value is retained.
   
-- - c2/c4 are of the Nullable type, and the old values are retained.
   
-- - a1 is an empty Array value, and the old value is retained.
   
-- For m1, update m1{'k2'}, and retain m1{'k1'}.
   
┌─k─┬─c1─┬───c2─┬─c3──┬───c4─┬─m1──────────────┬─a1────────┐
   
│ 1 │ 10 │ 3.14 │ foo │ ᴺᵁᴸᴸ │ {'k1':1,'k2':2} │ ['hello'] │
   
└───┴────┴──────┴─────┴──────┴─────────────────┴───────────┘
   

   
INSERT INTO t1 (k, c1, c2, c3, c4, m1, a1) VALUES (1, 20, null, 'bar', 30, {'k2':0, 'k3':3}, ['world']);
   
-- c1 is not the default value, so update it.
   
-- c2 is null, retain the old value; c3/c4 are not null, update them.
   
-- Update m1{'k2'} and m1{'k3'}, and retain m1{'k1'}.
   
-- a1 is not a null value, so update it.
   
┌─k─┬─c1─┬───c2─┬─c3──┬─c4─┬─m1─────────────────────┬─a1────────┐
   
│ 1 │ 20 │ 3.14 │ bar │ 30 │ {'k1':1,'k2':0,'k3':3} │ ['world'] │
   
└───┴────┴──────┴─────┴────┴────────────────────────┴───────────┘
   
```

[Caution] When creating tables using this method, **use default values sparingly!**
When creating tables, you can specify default values after fields, which can be expressions. If users specify default values, columns that are missing during writing will be filled according to the method specified at table creation. However, when updating some columns to determine if they are default values, it's judged based on the engine's internal data type default values, which may lead to behaviors not as expected. The following will provide an example for illustration.
```sql
CREATE TABLE t1 (
   
  k Int32,
   
  c1 Int32 DEFAULT k + 1,
   
  c2 Nullable(Float64))
   
ENGINE = HaUniqueMergeTree('/clickhouse/default/t1/{shard}', '{replica}')
   
UNIQUE KEY k ORDER BY k SETTINGS enable_unique_partial_update = 1, 
   
partial_update_enable_specify_update_columns = 0;
   

   
insert into t1 values (1, 10, 3.14);
   
┌─k─┬─c1─┬───c2─┐
   
│ 1 │ 10 │ 3.14 │
   
└───┴────┴──────┘
   

   
insert into t1 (k, c2) values (1, 31.4);
   
┌─k─┬─c1─┬───c2─┐
   
│ 1 │  2 │ 31.4 │
   
└───┴────┴──────┘
   
-- -- If the default value of c1 is not specified when creating the table, then the semantics of this write operation is that the value of c2 for the row with k = 1 will be updated to 31.4. However, since the default value was specified when creating the table, it is equivalent to "insert into t1 values (1, 2, 31.4)", so c1 is also updated to 2. In this case, in order to achieve the goal of only updating c2, there are the following two methods: 1. Do not use the default value when creating the table; 2. Specify the default value explicitly, that is, "insert into t1 values (1, 0, 31.4)".  
   
-- ┌─k─┬─c1─┬───c2─┐
   
-- │ 1 │ 10 │ 31.4 │
   
-- └───┴────┴──────┘
   
```

<span id="性能"></span>
# Performance
In in-memory mode, the import performance of HaUniqueMergeTree is about half that of HaMergeTree or the MergeTree engine from the community, at 10k rows/s/shard, or 20 MB/s. The performance is nearly consistent with the community's ReplacingMergeTree.
However, the query performance of HaUniqueMergeTree is consistent with that of HaMergeTree or the MergeTree engine.
In disk-based mode, the import performance of HaUniqueMergeTree is about 30-40% of HaMergeTree or the community's MergeTree engine, at 6-8k rows/s/shard, or 12-16 MB/s. The query performance remains unchanged.
<span id="引擎限制"></span>
# Engine Restrictions

* When importing into Kafka, users must ensure that data with the same unique key is written to the same Topic Partition and disable Topic expansion.
* The cluster with the unique key currently does not support expansion.
* In in-memory index mode, memory usage is directly proportional to the size and cardinality of the unique key, and is not suitable for tables with more than 100 million records on a single node, as improper use can cause node OOM; disk index mode must be enabled.

<span id="最佳使用实践"></span>
# Best Practices
<span id="建表参数推荐"></span>
## Recommended Table Creation Parameters
<span id="in-memory-与-disk-based-选择"></span>
### In-memory and Disk-based Options
Currently, there are two key index usages for unique tables: in-memory and disk-based. Controlled by the table-level parameter `enable_disk_based_unique_key_index`.

* The use of disk-based does not limit the total volume of data in the table, but its performance is 40% lower than that of the in-memory mode. Approximately 6 MB/s per Shard.
* In-memory performance is better, reaching up to 10MB/s, but it limits data volume. The recommendation is as follows:
   * When "table-level uniqueness" is enabled, in-memory indexes for all partitions must be resident in memory; thus, it is not advisable to enable unique keys on tables with more than 100 million records per single node. If the cluster has 20 shards, then it can support up to 20 billion records.
   * With "partition-level uniqueness," only the partitions that have had recent data writes need to load in-memory indexes. Therefore, if the business only updates data from the last N days, as long as the number of records from N days does not exceed 100 million on a single node, in-memory mode can be utilized.

<span id="唯一键选择"></span>
### Choice of unique keys
If it includes many fields, consider using hash values. Example: `UNIQUE KEY sipHash64(val1, val2, val3...)`
<span id="唯一键级别"></span>
### Unique key level
Always use the default partition level unique.
If business scenarios necessitate using table level unique, consider setting TTL, adopting coarser partition granularity (e.g., monthly partitioning), etc., to reduce the number of partitions.
<span id="版本字段选择"></span>
### Version field selection
If specifying a version field is necessary, prioritize using partition values as the version to reduce memory usage.
<span id="表修改"></span>
## Table modifications

1. The operations Detach partition and Attach partition can only be executed on the leader node.
2. Real-time delete features and their relationship with unique key levels and versions:
   * The real-time delete level and unique key level match; that is, if the unique key level is partition, deletion will only remove data from the corresponding partition.
   * When a specific version (non-zero) is designated, real-time deletion will follow the version rules; when no version is specified or specified as zero, real-time. Deletion will not follow version rules.
3. After a ByteHouse unique table is created, the types of the unique key and unique key columns cannot be modified.

<span id="kafka-导入"></span>
## Importing to Kafka
The consumer writes directly to the local shard. Therefore

* Businesses need to ensure that **data with the same unique key is written to the same topic partition**
* To ensure that the mapping from key to shard remains unchanged, **the topic needs to be set with a fixed number of partitions and disable automatic partition changes**
* If you want to import data to the same table through both batch and streaming modes, you can use the batch data source -> Kafka -> CH method to ensure that the sharding approaches for offline data match those of real-time.
