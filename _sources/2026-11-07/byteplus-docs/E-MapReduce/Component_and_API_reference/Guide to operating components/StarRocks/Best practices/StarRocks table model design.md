---
title: "StarRocks table model design"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_table_model_design"
---

<span id="_1-starrocks-表设计"></span>
## 1 StarRocks table design

<span id="_1-1-列式存储"></span>
### 1.1 Columnar storage

Tables in StarRocks consist of rows and columns. Each row of data corresponds to a user record, and each column contains data of the same type. All data rows have the same number of columns, and columns can be dynamically added or removed. In StarRocks, the columns of a table can be divided into dimension columns (also called Key columns) and metric columns (also called Value columns). Dimension columns are used for grouping and sorting.

In StarRocks, table data is stored by column. Physically, each column of data undergoes block encoding, compression, and other operations, and is then persistently stored on non\-volatile devices. Logically, each column of data can be regarded as an array composed of elements of the same type. All column values of a row are arranged in their respective arras in column order, that is, they share the same array index. The array index is implicit and does not need to be stored. All rows in the table are sorted multiple times according to the dimension columns, and the position after sorting is the row number of that row.

<span id="_1-2-索引"></span>
### 1.2 Indexes

StarRocks uses prefix indexes (Prefix Index) and column\-level indexes to quickly locate the starting row number of the data block containing the target row.

The principles of StarRocks table design are illustrated in the following diagram.

The data organization in a table mainly consists of three parts:


* Prefix index

* Every 1,024 rows of data in the table form a logical data block (Data Block). Each logical data block stores an index entry in the prefix index table. The index entry contains the prefix formed by the dimension columns of the first row in the data block, with a length not exceeding 36 bytes. The prefix index is a sparse index. By searching the prefix index table with the prefix formed by the dimension columns of a row in the table, the starting row number of the logical data block containing that row can be determined.

* Column\-level data block

* Each column of data in the table is stored in blocks of 64 KB. Each data block is encoded and compressed as a Unit, and also serves as an I/O Unit, being written back to or read from the device as a whole.

* Column\-level index

* Each column in the table has an independent row number index. In the row number index table, the data blocks of this column correspond one\-to\-one with the row numbers. Each row number index entry consists of the starting row number, position, and length information of the corresponding data block. By using the row number of a row to look up the row number index table, you can obtain the location of the data block containing that row number. After reading the target data block, you can further search for the data.


Therefore, the process of searching for a row of data using the prefix formed by the dimension columns of that row includes the following five steps:


1. First, search the prefix index table to obtain the starting row number of the logical data block.

2. Search the row number index of the dimension column to locate the data block of the dimension column.

3. Read the data block.

4. Decompress and decode the data block.

5. Find the data item corresponding to the dimension column prefix in the data block.


<span id="_2-明细模型"></span>
## 2 Detail model

The detail model is the default table creation model. If no model is specified when creating a table, a detail\-type table is created by default.

You can define sort keys when creating a table. If the query filter conditions include sort keys, StarRocks can quickly filter data and improve query efficiency. The detail model is suitable for scenarios such as log data analysis, supports appending new data, and does not support modifying historical data.

<span id="_2-1-适用场景"></span>
### 2.1 Use cases


* Analyze raw data, such as raw logs and raw operation records.

* Query methods are flexible and are not limited to pre\-aggregated analysis.

* Import log data or time series data, with the main characteristic that old data is not updated and only new data is appended.


<span id="_2-2-创建表"></span>
### 2.2 Create table

For example, to analyze data for a certain type of event within a specific time range, you can use event time (`event_time`) and event type (`event_type`) as sort keys.

In this business scenario, the table creation statement is as follows:

```sql
CREATE TABLE IF NOT EXISTS detail (
    event_time DATETIME NOT NULL COMMENT "datetime of event",
    event_type INT NOT NULL COMMENT "type of event",
    user_id INT COMMENT "id of user",
    device_code INT COMMENT "device code",
    channel INT COMMENT ""
)
DUPLICATE KEY(event_time, event_type)
DISTRIBUTED BY HASH(user_id)
PROPERTIES (
"replication_num" = "3"
);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <code>DISTRIBUTED BY HASH</code> clause must be used to specify the bucket key when creating a table; otherwise, table creation fails.</div>


<span id="_2-3-使用说明"></span>
### 2.3 Note


* Note on sort keys:

   * In the table creation statement, sort keys must be defined before other columns.

   * The sort key can be explicitly defined through `DUPLICATE KEY`. In this example, the sort keys are `event_time` and `event_type`.

> * If not specified, the first three columns of the table are selected as the default sort keys.

* In the detail model, the sort key can consist of some or all of the dimension columns.

* When creating a table, you can create indexes such as BITMAP and Bloom Filter for metric columns.


<span id="_3-聚合模型"></span>
## 3. Aggregate model

When creating a table, you can define sort keys and metric columns, and specify aggregation functions for metric columns. When multiple records have the same sort key, the metric columns will be aggregated. When analyzing statistics and summary data, the aggregate model can reduce the amount of data processed during queries and improve query efficiency.

<span id="_3-1-适用场景"></span>
### 3.1 Use cases

Suitable for analyzing statistics and summary data. For example:


* By analyzing website or app traffic, calculate the total visit duration and total number of times for users.

* Advertising vendors provide advertisers with total ad clicks, total impressions, ad spend statistics, and more.

* By analyzing annual e\-commerce transaction data, obtain the best\-selling products among various consumer groups in a specified quarter or month.


In these scenarios, data querying and importing have the following characteristics:


* Most queries are summary\-type, such as SUM, MAX, MIN, and similar queries.

* There is no need to query the original detail data.

* Updates to old data are infrequent; only new data is appended.


<span id="_3-2-原理"></span>
### 3.2 Principles

From data import to data query, records with the same sort key in the aggregate model are aggregated multiple times. The specific timing and mechanism of aggregation are as follows:


1. Data import stage: When data is imported in batches into the aggregate model, each batch forms a version. Within a version, records with the same sort key are aggregated once.

2. Background file merge stage (Compaction): When data is imported in batches multiple times into the aggregate model, multiple versions of files are generated. When multiple versions are periodically merged into a larger version file, records with the same sort key are aggregated once.

3. Query phase: Data with the same sort key across all versions is aggregated, and then the query result is returned.


Therefore, multiple aggregations of data in the aggregation model can reduce the amount of data that needs to be processed during queries, thereby improving query efficiency.

For example, import the following data into the aggregation model, with Date and Country as the sort keys:


|Date |Country |PV |
|---|---|---|
|2020.05.01 |CHN |1 |
|2020.05.01 |CHN |2 |
|2020.05.01 |USA |3 |
|2020.05.01 |USA |4 |


In the aggregation model, the above four records will be aggregated into two records. This significantly reduces the amount of data processed in subsequent queries.


|Date |Country |PV |
|---|---|---|
|2020.05.01 |CHN |3 |
|2020.05.01 |USA |7 |


<span id="_3-3-创建表"></span>
### 3.3 Create table

For example, suppose you need to analyze the total number of times users from different cities visit different web pages within a certain period. You can use the web page address `site_id`, date `date`, and city code `city_code` as sort keys, use the visit count `pv` as a metric column, and specify the aggregation function for the metric column `pv` as SUM.

In this business scenario, the table creation statement is as follows:

```sql
CREATE TABLE IF NOT EXISTS example_db.aggregate_tbl (
    site_id LARGEINT NOT NULL COMMENT "id of site",
    date DATE NOT NULL COMMENT "time of event",
    city_code VARCHAR(20) COMMENT "city_code of user",
    pv BIGINT SUM DEFAULT "0" COMMENT "total page views"
)
AGGREGATE KEY(site_id, date, city_code)
DISTRIBUTED BY HASH(site_id)
PROPERTIES (
"replication_num" = "3"
);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The <code>DISTRIBUTED BY HASH</code> clause must be used to specify the bucket key when creating a table.</div>


* <div data-tips="true" data-tips-type="warning">Since version 2.5.7, StarRocks supports automatically setting the number of buckets (BUCKETS) when creating tables and adding partitions, so you do not need to set the number of buckets manually.</div>



<span id="_3-4-使用说明"></span>
### 3.4 Usage notes


* Notes on sort keys:

   * In the table creation statement, **sort keys must be defined before other columns**.

   * Sort keys can be explicitly defined using `AGGREGATE KEY`.

> ```Plain Text
  * If `AGGREGATE KEY` does not include all dimension columns (columns other than metric columns), table creation will fail.
  * If sort keys are not explicitly defined using `AGGREGATE KEY`, by default, all columns except metric columns are used as sort keys.
```



* Sort keys must satisfy the uniqueness constraint, must include all dimension columns, and the values of these columns will not be updated.

* Metric column: By specifying an aggregation function after the column name, the column is defined as a metric column. This generally refers to data that needs to be aggregated and counted.

* Aggregation function: The aggregation function used by the metric column. For aggregation functions supported by the aggregation model, see [StarRocks table model design](https://docs.byteplus.com/docs/E-MapReduce/109522).

* During queries, sort keys can be filtered before multi\-version aggregation, while metric columns are filtered after multi\-version aggregation. Therefore, it is recommended to use frequently used filter fields as sort keys, so that data can be filtered before aggregation, thereby improving query performance.

* When creating a table, it is not supported to create BITMAP, Bloom Filter, or other indexes on metric columns.


<span id="_4-更新模型"></span>
## 4 Update model

When creating a table, you can define primary keys and metric columns. When querying, the latest data from the group of records with the same primary key is returned. Compared to the detail model, the update model simplifies the data import process and better supports real\-time and frequent update scenarios.

<span id="_4-1-适用场景"></span>
### 4.1 use cases

Business scenarios with real\-time and frequent updates, such as analyzing e\-commerce orders. In e\-commerce scenarios, the status of orders frequently changes, and the daily volume of order updates can exceed hundreds of millions.

<span id="_4-2-原理"></span>
### 4.2 Principles

The update model can be regarded as a special case of the aggregate model, where the aggregation function specified for metric columns is REPLACE, returning the latest data from the group of records with the same primary key.

Data is imported into the update model in multiple batches, with each batch assigned a version number. Therefore, records with the same primary key may have multiple versions, and queries return the data with the latest version (that is, the largest version number). Compared to the detail model, the update model supports real\-time and frequent updates more effectively by simplifying the import process.

For example, in the table below, `ID` is the primary key, `value` is the metric column, and `_version` is the internal version number in StarRocks. Among them, the data with `ID` equal to 1 has two import batches, with version numbers `1` and `2` respectively; the data with `ID` equal to `2` has three import batches, with version numbers `3`, `4`, and `5` respectively.


|ID |value |_version |
|---|---|---|
|1 |100 |1 |
|1 |101 |2 |
|2 |100 |3 |
|2 |101 |4 |
|2 |102 |5 |


When querying data with `ID` equal to `1`, only the latest version `2` is returned. When querying data with `ID` equal to `2`, only the latest version `5` is returned. The final query result is as follows:


|ID |value |
|---|---|
|1 |101 |
|2 |102 |


<span id="_4-3-创建表"></span>
### 4.3 Create table

In e\-commerce order analysis scenarios, order status is often analyzed by date. Frequently used filter fields, such as order creation time `create_time` and order number `order_id`, can be used as primary keys, while other columns, such as order status `order_state` and total price `total_price`, can be used as metric columns. This approach meets the need for real\-time updates to order status and enables fast filtering during queries.

The table creation statement for this business scenario is as follows:

```sql
CREATE TABLE IF NOT EXISTS orders (
    create_time DATE NOT NULL COMMENT "create time of an order",
    order_id BIGINT NOT NULL COMMENT "id of an order",
    order_state INT COMMENT "state of an order",
    total_price BIGINT COMMENT "price of an order"
)
UNIQUE KEY(create_time, order_id)
DISTRIBUTED BY HASH(order_id)
PROPERTIES (
"replication_num" = "3"
);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The <code>DISTRIBUTED BY HASH</code> clause must be used to specify the bucket key when creating a table.</div>


* <div data-tips="true" data-tips-type="warning">Since version 2.5.7, StarRocks supports automatically setting the number of buckets (BUCKETS) when creating tables and adding partitions, so you do not need to set the number of buckets manually.</div>



<span id="_4-4-使用说明"></span>
### 4.4 Usage note


* Note on primary keys:

   * In table creation statements, the primary key must be defined before other columns.

   * The primary key is defined using `UNIQUE KEY`.

   * The primary key must satisfy the uniqueness constraint, and the values of its columns will not be modified.

   * Set an appropriate primary key.

      * During queries, the primary key can be filtered before aggregation, whereas filtering on metric columns typically occurs after multi\-version aggregation. Therefore, it is recommended to use frequently filtered fields as the primary key, so data can be filtered before aggregation, improving query performance.

      * All primary keys are compared during aggregation, so avoid including too many columns in the primary key to prevent decreased query performance. If a column is only occasionally used as a filter condition in queries, it is not recommended to include it in the primary key.

* When creating a table, it is not supported to create indexes such as BITMAP or Bloom Filter for metric columns.


<span id="_5-主键模型"></span>
## 5. Primary key model

The primary key model supports defining the primary key and sort key separately. When importing data into a table with the primary key model, the data is first sorted by the sort key before being stored. When querying, the latest data from the group of records with the same primary key is returned. Compared to the update model, the primary key model does not require aggregation operations during queries and supports predicate and index pushdown, enabling efficient queries while supporting **real\-time and frequent updates** scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before version 3.0, the primary key model did not support defining the primary key and sort key separately.</div>


* <div data-tips="true" data-tips-type="tip">Since version 3.1, the compute\-storage separation mode supports creating primary key model tables, and since version 3.1.4, supports persistent indexes on local disks.</div>



<span id="_5-1-适用场景"></span>
### 5.1 Use cases

The primary key model is suitable for real\-time and frequent updates, such as:


* **Real\-time integration of transactional data into StarRocks**. In transactional databases, besides inserting data, there are usually many update and delete operations. Therefore, when synchronizing transactional database data to StarRocks, it is recommended to use the primary key model.[StarRocks table model design](https://docs.byteplus.com/docs/E-MapReduce/109522) Real\-time synchronization of insert, update, and delete data to the primary key model can simplify the data synchronization process, and compared to the update model with the Merge\-On\-Read strategy, query performance can be improved by 3 to 10 times.

* **Easily implement multi\-stream JOIN using partial column updates**. In analysis scenarios such as user profiling, a wide table approach is generally adopted to improve the performance of multidimensional analysis and to simplify the usage model for data analysts. In these scenarios, upstream data often comes from multiple different businesses (such as shopping and consumption, express delivery, banking, and more) or systems (such as machine learning systems that calculate different user label attributes). The partial column update feature of the primary key model effectively meets this requirement, allowing each business to update only the columns relevant to its needs, while still benefiting from the primary key model's real\-time synchronization of data insertions, deletions, and updates, as well as efficient query performance.


<span id="_5-2-注意事项"></span>
### 5.2 Important notes


* If persistent indexing is enabled, the primary key model significantly reduces the memory usage of the primary key index. This is because, during import, only a small portion of the primary key index resides in memory, while most of the primary key index is stored on disk. **The maximum length of a single encoded primary key is 128 bytes**.

* If persistent indexing is not enabled, the primary key model is suitable for scenarios where the space occupied by the primary key is relatively controllable, because the primary key index is loaded into memory during import. **The maximum length and memory usage limit of a single encoded primary key is 128 bytes**. In the following two scenarios, the space occupied by the primary key is relatively controllable:

   * **The data has hot and cold characteristics**, meaning that only the hot data from the past few days is frequently modified, while older cold data is rarely modified. For example, a MySQL order table is synchronized in real time to StarRocks to provide analytical queries. In this case, the data is partitioned by day, and modifications to orders are concentrated on newly created orders from the past few days. Once older orders are completed, they are no longer updated. Therefore, the primary key index for these older orders is not loaded during import and does not occupy memory; only the indexes for the most recent days are loaded into memory.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53f45f2f4f9c972ce0822d5345f4d0d6.png) </span>

> * As shown in the figure, the data is partitioned by day, and the data in the latest two partitions is updated more frequently.

>    * **Wide tables** (hundreds to thousands of columns). The primary key occupies only a very small portion of the entire dataset, resulting in low memory overhead. For example, in user status and profile tables, although there are many columns, the total number of users is not large (tens of millions to hundreds of millions), so the memory usage of the primary key index is relatively manageable.

> * As shown in the figure, in wide tables, the primary key occupies only a small part, and the number of rows is limited.


<span id="_5-3-原理"></span>
### 5.3 Principle

The primary key model is supported by a newly designed and developed storage engine in StarRocks. Compared to the update model, the primary key model organizes metadata, reads, and writes in a completely different way. It does not require aggregation operations and supports predicate and index pushdown, which greatly improves query performance.

The update model generally adopts a Merge\-On\-Read strategy. Although processing during writes is simple and efficient, queries require online aggregation of multiple versions. Moreover, due to the presence of the Merge operator, predicates and indexes cannot be pushed down, which severely impacts query performance.

The primary key model, on the other hand, uses a Delete+Insert strategy to ensure that only one record exists for each primary key, thereby completely avoiding the Merge operation. The specific implementation is as follows:


* When StarRocks receives an update operation for a record, it locates the record through the primary key index, marks it as deleted, and then inserts a new record. This is equivalent to rewriting an Update as Delete+Insert.

* When StarRocks receives a delete operation for a record, it locates the record through the primary key index and marks it as deleted.


As a result, queries do not require aggregation operations, and predicate and index pushdown are not affected, ensuring efficient query execution.

<span id="_5-4-创建表"></span>
### 5.4 Create table


* For example, to analyze orders in real time by day, you can use `dt` (date) and `order_id` (order number) as the primary key, with the remaining columns as metric columns. The table creation statement is as follows:


```sql
create table orders (
    dt date NOT NULL,
    order_id bigint NOT NULL,
    user_id int NOT NULL,
    merchant_id int NOT NULL,
    good_id int NOT NULL,
    good_name string NOT NULL,
    price int NOT NULL,
    cnt int NOT NULL,
    revenue int NOT NULL,
    state tinyint NOT NULL
) PRIMARY KEY (dt, order_id)
PARTITION BY RANGE(`dt`) (
    PARTITION p20210820 VALUES [('2021-08-20'), ('2021-08-21')),
    PARTITION p20210821 VALUES [('2021-08-21'), ('2021-08-22')),
    PARTITION p20210929 VALUES [('2021-09-29'), ('2021-09-30')),
    PARTITION p20210930 VALUES [('2021-09-30'), ('2021-10-01'))
) DISTRIBUTED BY HASH(order_id)
PROPERTIES (
    "replication_num" = "3",
    "enable_persistent_index" = "true"
);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The <code>DISTRIBUTED BY HASH</code> clause must be used to specify the bucket key when creating a table; otherwise, table creation fails.</div>


* <div data-tips="true" data-tips-type="warning">Since version 2.5.7, StarRocks supports automatically setting the number of buckets (BUCKETS) when creating tables and adding partitions, so you do not need to set the number of buckets manually.</div>


* For example, to analyze user status in real time by region and recent activity time, you can use the `user_id` column representing the user ID as the primary key, and the `address` column representing the region and the `last_active` column representing the recent activity time as sorting columns. The table creation statement is as follows:


```sql
create table users (
    user_id bigint NOT NULL,
    name string NOT NULL,
    email string NULL,
    address string NULL,
    age tinyint NULL,
    sex tinyint NULL,
    last_active datetime,
    property0 tinyint NOT NULL,
    property1 tinyint NOT NULL,
    property2 tinyint NOT NULL,
    property3 tinyint NOT NULL
) PRIMARY KEY (user_id)
DISTRIBUTED BY HASH(user_id)
ORDER BY(`address`,`last_active`)
PROPERTIES (
    "replication_num" = "3",
    "enable_persistent_index" = "true"
);
```


<span id="_5-5-使用说明"></span>
### 5.5 Usage notes


* Note on primary keys:

   * In the table creation statement, the primary key must be defined before other columns.

   * The primary key is defined using `PRIMARY KEY`.

   * The primary key must satisfy the uniqueness constraint, and the values of its columns cannot be modified. In this example, the primary key is `dt` and `order_id`.

   * The primary key supports the following data types: BOOLEAN, TINYINT, SMALLINT, INT, BIGINT, LARGEINT, DATE, DATETIME, VARCHAR/STRING. It cannot be NULL.

   * Partition columns and bucket columns must be included in the primary key.

* `enable_persistent_index`: Whether to persist the primary key index, storing the primary key index in both disk and memory to prevent excessive memory usage by the primary key index. Generally, after persisting the primary key index, the memory occupied by the primary key index is reduced to one\-tenth of its previous size. You can configure this parameter in `PROPERTIES` when creating the table. The value range is `true` or `false` (default).

> * Since version 2.3.0, StarRocks supports configuring this parameter.

> * If the disk is a solid\-state drive (SSD), it is recommended to set it to `true`. If the disk is a hard disk drive (HDD) and the import frequency is not high, it can also be set to `true`.

> * After creating the table, to modify this parameter, see ALTER TABLE [修改表的属性](https://docs.byteplus.com/docs/E-MapReduce/109522#%E4%BF%AE%E6%94%B9%E8%A1%A8%E7%9A%84%E5%B1%9E%E6%80%A7).

> * Since version 3.1, the compute\-storage separation mode supports creating tables using the primary key model, and since version 3.1.4, supports persistent indexes based on local disks.

* If persistent indexing is not enabled, the primary key index resides in memory during import, which may result in high memory usage. Therefore, it is recommended to follow these suggestions:

   * Set the number and length of primary key columns appropriately. It is recommended to use data types that occupy less memory space for the primary key, such as INT, BIGINT, and so on. Using VARCHAR is not recommended for now.

   * Before creating the table, estimate the memory space occupied by the primary key index based on the data type of the primary key and the number of rows in the table to avoid memory overflow. The following example illustrates how to calculate the memory space occupied by the primary key index:

      * Assume there is a primary key model, with the primary key being `dt` and `id`, and the data types are DATE (4 bytes) and BIGINT (8 bytes). The primary key therefore occupies 12 bytes.

      * Assume the table's hot data contains 10 million rows, stored as three replicas.

      * The memory usage calculation is as follows: `(12 + 9 (fixed overhead per row)) * 10 million * 3 * 1.5 (average additional overhead for hash table) = 945 MB`

* By specifying the sorting key with the `ORDER BY` keyword, you can set any combination of columns as the sorting key.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If a sort key is specified, a prefix index is built based on the sort key; if no sort key is specified, a prefix index is built based on the primary key.</div>


* ALTER TABLE is supported for modifying the table structure, but there are the following important notes:

   * Modifying the primary key is not supported.

   * For the sorting key, ALTER TABLE ... ORDER BY ... is supported to reassign the sorting key. Deleting the sorting key and modifying the data type of columns in the sorting key are not supported.

   * Adjusting the column order is not supported.

* Since version 2.3, columns other than the primary key additionally support the BITMAP and HLL data types.

* When creating a table, it is supported to create indexes such as BITMAP and Bloom Filter for columns other than the primary key.

* Since version 2.4, tables based on the primary key model support creating [StarRocks table model design](https://docs.byteplus.com/docs/E-MapReduce/109522).


<span id="_6-表模型最佳实践"></span>
## 6 Table model best practices

You can optimize StarRocks performance during the table creation phase in the following ways.

<span id="_6-1-选择表类型"></span>
### 6.1 Choose the table type

StarRocks supports four table types: primary key table (PRIMARY KEY), aggregate table (AGGREGATE KEY), unique key table (UNIQUE KEY), and duplicate key table (DUPLICATE KEY). In all four types of tables, data is sorted based on the KEY.


* **Aggregate table**

* In aggregate tables, if the Key columns of newly written records are the same as those of existing records in the table, the new and old records are aggregated. Currently supported aggregation functions are SUM, MIN, MAX, and REPLACE. Aggregate tables can aggregate data in advance and are suitable for reporting and multidimensional analysis workloads.


```sql
CREATE TABLE site_visit
(
    siteid      INT,
    city        SMALLINT,
    username    VARCHAR(32),
    pv BIGINT   SUM DEFAULT '0'
)
AGGREGATE KEY(siteid, city, username)
DISTRIBUTED BY HASH(siteid);
```



* **Unique key table (UNIQUE KEY)** 

* In unique key tables, if the Key columns of newly written records are the same as those of existing records in the table, the new record will overwrite the old record. Currently, the implementation of UNIQUE KEY is the same as the REPLACE aggregation method of AGGREGATE KEY, and essentially they can be considered equivalent. Unique key tables are suitable for analytical workloads that require updates.


```sql
CREATE TABLE sales_order
(
    orderid     BIGINT,
    status      TINYINT,
    username    VARCHAR(32),
    amount      BIGINT DEFAULT '0'
)
UNIQUE KEY(orderid)
DISTRIBUTED BY HASH(orderid);
```



* **Duplicate key table (DUPLICATE KEY)** 

* Duplicate key tables are only used for sorting; records with the same DUPLICATE KEY will coexist. Duplicate key tables are suitable for analytical workloads where data does not need to be aggregated in advance.


```sql
CREATE TABLE session_data
(
    visitorid   SMALLINT,
    sessionid   BIGINT,
    visittime   DATETIME,
    city        CHAR(20),
    province    CHAR(20),
    ip          varchar(32),
    brower      CHAR(20),
    url         VARCHAR(1024)
)
DUPLICATE KEY(visitorid, sessionid)
DISTRIBUTED BY HASH(sessionid, visitorid);
```



* **Primary key table (PRIMARY KEY)** 

* Primary key tables ensure that only one record exists under the same primary key. Compared to update tables, primary key tables do not require aggregation operations during queries and support predicate and index pushdown, enabling efficient queries while supporting scenarios such as real\-time and frequent updates.


```sql
CREATE TABLE orders (
    dt date NOT NULL,
    order_id bigint NOT NULL,
    user_id int NOT NULL,
    merchant_id int NOT NULL,
    good_id int NOT NULL,
    good_name string NOT NULL,
    price int NOT NULL,
    cnt int NOT NULL,
    revenue int NOT NULL,
    state tinyint NOT NULL
)
PRIMARY KEY (dt, order_id)
DISTRIBUTED BY HASH(order_id);
```


<span id="_6-2-使用-colocate-table"></span>
### 6.2 Use Colocate Table

StarRocks supports storing related tables with the same distribution on shared bucket columns, allowing JOIN operations between related tables to be performed locally and thereby accelerating queries. For more information, refer to [Colocate Join](https://docs.starrocks.io/zh/docs/using_starrocks/Colocate_join/).

```sql
CREATE TABLE colocate_table
(
    visitorid   SMALLINT,
    sessionid   BIGINT,
    visittime   DATETIME,
    city        CHAR(20),
    province    CHAR(20),
    ip          varchar(32),
    brower      CHAR(20),
    url         VARCHAR(1024)
)
DUPLICATE KEY(visitorid, sessionid)
DISTRIBUTED BY HASH(sessionid, visitorid)
PROPERTIES(
    "colocate_with" = "group1"
);
```


<span id="_6-3-使用星型模型"></span>
### 6.3 Use star schema

StarRocks supports choosing a more flexible star schema to replace the traditional modeling approach of wide tables. With the star schema, you can use a view instead of a wide table for modeling and directly perform queries using multi\-table joins. In comparisons using the standard SSB test set, StarRocks shows no significant performance degradation for multi\-table joins compared to single\-table queries.

The disadvantages of wide tables compared to the star schema include:


* Higher cost for dimension updates. In wide tables, updates to dimension information affect the entire table, and the frequency of these updates directly impacts query efficiency.

* Higher maintenance cost. Building wide tables requires additional development work, storage space, and data backfill cost.

* Higher import cost. Wide tables have a larger number of schema fields, and aggregate tables may contain more key columns. The number of columns that need to be sorted during import increases, resulting in longer import times.


It is recommended to prioritize the star schema to achieve efficient metric analysis while maintaining flexibility. However, if your business requires high concurrency or low latency, you can still choose the wide table model for acceleration. StarRocks provides wide table query performance comparable to ClickHouse.

<span id="_6-4-使用分区和分桶"></span>
### 6.4 Use partitions and buckets

StarRocks supports two\-level partitioned storage: the first level is RANGE partitions (Partition), and the second level is HASH buckets (Bucket).

RANGE partitions are used to divide data into different intervals, which logically is equivalent to splitting the original table into multiple sub\-tables. In production environments, most users partition by time. The following are the benefits of time\-based partitioning:


* It enables differentiation between hot and cold data.

* You can use the StarRocks tiered storage (SSD + SATA) feature.

* Deleting data by partition is faster.


HASH bucketing refers to dividing data into different buckets based on hash values.


* It is recommended to use columns with high cardinality for bucketing to avoid data skew.

* To facilitate data recovery, it is recommended to keep the size of a single bucket small. The compressed data in each bucket should be kept between 100 MB and 1 GB. When creating a table or adding partitions, it is recommended to reasonably consider the number of buckets. Different partitions can specify different numbers of buckets.

* It is not recommended to use random bucketing. When creating a table, specify clear hash bucket columns.


<span id="_6-5-使用稀疏索引和-bloomfilter"></span>
### 6.5 Use sparse indexes and Bloom filters

StarRocks supports ordered data storage and builds sparse indexes on top of ordered data, with an index granularity of block (1,024 rows).

The sparse index selects a fixed\-length prefix from the schema as its index content. Currently, StarRocks selects a 36\-byte prefix as the index.

When creating a table, it is recommended to place fields that are commonly used as filters in queries at the front of the schema. Fields with higher cardinality and higher query frequency should be placed further forward. Fields of type VARCHAR can only be used as the last field in a sparse index, because the index will be truncated at the VARCHAR field. If VARCHAR data appears earlier, the index length may be less than 36 bytes.

For example, for the above `site_visit` table, its sort columns include `siteid`, `city`, and `username`. Among them, `siteid` occupies 4 bytes, `city` occupies 2 bytes, and `username` occupies 32 bytes. Therefore, the prefix index content of this table consists of the first 30 bytes of `siteid` + `city` + `username`.

In addition to sparse indexes, StarRocks also provides Bloom filter indexes. Bloom filter indexes are particularly effective for filtering columns with high cardinality. To place VARCHAR fields at the front, you can create a Bloom filter index.

<span id="_6-6-使用倒排索引"></span>
### 6.6 Use inverted indexes

StarRocks supports inverted indexes, which are built using bitmap technology (bitmap index). Indexes can be applied to all columns of detail tables, as well as to the key columns of aggregate and update tables. Bitmap indexes are suitable for columns with a small value space, such as gender, city, province, and other information columns. As the value space increases, the bitmap index will expand accordingly.

<span id="_6-7-使用物化视图"></span>
### 6.7 Using materialized views

A materialized view (Rollup) can essentially be understood as a materialized index of the base table. When creating a materialized view, you can select only some columns from the base table as the schema, and the order of fields in the schema can also differ from that of the base table. The following situations may warrant creating a materialized view:


* The base table has a low degree of aggregation. This is usually because the base table contains fields with high cardinality. In this case, you can consider selecting some columns to create a materialized view. For the above `site_visit` table, `siteid` may result in a low degree of data aggregation. If there is a frequent need to count `pv` by city, you can create a materialized view containing only `city` and `pv`.


```sql
ALTER TABLE site_visit ADD ROLLUP rollup_city(city, pv);
```



* The prefix index in the base table cannot be hit, which is usually because the way the base table is created cannot cover all query patterns. In this case, you can consider adjusting the column order and creating a materialized view. For the above `session_data` table, if, in addition to analyzing visits by `visitorid`, there are also scenarios for analysis by `browser` and `province`, a separate materialized view can be created.


```sql
ALTER TABLE session_data ADD ROLLUP rollup_brower(brower,province,ip,url) DUPLICATE KEY(brower,province);
```


<span id="_6-8-优化导入性能"></span>
### 6.8 Optimizing import performance

StarRocks currently provides two import methods: Broker Load and Stream Load, and uses an import label to identify a batch import. StarRocks ensures atomicity for a single batch import, even when importing multiple tables in a single batch.


* Stream Load: Imports data via HTTP streaming, used for micro\-batch imports. In this mode, the import latency for 1 MB of data can be maintained within seconds, making it suitable for high\-frequency imports.

* Broker Load: Imports data in batches by pulling, suitable for importing large volumes of data.


<span id="_6-9-优化-schema-change-性能"></span>
### 6.9 Optimizing schema change performance

StarRocks currently supports three schema change methods: Sorted Schema Change, Direct Schema Change, and Linked Schema Change.


* Sorted Schema Change: Changes the column sorting order and requires re\-sorting the data. For example, deleting a column from the sort key and reordering fields.


```sql
ALTER TABLE site_visit DROP COLUMN city;
```



* Direct Schema Change: Does not require re\-sorting, but a data transformation is needed. For example, modifying the column type or adding a column to a sparse index.


```sql
ALTER TABLE site_visit MODIFY COLUMN username varchar(64);
```



* Linked Schema Change: No data conversion is required; the change is completed immediately. For example, adding a column.


```sql
ALTER TABLE site_visit ADD COLUMN click bigint SUM default '0';
```


It is recommended to carefully design the schema when creating a table to accelerate subsequent schema change operations.
