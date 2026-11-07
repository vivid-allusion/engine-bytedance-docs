---
title: "Serverless StarRocks table model design"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_StarRocks_table_model_design"
---

<span id="_1-starrocks-表设计"></span>
## 1 StarRocks table design

<span id="_1-1-列式存储"></span>
### 1.1 Columnar storage

Tables in StarRocks consist of rows and columns. Each row of data corresponds to a user record, and all values in a column have the same data type. All data rows have the same number of columns, and columns can be dynamically added or removed. In StarRocks, the columns of a table can be divided into dimension columns (also known as Key columns) and metric columns (also known as Value columns). Dimension columns are used for grouping and sorting.

In StarRocks, table data is stored by column. Physically, each column of data undergoes block encoding, compression, and other operations, and is then persistently stored on non\-volatile devices. Logically, each column of data can be viewed as an array composed of elements of the same type. All column values of a row are arranged in their respective arrays in column order, that is, they share the same array index. The array index is implicit and does not need to be stored. All rows in the table are sorted by dimension columns in multiple levels, and the position after sorting is the row number of that row.

<span id="_1-2-索引"></span>
### 1.2 Index

StarRocks uses prefix index (Prefix Index) and column\-level indexes to quickly locate the starting row number of the target row in the data block.

The principle of StarRocks table design is illustrated in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79394c77407e7d3f06d63a3a3fe97e17.png) </span>

The data organization in a table mainly consists of three parts:


* Prefix index

* Every 1,024 rows of data in the table form a logical data block (Data Block). Each logical data block stores an index entry in the prefix index table. The content of the index entry is the prefix formed by the dimension columns of the first row in the data block, with a length not exceeding 36 bytes. The prefix index is a sparse index. By searching the prefix index table with the prefix formed by the dimension columns of a certain row in the table, the starting row number of the logical data block containing that row can be determined.

* Column\-level data block

* Each column of data in the table is stored in blocks of 64 KB. The data block is encoded and compressed as a Unit, and also serves as an I/O Unit, being written back to or read from the device as a whole.

* Column\-level index

* Each column in the table has an independent row number index. In the row number index table, the data block of the column corresponds to the row number one\-to\-one. Each row number index entry consists of the starting row number, position, and length information of the corresponding data block. By searching the row number index table using the row number of a specific row of data, you can obtain the location of the data block containing the corresponding row number. After reading the target data block, you can further search for the data.


Therefore, the process of searching for a row of data using the prefix formed by the dimension columns of that row includes the following five steps:


1. First, search the prefix index table to obtain the starting row number of the logical data block.

2. Search the row number index of the dimension column to locate the data block of the dimension column.

3. Read the data block.

4. Decompress and decode the data block.

5. Find the data item corresponding to the dimension column prefix in the data block.


<span id="_2-明细模型"></span>
## 2 Detail model

The detail model is the default table creation model. If no model is specified when creating a table, a detail\-type table is created by default.

You can define sorting keys when creating a table. If the query filter conditions include sorting keys, StarRocks can quickly filter data and improve query efficiency. The detail model is suitable for use cases such as log data analysis. It supports appending new data and does not support modifying historical data.

<span id="_2-1-适用场景"></span>
### 2.1 Use cases


* Analyze raw data, such as raw logs and raw operation records.

* The query method is flexible and does not need to be limited to pre\-aggregated analysis methods.

* When importing log data or time\-series data, the main characteristic is that old data is not updated, only new data is appended.


<span id="_2-2-创建表"></span>
### 2.2 Create table

For example, to analyze data for a certain type of event within a specific time range, you can use event time (`event_time`) and event type (`event_type`) as sorting keys.

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



* <div data-tips="true" data-tips-type="warning">Versions prior to StarRocks 3.1: In the detail model, you must use the <code>DISTRIBUTED BY HASH</code> clause to specify the bucket key when creating a table; otherwise, table creation will fail. For more information about bucket keys, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E5%88%86%E6%A1%B6">分桶</a>.</div>


* <div data-tips="true" data-tips-type="warning">StarRocks 3.1 and later versions: In the detail model, you can also omit the <code>DISTRIBUTED BY</code> clause in the table creation statement. StarRocks will default to random bucketing (<code>DISTRIBUTED BY RANDOM</code>), and data will be evenly and randomly written to each bucket within the partition in a round\-robin manner.</div>



<span id="_2-3-使用说明"></span>
### 2.3 Usage instructions


* Explanation regarding sorting keys:

   * In the table creation statement, sorting keys must be defined before other columns.

   * The sorting key can be explicitly defined using `DUPLICATE KEY`. In this example, the sorting keys are `event_time` and `event_type`.

> * If not specified, the first three columns of the table are selected as the default sorting keys.

* In the detail model, the sorting key can be some or all of the dimension columns.

* When creating a table, you can create indexes such as BITMAP and Bloom Filter for metric columns.


<span id="_3-聚合模型"></span>
## 3 Aggregation model

When creating a table, you can define sorting keys and metric columns, and specify aggregation functions for metric columns. When multiple records have the same sorting key, the metric columns will be aggregated. When analyzing statistics and summary data, the aggregation model can reduce the amount of data processed during queries and improve query efficiency.

<span id="_3-1-适用场景"></span>
### 3.1 Use cases

Used for analyzing statistics and summary data. For example:


* By analyzing website or app traffic, calculate the total visit duration and total number of times for users.

* Advertising vendors provide advertisers with statistics such as total ad clicks, total impressions, and spending statistics.

* By analyzing the annual transaction data of e\-commerce, identify popular products among various consumer groups for a specified quarter or month.


In these scenarios, data querying and importing have the following characteristics:


* Most queries are summary\-type queries, such as SUM, MAX, MIN, and similar queries.

* There is no need to query the original detail data.

* Updates to old data are infrequent; only new data is appended.


<span id="_3-2-原理"></span>
### 3.2 Principles

From the data import stage to the data query stage, data with the same sorting key within the aggregation model will be aggregated multiple times. The specific timing and mechanism of aggregation are as follows:


1. Data import stage: When data is imported into the aggregation model in batches, each batch forms a version. Within a version, data with the same sorting key will be aggregated once.

2. Background file merge stage (Compaction): When data is imported into the aggregation model in multiple batches, multiple versions of files are generated. When multiple versions are periodically merged into a consolidated file, data with the same sorting key will be aggregated once.

3. Query phase: Data with the same sort key across all versions is aggregated, and then the query result is returned.


Therefore, repeated aggregation of data in the aggregation model can reduce the amount of data that needs to be processed during queries, thereby improving query efficiency.

For example, import the following data into the aggregation model, with Date and Country as the sort keys:


|Date |Country |PV |
|---|---|---|
|2020.05.01 |CHN |1 |
|2020.05.01 |CHN |2 |
|2020.05.01 |USA |3 |
|2020.05.01 |USA |4 |


In the aggregation model, the above four records will be aggregated into two records. This significantly reduces the amount of data to be processed in subsequent query operations.


|Date |Country |PV |
|---|---|---|
|2020.05.01 |CHN |3 |
|2020.05.01 |USA |7 |


<span id="_3-3-创建表"></span>
### 3.3 Create table

For example, you may need to analyze the total number of times users from different cities visit different web pages within a certain period. You can use the web page address `site_id`, date `date`, and city code `city_code` as sort keys, use the total number of times `pv` as the indicator column, and specify the aggregate function SUM for the indicator column `pv`.

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



* <div data-tips="true" data-tips-type="warning">You must use the <code>DISTRIBUTED BY HASH</code> clause to specify the bucket key when creating a table. For more information about bucket keys, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E5%88%86%E6%A1%B6">分桶</a>.</div>


* <div data-tips="true" data-tips-type="warning">Since version 2.5.7, StarRocks supports automatically setting the number of buckets (BUCKETS) when creating tables and adding partitions, so you do not need to manually set the number of buckets. For more information, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E7%A1%AE%E5%AE%9A%E5%88%86%E6%A1%B6%E6%95%B0%E9%87%8F">确定分桶数量</a>.</div>



<span id="_3-4-使用说明"></span>
### 3.4 Note


* Note

   * In the table creation statement, **sort keys must be defined before other columns**.

   * Sort keys can be explicitly defined using `AGGREGATE KEY`.

> ```Plain Text
  * If `AGGREGATE KEY` does not include all dimension columns (columns other than indicator columns), table creation will fail.
  * If sort keys are not explicitly defined using `AGGREGATE KEY`, all columns except indicator columns are considered sort keys by default.
```



* Sort keys must satisfy the uniqueness constraint, must include all dimension columns, and the values of these columns will not be updated.

* Indicator column: By specifying an aggregate function after the column name, the column is defined as an indicator column. Generally, this refers to data that needs to be summarized and counted.

* Aggregate function: The aggregate function used by the indicator column. For supported aggregate functions in the aggregation model, see [Serverless StarRocks table model design](https://docs.byteplus.com/docs/E-MapReduce/109151).

* During queries, sort keys can be filtered before multi\-version aggregation, while indicator columns are filtered after multi\-version aggregation. Therefore, it is recommended to use frequently filtered fields as sort keys, so that data can be filtered before aggregation, thereby improving query performance.

* When creating a table, it is not supported to create BITMAP, Bloom Filter, or other indexes for indicator columns.


<span id="_4-更新模型"></span>
## 4 Update model

When creating a table, you can define primary keys and metric columns. When querying, the latest data among the group of records with the same primary key is returned. Compared to the detail model, the update model simplifies the data import process and better supports real\-time and frequent update scenarios.

<span id="_4-1-适用场景"></span>
### 4.1 Use cases

Business scenarios with real\-time and frequent updates, such as analyzing e\-commerce orders. In e\-commerce scenarios, the status of orders often changes, and the number of daily order updates can exceed hundreds of millions.

<span id="_4-2-原理"></span>
### 4.2 Principles

The update model can be regarded as a special case of the aggregate model, where the aggregation function specified for metric columns is REPLACE, returning the latest data among the group of records with the same primary key.

Data is imported into the update model in multiple batches, with each batch assigned a version number. Therefore, data with the same primary key may have multiple versions, and queries return the data with the latest version (that is, the largest version number). Compared to the detail model, the update model supports real\-time and frequent updates more effectively by simplifying the import process.

For example, in the table below, `ID` is the primary key, `value` is the metric column, and `_version` is the internal version number in StarRocks. Among them, the data with `ID` equal to 1 has two import batches, with version numbers `1` and `2` respectively; the data with `ID` equal to `2` has three import batches, with version numbers `3`, `4`, and `5` respectively.


|ID |value |_version |
|---|---|---|
|1 |100 |1 |
|1 |101 |2 |
|2 |100 |3 |
|2 |101 |4 |
|2 |102 |5 |


When querying the data with `ID` equal to `1`, only the latest version `2` is returned. When querying the data with `ID` equal to `2`, only the latest version `5` is returned. The final query result is as follows:


|ID |value |
|---|---|
|1 |101 |
|2 |102 |


<span id="_4-3-创建表"></span>
### 4.3 Create table

In e\-commerce order analysis scenarios, order status is often analyzed by date. Therefore, frequently used filter fields such as order creation time `create_time` and order number `order_id` can be used as primary keys, while other columns such as order status `order_state` and total order price `total_price` can be used as metric columns. This approach meets the need for real\-time updates to order status and enables fast filtering during queries.

In this business scenario, the table creation statement is as follows:

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



* <div data-tips="true" data-tips-type="warning">You must use the <code>DISTRIBUTED BY HASH</code> clause to specify the bucket key when creating a table. For more information about bucket keys, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E5%88%86%E6%A1%B6">分桶</a>.</div>


* <div data-tips="true" data-tips-type="warning">Since version 2.5.7, StarRocks supports automatically setting the number of buckets (BUCKETS) when creating tables and adding partitions, so you do not need to manually set the number of buckets. For more information, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E7%A1%AE%E5%AE%9A%E5%88%86%E6%A1%B6%E6%95%B0%E9%87%8F">确定分桶数量</a>.</div>



<span id="_4-4-使用说明"></span>
### 4.4 Usage notes


* Note on primary keys:

   * In the CREATE TABLE statement, the primary key must be defined before other columns.

   * The primary key is defined using `UNIQUE KEY`.

   * The primary key must satisfy the uniqueness constraint, and the values of its columns are not modified.

   * Set an appropriate primary key.

      * During queries, the primary key can be filtered before aggregation, whereas filtering on metric columns typically occurs after multi\-version aggregation. Therefore, it is recommended to use frequently filtered fields as the primary key so that data can be filtered before aggregation, improving query performance.

      * All primary keys are compared during aggregation, so avoid including too many columns in the primary key to prevent reduced query performance. If a column is only occasionally used as a filter condition in queries, it is not recommended to include it in the primary key.

* When creating a table, creating indexes such as BITMAP or Bloom Filter for metric columns is not supported.


<span id="_5-主键模型"></span>
## 5 Primary key model

The primary key model supports separately defining primary keys and sort keys. When importing data into a table using the primary key model, the data is first sorted by the sort key and then stored. When querying, the latest data from the group of rows with the same primary key is returned. Compared to the update model, the primary key model does not require aggregation operations during queries and supports predicate and index pushdown, enabling efficient queries while supporting **real\-time and frequent updates** scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Prior to version 3.0, the primary key model did not support separately defining the primary key and sort key.</div>


* <div data-tips="true" data-tips-type="tip">Since version 3.1, the storage\-compute separation mode supports creating tables with the primary key model, and since version 3.1.4, supports persistent indexes based on local disks.</div>



<span id="_5-1-适用场景"></span>
### 5.1 Use cases

The primary key model is suitable for real\-time and frequent update scenarios, such as:


* **Real\-time integration of transactional data into StarRocks**. In transactional databases, besides inserting data, there are usually many update and delete operations. Therefore, when synchronizing transactional database data to StarRocks, it is recommended to use the primary key model.[Serverless StarRocks table model design](https://docs.byteplus.com/docs/E-MapReduce/109151) Real\-time synchronization of insert, update, and delete data to the primary key model can simplify the data synchronization process, and compared to the update model with the Merge\-On\-Read strategy, query performance can be improved by 3 to 10 times.

* **Easily achieve multi\-stream JOINs using partial column updates**. In user profiling and similar analysis scenarios, a wide table approach is typically used to enhance multidimensional analysis performance and simplify the data analyst's usage model. In these scenarios, upstream data often comes from multiple different businesses (such as shopping and consumption, express delivery, banking, and more) or systems (such as machine learning systems that calculate various user tag attributes). The partial column update feature of the primary key model perfectly meets these requirements: each business can directly update the columns relevant to its operations as needed, while continuing to benefit from the primary key model's real\-time synchronization of data additions, deletions, and modifications, as well as efficient query performance.


<span id="_5-2-注意事项"></span>
### 5.2 Important notes


* If persistent indexing is enabled, the primary key model significantly reduces the memory usage of the primary key index. During data import, a small portion of the primary key index resides in memory, while most of the primary key index is stored on disk. **The maximum length of a single encoded primary key is 128 bytes**.

* If persistent indexing is not enabled, the primary key model is suitable for scenarios where primary key space usage is relatively controllable, since the primary key index is loaded into memory during import. **The maximum length and memory usage limit of a single encoded primary key is 128 bytes**. In the following two scenarios, primary key space usage is relatively controllable:

   * **Data exhibits hot and cold characteristics**, meaning only the hot data from the past few days is frequently modified, while older cold data is rarely changed. For example, a MySQL order table is synchronized in real time to StarRocks for analytical queries. In this case, data is partitioned by day, and order modifications are concentrated in newly created orders from the past few days. Once older orders are completed, they are no longer updated. Therefore, their primary key indexes are not loaded during import and do not occupy memory; only the indexes from the past few days are loaded into memory.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53f45f2f4f9c972ce0822d5345f4d0d6.png) </span>

> * As shown in the figure, data is partitioned by day, and updates are more frequent in the two most recent partitions.

>    * **Wide tables** (hundreds to thousands of columns). The primary key only occupies a very small portion of the entire dataset, resulting in low memory overhead. For example, in user status and profile tables, although there are many columns, the total number of users is not large (tens of millions to hundreds of millions), so the memory usage of the primary key index is relatively manageable.

> * As shown in the figure, in wide tables, the primary key only occupies a small part, and there are not many rows.


<span id="_5-3-原理"></span>
### 5.3 Principle

The primary key model is supported by a newly designed and developed storage engine in StarRocks. Compared to the update model, the primary key model organizes metadata, reads, and writes in a completely different way. It does not require aggregation operations and supports predicate and index pushdown, which greatly improves query performance.

The update model generally adopts a Merge\-On\-Read strategy. Although processing during writes is simple and efficient, queries require online aggregation of multiple versions. Moreover, due to the presence of the Merge operator, predicates and indexes cannot be pushed down, which severely impacts query performance.

The primary key model, on the other hand, uses a Delete+Insert strategy to ensure that only one record exists for each primary key, thereby completely avoiding the Merge operation. The specific implementation is as follows:


* When StarRocks receives an update operation for a record, it locates the record using the primary key index, marks it as deleted, and then inserts a new record. This is equivalent to rewriting an Update as Delete+Insert.

* When StarRocks receives a delete operation for a record, it locates the record using the primary key index and marks it as deleted.


As a result, queries do not require aggregation operations, and predicate and index pushdown are not affected, ensuring efficient query execution.

<span id="_5-4-创建表"></span>
### 5.4 Create tables


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



* <div data-tips="true" data-tips-type="warning">You must use the <code>DISTRIBUTED BY HASH</code> clause to specify the bucket key when creating a table; otherwise, table creation will fail. For more information about bucket keys, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E5%88%86%E6%A1%B6">分桶</a>.</div>


* <div data-tips="true" data-tips-type="warning">Since version 2.5.7, StarRocks supports automatically setting the number of buckets (BUCKETS) when creating tables and adding partitions, so you do not need to manually set the number of buckets. For more information, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109151#%E7%A1%AE%E5%AE%9A%E5%88%86%E6%A1%B6%E6%95%B0%E9%87%8F">确定分桶数量</a>.</div>


* For example, to analyze user data in real time by region and recent activity time, you can use the `user_id` column representing the user ID as the primary key, and the `address` column representing the region and the `last_active` column representing the recent activity time as sort keys. The table creation statement is as follows:


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
### 5.5 Note


* Note on the primary key:

   * In the table creation statement, the primary key must be defined before other columns.

   * The primary key is defined using `PRIMARY KEY`.

   * The primary key must satisfy the uniqueness constraint, and the values of its columns cannot be modified. In this example, the primary key is `dt` and `order_id`.

   * The primary key supports the following data types: BOOLEAN, TINYINT, SMALLINT, INT, BIGINT, LARGEINT, DATE, DATETIME, VARCHAR/STRING. It cannot be NULL.

   * Partition columns and bucket columns must be included in the primary key.

* `enable_persistent_index`: Whether to persist the primary key index, storing the primary key index in both disk and memory to prevent excessive memory usage. Typically, after persisting the primary key index, the memory occupied by the primary key index is reduced to one\-tenth of the previous amount. You can configure this parameter in `PROPERTIES` when creating the table. The value range is `true` or `false` (default).

> * Since version 2.3.0, StarRocks supports configuring this parameter.

> * If the disk is a solid\-state drive (SSD), it is recommended to set it to `true`. If the disk is a hard disk drive (HDD) and the import frequency is not high, it can also be set to `true`.

> * After creating the table, to modify this parameter, see ALTER TABLE [修改表的属性](https://docs.byteplus.com/docs/E-MapReduce/109151#%E4%BF%AE%E6%94%B9%E8%A1%A8%E7%9A%84%E5%B1%9E%E6%80%A7) .

> * Since version 3.1, the compute\-storage separation mode supports creating primary key model tables, and since version 3.1.4, supports persistent indexes based on local disks.

* If persistent indexing is not enabled, the primary key index exists in memory during import, which may result in high memory usage. Therefore, it is recommended to follow these suggestions:

   * Set the number and length of primary key columns appropriately. It is recommended to use data types that occupy less memory space for the primary key, such as INT and BIGINT. It is not recommended to use VARCHAR for now.

   * Before creating the table, estimate the memory space occupied by the primary key index based on the data type of the primary key and the number of rows in the table to avoid memory overflow. The following example illustrates how to calculate the memory space occupied by the primary key index:

      * Assume there is a primary key model, with the primary key being `dt` and `id`, and the data types are DATE (4 bytes) and BIGINT (8 bytes). The primary key therefore occupies 12 bytes.

      * Assume the table's hot data has 10 million rows, stored as three replicas.

      * The memory usage calculation is as follows: `(12 + 9 (fixed overhead per row)) * 10 million * 3 * 1.5 (average hash table overhead) = 945 M`

* By specifying the sorting key using the `ORDER BY` keyword, you can set it as any combination of columns.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If a sort key is specified, a prefix index is built based on the sort key; if no sort key is specified, a prefix index is built based on the primary key.</div>


* You can use ALTER TABLE to modify the table structure, but there are the following important notes:

   * Modifying the primary key is not supported.

   * For sorting keys, ALTER TABLE ... ORDER BY ... Reassigning the sorting key is supported. Deleting sorting keys and modifying the data types of columns in sorting keys are not supported.

   * Adjusting column order is not supported.

* Since version 2.3, columns other than the primary key additionally support BITMAP and HLL data types.

* You can create indexes such as BITMAP and Bloom Filter for columns other than the primary key when creating a table.

* Since version 2.4, you can create [Serverless StarRocks table model design](https://docs.byteplus.com/docs/E-MapReduce/109151) for tables based on the primary key model.


<span id="_6-表模型最佳实践"></span>
## 6. Table model best practices

You can optimize StarRocks performance during the table creation phase in the following ways.

<span id="_6-1-选择表类型"></span>
### 6.1 Choose table type

StarRocks supports four table types: primary key table (PRIMARY KEY), aggregate table (AGGREGATE KEY), unique key table (UNIQUE KEY), and duplicate key table (DUPLICATE KEY). Data in all four types of tables is sorted based on the KEY.


* **Aggregate table**

* In aggregate tables, if the Key columns of newly written records are the same as those of existing records, the new and old records are aggregated. Currently supported aggregation functions are SUM, MIN, MAX, and REPLACE. Aggregate tables can aggregate data in advance and are suitable for reporting and multidimensional analysis workloads.


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

* In unique key tables, if the Key columns of newly written records are the same as those of existing records, the new record will overwrite the old record. Currently, the implementation of UNIQUE KEY is the same as the REPLACE aggregation method of AGGREGATE KEY, and the two can essentially be considered equivalent. Unique key tables are suitable for analytical workloads that require updates.


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

* Duplicate key tables are only used for sorting, and records with the same DUPLICATE KEY will coexist. Duplicate key tables are suitable for analytical workloads where data does not need to be aggregated in advance.


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

* Primary key tables ensure that only one record exists under the same primary key. Compared with update tables, primary key tables do not require aggregation operations during queries and support predicate and index pushdown, enabling efficient queries while supporting scenarios such as real\-time and frequent updates.


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
### 6.2 Use colocate table

StarRocks supports storing related tables with the same distribution on common bucket columns, so that JOIN operations on related tables can be performed locally, thereby accelerating queries. For more information, see [Colocate Join](https://docs.starrocks.io/zh/docs/using_starrocks/Colocate_join/).

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

StarRocks supports choosing a more flexible star schema to replace the traditional wide table modeling approach. With the star schema, you can use a view to replace the wide table for modeling and perform queries directly using multi\-table joins. In the comparison with the standard SSB test set, the multi\-table join performance of StarRocks does not show a significant decrease compared to single\-table queries.

The disadvantages of wide tables compared to the star schema include:


* Higher dimension update costs. In wide tables, updates to dimension information affect the entire table, and the update frequency directly impacts query efficiency.

* Higher maintenance costs. Building wide tables requires additional development work, storage space, and data backfill costs.

* Higher import costs. Wide tables have more schema fields, and aggregate tables may contain more key columns, which increases the number of columns that need to be sorted during import, resulting in longer import times.


Prioritize the star schema to ensure flexibility and efficient metric analysis. To accelerate workloads with high concurrency or low latency requirements, you can choose the wide table model. StarRocks provides wide table query performance comparable to ClickHouse.

<span id="_6-4-使用分区和分桶"></span>
### 6.4 Use partitioning and bucketing

StarRocks supports two\-level partitioned storage: the first level is RANGE partitioning (Partition), and the second level is HASH bucketing (Bucket).

RANGE partitioning is used to divide data into different ranges, which is logically equivalent to splitting the original table into multiple subtables. In production environments, most users partition according to time. The following are the benefits of partitioning based on time:


* It enables differentiation between hot and cold data.

* You can use the StarRocks tiered storage (SSD + SATA) feature.

* Deleting data by partition is faster.


Hash bucketing refers to dividing data into different buckets based on hash values.


* It is recommended to use columns with high cardinality for bucketing to avoid data skew.

* To facilitate data recovery, it is recommended to keep the size of each bucket small. The compressed data in each bucket should be kept between 100 MB and 1 GB. When creating a table or adding partitions, it is advisable to carefully consider the number of buckets. Different partitions can specify different numbers of buckets.

* Random bucketing is not recommended. When creating a table, specify explicit hash bucketing columns.


<span id="_6-5-使用稀疏索引和-bloomfilter"></span>
### 6.5 Using sparse indexes and Bloom filter

StarRocks supports ordered storage of data and builds sparse indexes on top of ordered data. The index granularity is block (1024 rows).

Sparse indexes select a fixed\-length prefix from the schema as the index content. Currently, StarRocks uses a 36\-byte prefix as the index.

When creating a table, it is recommended to place commonly used filter fields at the front of the schema. Fields with higher cardinality and higher query frequency should be placed further forward. Fields of type VARCHAR can only be used as the last field in a sparse index, because the index is truncated at the VARCHAR field. If VARCHAR data appears earlier, the index length may be less than 36 bytes.

For example, for the above `site_visit` table, its sorting columns include `siteid`, `city`, and `username`. Among them, `siteid` occupies 4 bytes, `city` occupies 2 bytes, and `username` occupies 32 bytes. Therefore, the prefix index content of this table is the first 30 bytes of `siteid` + `city` + `username`.

In addition to sparse indexes, StarRocks also provides Bloom filter indexes. Bloom filter indexes are effective for filtering columns with high cardinality. To place VARCHAR fields at the front, you can create Bloom filter indexes.

<span id="_6-6-使用倒排索引"></span>
### 6.6 Using inverted indexes

StarRocks supports inverted indexes, which are constructed using bitmap technology (Bitmap Index). You can apply indexes to all columns in detail tables, and to key columns in aggregate tables and update tables. Bitmap indexes are suitable for columns with a small value space, such as columns containing information like gender, city, or province. As the value space increases, the bitmap index will expand accordingly.

<span id="_6-7-使用物化视图"></span>
### 6.7 Use materialized views

A materialized view (Rollup) can essentially be understood as a materialized index of the base table. When creating a materialized view, you can select only certain columns from the base table as the schema, and the order of fields in the schema can also differ from that of the base table. The following situations are suitable for creating a materialized view:


* The data in the base table is not highly aggregated. This is usually because the base table contains fields with high cardinality. In this case, you can consider selecting some columns to create a materialized view. For the `site_visit` table mentioned above, `siteid` may result in low data aggregation. To frequently count `pv` by city, create a materialized view containing only `city` and `pv`.


```sql
ALTER TABLE site_visit ADD ROLLUP rollup_city(city, pv);
```



* The prefix index in the base table cannot be used, which is usually because the table definition of the base table cannot cover all query patterns. In this case, you can consider adjusting the column order and creating a materialized view. For the `session_data` table mentioned above, if you need to analyze visits not only by `visitorid` but also by `browser` and `province`, you can create a separate materialized view.


```sql
ALTER TABLE session_data ADD ROLLUP rollup_brower(brower,province,ip,url) DUPLICATE KEY(brower,province);
```


<span id="_6-8-优化导入性能"></span>
### 6.8 Optimize import performance

StarRocks currently provides two import methods: Broker Load and Stream Load. You can specify an import label to identify a batch of imports. StarRocks ensures atomicity for each batch import. Even when importing multiple tables in a single batch, atomicity is still guaranteed.


* Stream Load: Imports data via HTTP streaming, suitable for micro\-batch imports. In this mode, the import latency for 1 MB of data can be maintained within seconds, making it suitable for high\-frequency imports.

* Broker Load: Imports data in batches by pulling, suitable for large\-scale data imports.


<span id="_6-9-优化-schema-change-性能"></span>
### 6.9 Optimize schema change performance

StarRocks currently supports three schema change methods: Sorted Schema Change, Direct Schema Change, and Linked Schema Change.


* Sorted Schema Change: Changes the column order and requires data to be resorted. For example, deleting a column from the sorted columns or reordering fields.


```sql
ALTER TABLE site_visit DROP COLUMN city;
```



* Direct Schema Change: Does not require resorting, but a data transformation is needed. For example, modifying the column type or adding a column to a sparse index.


```sql
ALTER TABLE site_visit MODIFY COLUMN username varchar(64);
```



* Linked Schema Change: No data conversion required, completed immediately. For example, adding columns.


```sql
ALTER TABLE site_visit ADD COLUMN click bigint SUM default '0';
```


It is recommended to carefully design the schema when creating a table to accelerate subsequent schema change operations.
