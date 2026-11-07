---
title: "CnchMergeTree"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cnchmergetree"
---

<span id="表引擎介绍"></span>
## Introduction to Table Engines

The table engine, which is the type of the table, determines:


* The organization and storage method of data

* The method and type of indexing

* The types of queries supported and how they are supported

* Some other specific features and configurations


The most commonly used table engine in ByteHouse Cloud Data Warehouse Edition is CnchMergeTree, along with other special types of table engines including Hive external tables, Kafka tables, etc. This article primarily shares the principles of the CnchMergeTree table engine.

<span id="cnchmergetree-表引擎"></span>
## CnchMergeTree table engine

CNCHMergeTree is the most commonly used table engine. Its core concept is similar to LSM\-Tree, where data is partitioned by the partition key and then stored in order by the sorting key. Main features include:

**1. Logical Partitioning**

If a partition key is specified, data is divided into different logical data sets (logical partitions, Partition).

Each logical partition can have zero or more data fragments (DataPart). If the query conditions can prune partitions, this can often speed up queries. If no partition key is specified, all data resides in a single logical partition.

**2. Data Fragments**

Data segments are sorted by the sorting key. Each data segment also has a min/max index to accelerate partition selection.

**3. Data Granule**

Each data segment is logically divided into granules, with the default granule size being 8192 rows (determined by the table's index_granularity setting). Granules are the smallest indivisible data sets used in ByteHouse for data querying. The first row of each granule is marked by the primary key value of that row, and ByteHouse creates an index file for each data segment to store these markers. For each column, whether or not it is part of the primary key, ByteHouse stores similar markers. These markers allow you to directly locate data in the column files. Granules serve as the indexing target for ByteHouse's sparse index and are also the unit for data scanning in memory.

**4. Background Merge**

Background tasks periodically merge DataParts in the same partition and maintain order by sorting key. Background merges reduce the number of parts to allow for more efficient storage and improved query performance.

<span id="cnchmergetree-建表语句和相关配置"></span>
## Table creation statements and related configurations for CnchMergeTree

The table engine of CnchMergeTree supports the following syntax for table creation:

```SQL
CREATE TABLE [IF NOT EXISTS] [db.]table_name
(
    name1 [type1] [DEFAULT|ALIAS expr1] [compression_codec] [TTL expr1],
    name2 [type2] [DEFAULT|ALIAS expr2] [compression_codec] [TTL expr2],
    ...
    INDEX index_name1 expr1 TYPE type1(...) GRANULARITY value1,
    INDEX index_name2 expr2 TYPE type2(...) GRANULARITY value2，
) ENGINE = CnchMergeTree()
ORDER BY expr
[PARTITION BY expr]
[CLUSTER BY (column, expression, ...) INTO value1 BUCKETS SPLIT_NUMBER value2 WITH_RANGE]
[PRIMARY KEY expr]
[UNIQUE KEY expr]
[SAMPLE BY expr]
[TTL expr]
[SETTINGS name=value, ...]
```


<span id="配置参数说明"></span>
## Configuration parameter description

<span id="设计分区键（partition-by"></span>
### Designing a partition key (PARTITION BY)

The partition key defines partitions, which are logical data sets divided in a table according to specified rules. Partitions can be created based on any criterion, such as by date. To reduce the data needing handling, each partition is stored separately. When querying, ByteHouse strives to use the smallest subset of these partitions. Partitioning is specified at the time of table creation via the clause `PARTITION BY expr`. The partition key can be any expression of a column in the table. For example, specify partitioning by month with the expression `toYYYYMM(date)`; or by expression tuples, such as `(toMonday(date), EventType)`, etc.

Note that the range of values derived from the partition expression in the table should not be too large (recommended not to exceed ten thousand), as having too many partitions can occupy significant memory and cause considerable IO and computational overhead.

Properly designing partition keys can greatly reduce the amount of data needed to be scanned during queries, generally considering the most commonly used conditions in the query with a value range not exceeding ten thousand as partition keys (such as dates, etc.).

<span id="设计排序键（order-by）"></span>
### Design sorting keys (ORDER BY)

The sorting key can be a tuple of columns or any expression. For example: `ORDER BY (OrderID, Date)`.

If no sorting is needed, you can use `ORDER BY tuple()`, and DataPart will store the data in the order it was inserted.

<span id="设计主键-primary-key"></span>
### Primary key (PRIMARY KEY)

By default, no explicit specification is needed, and ByteHouse will use the sort key as the primary key. When the primary key and sort key are inconsistent in specific scenarios, the primary key must be the leftmost prefix of the sort key. If the sort key is (OrderID, Date), the primary key must be OrderID, not Date.

ByteHouse builds sparse indexes on the primary key at the Granule level, (in contrast, what are called dense indexes are those where an index entry is created for every row).

If the search criteria match the leftmost prefix of the primary key index, the primary key index can quickly filter out the data granules that may need to be read, which is usually much more efficient than scanning the entire DataPart.

**Additionally, it is important to note that the PRIMARY KEY cannot guarantee uniqueness, so data rows with duplicate primary keys can be inserted.** 

Partitioning (PARTITION BY) and primary key (PRIMARY KEY) are two different ways to accelerate data querying, and when defining them, it is best to stagger the use of different columns to cover more query scenarios. For instance, never repeat the first column of an order by in partition by. Below are some considerations for choosing a primary key:


* Whether it is a commonly used column in the search criteria.

* The first column is not a non\-partitioning key

* Columns like gender and yes/no with limited selectable values are not recommended for the primary key

* If the current primary key is (a, b), and in most cases, the data scope for given (a, b) is large (covering multiple granules), consider adding a commonly queried column to the primary key for filtering more data

* Overly long primary keys negatively affect insertion performance and memory consumption, but have no impact on query performance


<span id="唯一键索引-unique-key"></span>
### Unique key (UNIQUE KEY)

ByteHouse's primary key (PRIMARY KEY) does not ensure uniqueness. If unique de\-duplication is needed, set a unique key index when creating the table After setting a unique key, ByteHouse supports upsert update semantics, which allow for efficient data row updates based on unique keys, or virtual columns can be used to delete specified keys during an upsert by setting `_delete_flag_=1` Queries automatically return the latest value of each unique key

Unique keys can be a tuple of columns or any expression, such as `UNIQUE KEY (product_id, sipHash64(city))`

Querying with unique keys uses the unique key index to filter data and speed up queries, hence, primary keys used for sorting can be set with different columns than unique keys to cover more query conditions

For more details on unique key indexes and unique key tables, refer to [Unique Key table](https://docs.byteplus.com/docs/bytehouse/unique-key-table) and [Best practice for ByteHouse Unique Key tables](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>What are the differences between Primary key and Unique key?</strong></div>


<div data-tips="true" data-tips-type="warning">Primary Key accelerates queries due to its sparse indexing, while Unique Key ensures data uniqueness within the same partition (if the Unique Keys are identical, the more recently written data will overwrite the previous one). Consider your requirements when choosing between these two keys, and consider setting fields that act as filters as the Primary Key.</div>


<span id="4f8ebb25"></span>
### Bucketing (Cluster By)

Bucketing is commonly used in the following scenarios:


1. **Common scenario:**  Data distribution is uneven

   * **Definition and principle**: When partitioning does not achieve an even distribution of data, bucketing fields can be utilized. Bucketing fields ensure an even distribution of a column of data across each node in the cluster. This maximizes the performance of queries across the cluster. Proper configuration of partitioning fields also helps to address data skew problems, ensuring a more even data distribution.

   * **Field limitations**: Does not support Nullable.

   * **Configuration suggestion**: Choose fields that frequently appear in grouping criteria.

   * Once the table is created, this field cannot be modified in terms of column type.

2. **Specific scenes**: Slow duplicate data deletion speed.

   * **Definition and principles**: When a Unique Key is set and there is excessive data in a single partition (e.g., exceeding 100 million rows), data ingestion speed will be affected. This is because acquiring a lock is necessary to delete duplicate data. In such cases, you can partition the data into buckets to improve data ingestion speed.

   * **Field restrictions**: Nullable is not supported.

   * **Configuration recommendations**: The Bucket Key should be the same as the Unique Key. (Each bucket should contain fewer than 10 million rows)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying an existing table to add buckets will impact only new partitions and not affect existing ones.</div>


For operation details about bucket table, please refer to:


* [Create dynamic partitioned tables](https://docs.byteplus.com/docs/bytehouse/create-statement#b9a1a39f)

* [Bucket deduplication optimizations](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables#a8c5dffd)

* [Bucket table dynamic expansion](https://docs.byteplus.com/docs/bytehouse/bucket-table-dynamic-expansion)


<span id="采样"></span>
### Sampling

An expression used for sampling, which is an optional configuration.

If a sampling expression is used, the primary key must contain this expression. For example: `SAMPLE BY intHash32(UserID) ORDER BY (CounterID, EventDate, intHash32(UserID))`.

<span id="列和表的-ttl"></span>
### TTL of columns and tables

Optional rules list specifying the duration data is stored per row and defining the logic for moving data segments across disks and volumes.

At least one column of type `Date` or `DateTime` must exist in the expression, such as:

`TTL date + INTERVAl 1 DAY`。

<span id="9b5b59eb"></span>
### Compression

The compression_codec field can be used to configure the codec, which is optional, with LZ4 as the default value.

ByteHouse supports general\-purpose encodings and specific encodings, with general\-purpose codecs resembling the default ones (LZ4, ZTSD) and their modified versions. Specific codecs are designed to take advantage of the particular characteristics of the data to make compression more effective.


1. **General Encoding**

* NONE: No compression.

* LZ4: Default, lossless [high-speed compression algorithm](https://github.com/lz4/lz4).

* LZ4HC[(level)]: LZ4HC compression algorithm with configurable levels with higher compression rates. The default level is 9, supporting values from 1 to 12, with 4 to 9 recommended.

* ZSTD[(level)]: ZSTD compression algorithm with configurable levels. The default level is 1, supporting 1 to 22.

2. **Specific Encoding Algorithms**

* Delta(delta_bytes): Incremental encoding, maintaining the first position and storing the differences between every two subsequent values. The default value is the size of(type), optional values are 1, 2, 4, or 8, other values are considered as 1.

3. **Multicodec**


Use the aforementioned multiple codecs. Compression will be carried out in the order declared by the codecs, and decompression will follow the reverse order.

For example, refer to:

```SQL
CREATE TABLE codec_example
(
    date Date CODEC(Delta, ZSTD), 
    ts DateTime CODEC(LZ4HC),
    float_value Float32 CODEC(NONE),
    double_value Float64 CODEC(LZ4HC(9))
)
ENGINE = CnchMergeTree
PARTITION BY tuple()
ORDER BY date
```


<span id="更多配置"></span>
### More configurations

For more configuration related to table creation, such as Unique tables, bucketing tables, and others, refer to [Best practice for creating tables in ByteHouse](https://docs.byteplus.com/docs/bytehouse/bytehouse-table-creation-best-practice).

<span id="架构优劣势说明"></span>
## Description of architectural advantages and disadvantages

The core value of CnchMergeTree merging lies in zero\-storage linear retrieval: data is imported into the table in separate batches but can be reduced in file number through merging, allowing linear storage of data. Allowing ByteHouse to maximally utilize the disk's strong sequential reading capability, bringing exceptional query performance.

However, the problem with merging is clear: if the background writing is too fragmented (e.g., only inserting a few hundred or dozen rows at a time), it leads to numerous partitions, and the merge tasks will increase CPU costs, and memory consumption, resulting in diminished performance of query tasks. In addition, if too many small files slow down the merge, it will also reduce the query performance when querying the latest data, as Part has not had enough time to merge.

<span id="常见问题"></span>
## FAQ

<span id="为什么不建议使用-select"></span>
### Why is using `Select *` not recommended?

Since ByteHouse is a columnar storage database, data is stored in different columnar storage files (.bin), a design meant to speed up queries by only needing to read a limited number of files when querying specific columns.

If you use `select *`, the backend needs to read all the `.bin` columnar storage files, effectively losing the advantages of columnar storage.

<span id="为什么不建议-insert-into插入数据？"></span>
### Why is using `Insert Into` to insert data not recommended?

Every `Insert Into` creates a new part folder, and constantly calling `Insert Into` results in many parts, each with a small amount of data, requiring the backend to merge for a long time to reduce the number of parts. Problems it causes:


* During this period, queries are extremely slow because a range query might cross several parts' columnar storage files.

* Long\-term merges are incomplete, consuming system resources.


<span id="为什么建议查询时加限制分区字段的条件？"></span>
### Why is it recommended to add partition field conditions when querying?

After limiting partitions, querying will only scan a limited number of part directories, reducing the amount of data scanned and significantly speeding up the query.

<span id="为什么分区字段建议设置为日期字段？"></span>
### Why is it suggested to set the partition field as a date field?

Currently, ByteHouse only supports fields that can be converted to dates (int, string, data, datetime) to configure partition keys. From a business perspective, as the data volume per day/hour is close, partitioning by date field can make each partition size more balanced and prevent drastic fluctuations in latency for individual queries.

<span id="为什么排序索引建议设置为查询中最常用的字段？"></span>
### Why is it suggested to set the sorting index to the most commonly used field in the query?

As you can see from the previous text, each block is sorted according to the sorting index, and a sparse index is built on that field. If the query contains the sorting index, the MergeTree engine will use the relationship between the marks in the index and the corresponding data to prune unnecessary granules, reducing the number of rows scanned and enhancing query performance.

If the query does not include the sorting index, then a full file scan must be conducted, which is very inefficient.
