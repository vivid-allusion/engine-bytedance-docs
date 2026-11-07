---
title: "EMR Serverless Doris table model design best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Doris_table_model_design_best_practices"
---

<span id="bdcdf471"></span>
## Data table model

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, Doris table models are divided into three categories: DUPLICATE KEY, UNIQUE KEY, and AGGREGATE KEY.</div>


**Recommended guidelines**

The data model is determined when the table is created and cannot be modified. Therefore, selecting an appropriate data model is very important.


1. The Duplicate model is suitable for ad\-hoc queries of any dimension. Although it also cannot leverage pre\-aggregation, it is not constrained by the aggregation model and can take advantage of the columnar storage model (only the relevant columns are read, without needing to read all key columns).

2. The Aggregate model can significantly reduce the amount of data scanned and the computational load for aggregation queries through pre\-aggregation, making it very suitable for report\-type queries with a fixed pattern. However, this model is not friendly to count(\*) queries. At the same time, because the aggregation method for value columns is fixed, it is necessary to consider semantic correctness when performing other types of aggregation queries.

3. The Unique model is designed for scenarios that require a unique primary key constraint and can ensure primary key uniqueness. However, it cannot take advantage of query benefits brought by pre\-aggregation such as materialization. For users with high performance requirements for aggregation queries, it is recommended to use the merge\-on\-write implementation introduced in version 1.2.

4. To update some columns, you can choose:

5. a. The merge\-on\-write mode of the Unique model

6. b. The REPLACE_IF_NOT_NULL aggregation method of the Aggregate model


<span id="16ce01df"></span>
### DUPLICATE KEY table model

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b870640128b94764a39f66921024d83c~tplv-goo7wpa0wc-image.image) </span>

Only the sorting columns are specified, and rows with the same key are not merged.

Applicable to analytical services where data does not need to be pre\-aggregated:


* Raw data analysis

* Log or time\-series data analysis where only new data is appended


**Best practices**

```SQL
-- For example, log data analysis that allows duplicate KEYs and only appends new data
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
DUPLICATE KEY(visitorid, sessionid) -- Used only to specify sorting columns; rows with the same KEY are not merged
DISTRIBUTED BY HASH(sessionid, visitorid) BUCKETS 10;
```


<span id="21bea63b"></span>
### AGGREGATE KEY table model

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2acc9f5c455940ccad30ef084d960148~tplv-goo7wpa0wc-image.image) </span>

When the AGGREGATE KEY is the same, new and old records are aggregated. The currently supported aggregation methods are:


1. SUM: Sums the values, accumulating the value of multiple rows.

2. REPLACE: Replacement. The value in the next batch of data will replace the value in previously imported rows.

3. MAX: Retains the maximum value.

4. MIN: Retains the minimum value.

5. REPLACE_IF_NOT_NULL: Replaces with a non\-null value. The difference from REPLACE is that null values are not replaced.

6. HLL_UNION: The aggregation method for columns of HLL type, aggregated using the HyperLogLog algorithm.

7. BITMAP_UNION: The aggregation method for columns of the BITMAP type, performing a union aggregation of bitmaps.


Suitable for reporting and multidimensional analysis scenarios:


* Website traffic analysis

* Multidimensional data report analysis


**Best practices**

```SQL
-- For example, website traffic analysis
CREATE TABLE site_visit
(
    siteid      INT,
    city        SMALLINT,
    username    VARCHAR(32),
    pv BIGINT   SUM DEFAULT '0' -- PV calculation
)
AGGREGATE KEY(siteid, city, username) -- Rows with the same KEY are merged, and non-KEY columns are aggregated according to the specified aggregation function
DISTRIBUTED BY HASH(siteid) BUCKETS 10;
```


<span id="59285272"></span>
### UNIQUE KEY table model

When the UNIQUE KEY is the same, new records overwrite old records. Prior to version 1.2, the implementation of UNIQUE KEY was essentially the same as the REPLACE aggregation method of AGGREGATE KEY. Starting from version 1.2, we introduced the merge on write implementation for UNIQUE KEY, which provides better aggregation query performance.

Applicable to analytical scenarios with update requirements:


* Order deduplication analysis

* Real\-time synchronization of insert, delete, and update operations


**Best practices**

```SQL
-- For example, order deduplication analysis
CREATE TABLE sales_order
(
    orderid     BIGINT,
    status      TINYINT,
    username    VARCHAR(32),
    amount      BIGINT DEFAULT '0'
)
UNIQUE KEY(orderid) -- Rows with the same KEY are merged
DISTRIBUTED BY HASH(orderid) BUCKETS 10;
```


<span id="2d5d0da8"></span>
## Index

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Indexes are used to help quickly filter or search for data. Currently, two main types of indexes are supported:</div>



* <div data-tips="true" data-tips-type="tip">Built\-in automatically created intelligent indexes, including prefix indexes and ZoneMap indexes.</div>


* <div data-tips="true" data-tips-type="tip">User\-created secondary indexes, including inverted indexes, bloomfilter indexes, ngram bloomfilter indexes, and bitmap indexes.</div>



<span id="33bec245"></span>
### Prefix index

This applies to the Aggregate, Unique, and Duplicate data models. The underlying data storage is sorted and stored according to the columns specified in the AGGREGATE KEY, UNIQUE KEY, and DUPLICATE KEY in their respective table creation statements. The prefix index is an indexing method that enables fast data queries based on the given prefix columns, built on top of the sorted storage.

The prefix index is a sparse index and cannot precisely locate the row where the Key resides. It can only roughly locate the range where the Key may exist, and then use a binary search algorithm to accurately locate the Key's position.

**Recommended guidelines**


1. Choosing the correct column order when creating a table can greatly improve query efficiency.

2. Because the column order is already specified when creating the table, each table has only one prefix index. For queries that use columns which cannot utilize the prefix index as conditions, the efficiency may not meet requirements. In such cases, you can manually adjust the column order by creating a materialized view.

3. The first field of the prefix index must be the most frequently queried field and should be a high cardinality field:

4. a. Important notes regarding bucket fields: These are generally fields with relatively balanced data distribution and are frequently used. It is best if they are high cardinality fields.

5. b. Int(4) + Int(4) + varchar(50), the prefix index length is only 28

6. c. Int(4) + varchar(50) + Int(4), the prefix index length is only 24

7. d. varchar(10) + varchar(50), the prefix index length is only 30

8. e. Prefix index (36 bytes): The first field delivers the best query performance. When a prefix index encounters a field of varchar type, it automatically truncates to the first 20 characters.

9. f. Whenever possible, include the most commonly used query fields in the prefix index. If this is not feasible, they can be placed in the bucket field.

10. The field length in the prefix index should be specified as precisely as possible, because Doris only supports prefix indexing for the first 36 bytes.

11. If a certain range of data is difficult to design using partitioning, bucketing, or prefix indexing, consider introducing an inverted index to accelerate queries.


<span id="880dc167"></span>
### ZoneMap index

The ZoneMap index is automatically maintained for each column in the columnar storage format, including Min/Max values, the number of null values, and other information. During data queries, the scan range is selected based on ZoneMap statistics for fields filtered by range conditions.

For example, to filter the age field, the query statement is as follows:

`SELECT * FROM table WHERE age > 0 and age < 51;`

If the Short Key Index is not hit, the query conditions for age in the statement are used with the ZoneMap index to find the appropriate data range to scan, reducing the number of pages to be scanned.

<span id="7eae9100"></span>
### Inverted index

Starting from version 2.0.0, Doris supports inverted indexes, which can be used for full\-text search of text types, equality and range queries for ordinary numeric and date types, and quickly filter rows that meet the conditions from large volumes of data.

**Best practices**

```SQL
-- Creation example: Can be specified when creating the table or added later; the following example specifies during table creation
CREATE TABLE table_name
(
  columns_difinition,
  INDEX idx_name1(column_name1) USING INVERTED [PROPERTIES("parser" = "english|unicode|chinese")] [COMMENT 'your comment']
  INDEX idx_name2(column_name2) USING INVERTED [PROPERTIES("parser" = "english|unicode|chinese")] [COMMENT 'your comment']
  INDEX idx_name3(column_name3) USING INVERTED [PROPERTIES("parser" = "chinese", "parser_mode" = "fine_grained|coarse_grained")] [COMMENT 'your comment']
  INDEX idx_name4(column_name4) USING INVERTED [PROPERTIES("parser" = "english|unicode|chinese", "support_phrase" = "true|false")] [COMMENT 'your comment']
  INDEX idx_name5(column_name4) USING INVERTED [PROPERTIES("char_filter_type" = "char_replace", "char_filter_pattern" = "._"), "char_filter_replacement" = " "] [COMMENT 'your comment']
  INDEX idx_name5(column_name4) USING INVERTED [PROPERTIES("char_filter_type" = "char_replace", "char_filter_pattern" = "._")] [COMMENT 'your comment']
)
table_properties;

-- Usage example: Full-text search keyword matching, accomplished through MATCH_ANY and MATCH_ALL
SELECT * FROM table_name WHERE column_name MATCH_ANY | MATCH_ALL 'keyword1 ...';
```


**Recommended conventions**


1. If a certain range of data is difficult to design using partitioning, bucketing, or prefix indexing, consider introducing an inverted index to accelerate queries.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger"><strong>Mandatory constraints</strong></div>


<div data-tips="true" data-tips-type="danger">Inverted indexes have different Limits in different data models:</div>



1. <div data-tips="true" data-tips-type="danger">Aggregate KEY table model: Inverted indexes can only be created for Key columns.</div>


2. <div data-tips="true" data-tips-type="danger">Unique KEY table model: The merge on write feature must be enabled; after enabling, inverted indexes can be created for any column.</div>


3. <div data-tips="true" data-tips-type="danger">Duplicate KEY table model: Inverted indexes can be created for any column.</div>



<span id="0660489a"></span>
### BloomFilter index

Doris supports adding BloomFilter indexes to fields with high cardinality, which is suitable for equality queries on columns with high cardinality.

**Best practices**

```SQL
-- Creation example: Add "bloom_filter_columns"="k1,k2,k3" in the PROPERTIES section of the table creation statement
-- For example, we created BloomFilter indexes for saler_id and category_id.
CREATE TABLE IF NOT EXISTS sale_detail_bloom  (
    sale_date date NOT NULL COMMENT "销售时间",
    customer_id int NOT NULL COMMENT "客户编号",
    saler_id int NOT NULL COMMENT "销售员",
    sku_id int NOT NULL COMMENT "商品编号",
    category_id int NOT NULL COMMENT "商品分类",
    sale_count int NOT NULL COMMENT "销售数量",
    sale_price DECIMAL(12,2) NOT NULL COMMENT "单价",
    sale_amt DECIMAL(20,2)  COMMENT "销售总金额"
)
Duplicate  KEY(sale_date, customer_id,saler_id,sku_id,category_id)
DISTRIBUTED BY HASH(saler_id) BUCKETS 10
PROPERTIES (
"bloom_filter_columns"="saler_id,category_id"
);
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Mandatory constraints</div>



1. <div data-tips="true" data-tips-type="danger">BloomFilter indexes are not supported for columns of Tinyint, Float, or Double types.</div>


2. <div data-tips="true" data-tips-type="danger">BloomFilter indexes only accelerate filtering queries using in and = conditions.</div>


3. <div data-tips="true" data-tips-type="danger">BloomFilter indexes must be built on columns with in or = query conditions and high cardinality (above 5000).</div>


   1. <div data-tips="true" data-tips-type="danger">First, BloomFilter is suitable for non\-prefix filtering;</div>


   2. <div data-tips="true" data-tips-type="danger">Queries frequently filter based on this column, and most query conditions use in and = filtering;</div>


   3. <div data-tips="true" data-tips-type="danger">Unlike Bitmap, BloomFilter is suitable for high cardinality columns. For example, UserID. Because if the index is created on a column with low cardinality, such as the "gender" column, each Block will almost always contain all possible values, causing the BloomFilter index to lose its effectiveness;</div>


   4. <div data-tips="true" data-tips-type="danger">About half of the possible values are present in the data;</div>


   5. <div data-tips="true" data-tips-type="danger">For columns like ID number, which have particularly high cardinality and are queried using equality (=) queries, using a BloomFilter index can greatly accelerate <strong>.</strong></div>



<span id="97b60885"></span>
### NGram BloomFilter index

Starting from version 2.0.0, Doris added the NGram BloomFilter index to improve LIKE query performance.

**Best practices**

```SQL
-- Example of creation: Specify during table creation
CREATE TABLE `nb_table` (
  `siteid` int(11) NULL DEFAULT "10" COMMENT "",
  `citycode` smallint(6) NULL COMMENT "",
  `username` varchar(32) NULL DEFAULT "" COMMENT "",
  INDEX idx_ngrambf (`username`) USING NGRAM_BF PROPERTIES("gram_size"="3", "bf_size"="256") COMMENT 'username ngram_bf index'
) ENGINE=OLAP
AGGREGATE KEY(`siteid`, `citycode`, `username`) COMMENT "OLAP"
DISTRIBUTED BY HASH(`siteid`) BUCKETS 10;

-- PROPERTIES("gram_size"="3", "bf_size"="256"), which represent the number of grams and the number of bytes for the bloom filter, respectively.
-- The number of grams depends on the actual query scenario and is usually set to the length of most query strings. The bloom filter byte size can be determined through testing; generally, the larger the size, the better the filtering effect. You can start testing with 256 bytes to see the results. Of course, increasing the byte size will also raise the storage and memory cost of the index.
-- If the data cardinality is relatively high, the byte size does not need to be set too large. If the cardinality is not very high, you can improve the filtering effect by increasing the byte size.
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Mandatory specification</div>



1. <div data-tips="true" data-tips-type="danger">NGram BloomFilter only supports string columns</div>


2. <div data-tips="true" data-tips-type="danger">NGram BloomFilter index and BloomFilter index are mutually exclusive, meaning only one of them can be set for the same column</div>


3. <div data-tips="true" data-tips-type="danger">The NGram size and BloomFilter byte size can be tuned according to actual needs. If the NGram size is relatively small, you can appropriately increase the BloomFilter size.</div>


4. <div data-tips="true" data-tips-type="danger">For data at the hundred\-million level or above, if fuzzy matching is required, use an inverted index or NGram BloomFilter</div>



<span id="f1a0386c"></span>
### Bitmap index

To accelerate data queries, Doris supports adding Bitmap indexes to certain fields, which is suitable for equality or range queries on columns with low cardinality.

**Best practices**

```SQL
-- Example of creation: Create a Bitmap index for siteid on bitmap_table
CREATE INDEX [IF NOT EXISTS] bitmap_index_name ON
bitmap_table (siteid)
USING BITMAP COMMENT 'bitmap_siteid';
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Mandatory specification</div>



1. <div data-tips="true" data-tips-type="danger">Bitmap indexes are only created on single columns.</div>


2. <div data-tips="true" data-tips-type="danger">Bitmap indexes can be applied to all columns in the <code>Duplicate</code>, <code>Uniq</code> data models and to key columns in the <code>Aggregate</code> model.</div>


3. <div data-tips="true" data-tips-type="danger">The data types supported by Bitmap indexes are as follows:</div>


   * <div data-tips="true" data-tips-type="danger"><code>TINYINT</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>SMALLINT</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>INT</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>BIGINT</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>CHAR</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>VARCHAR</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>DATE</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>DATETIME</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>LARGEINT</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>DECIMAL</code></div>


   * <div data-tips="true" data-tips-type="danger"><code>BOOL</code></div>


4. <div data-tips="true" data-tips-type="danger">Bitmap indexes are only effective under Segment V2. When an index is created, the table's storage format will be automatically converted to V2 format by default.</div>


5. <div data-tips="true" data-tips-type="danger">Bitmap indexes must be built within a certain cardinality range; too high or too low cardinality is not suitable.</div>


   1. <div data-tips="true" data-tips-type="danger">They are suitable for columns with low cardinality, recommended between 100 and 100,000, such as occupation, city, and so on. If the duplication rate is too high, Bitmap indexes do not offer a significant advantage over other types of indexes; if the duplication rate is too low, space efficiency and performance will be greatly reduced. Specific types of queries, such as COUNT, OR, AND, and other logical operations, only require bitwise operations.</div>


   2. <div data-tips="true" data-tips-type="danger">This index is more suitable for orthogonal queries\*\*.\*\*</div>



<span id="da419208"></span>
## Field types

Doris supports multiple field types, such as precise deduplication BITMAP, approximate deduplication HLL, semi\-structured ARRAY/MAP/JSON, as well as common numeric, string, and time types.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Recommended conventions</div>



1. <div data-tips="true" data-tips-type="tip">VARCHAR</div>


   1. <div data-tips="true" data-tips-type="tip">Variable\-length string, with a length range of 1–65533 bytes. Stored using UTF\-8 encoding, so typically English characters occupy 1 byte, and Chinese characters occupy 3 bytes.</div>


   2. <div data-tips="true" data-tips-type="tip">There is a common misconception regarding the performance of varchar(255) and varchar(65533). If the stored data is the same, the performance is also the same. When creating a table and the maximum length of this field is uncertain, it is recommended to use 65533 directly to prevent import issues caused by excessively long strings.</div>


2. <div data-tips="true" data-tips-type="tip">STRING</div>


   1. <div data-tips="true" data-tips-type="tip">Variable\-length string, supports 1,048,576 bytes (1MB) by default and can be increased up to 2,147,483,643 bytes (2GB). Stored using UTF\-8 encoding, so typically English characters occupy 1 byte, and Chinese characters occupy 3 bytes.</div>


   2. <div data-tips="true" data-tips-type="tip">Can only be used in Value columns, not in Key columns or partition/bucket columns.</div>


   3. <div data-tips="true" data-tips-type="tip">Suitable for storing relatively large text. Generally, if there is no such requirement, it is recommended to use VARCHAR. STRING columns cannot be used in Key columns or bucket columns, which is a significant limitation.</div>


3. <div data-tips="true" data-tips-type="tip">Numeric fields: Select the corresponding data type according to the required precision; there are no particularly special cautions.</div>


4. <div data-tips="true" data-tips-type="tip">Caution: If high precision (millisecond timestamp) is required, specify the use of datetime(6); otherwise, millisecond timestamps are not supported by default.</div>


5. <div data-tips="true" data-tips-type="tip">It is recommended to use the JSON data type instead of string types for storing JSON data.</div>



<span id="5af46f45"></span>
## Table creation

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50974cdb629640ecb9d9ec9145c8b3b5~tplv-goo7wpa0wc-image.image) </span>

When creating a table, pay attention not only to the selection of the table model, index, and field types, but also to the configuration of partitioning and bucketing.

**Best practices**

```SQL
-- Taking the Merge-on-Write table of the Unique model as an example
-- The Merge-on-Write implementation of the Unique model is completely different from the aggregation model; query performance is closer to the duplicate model,
-- In scenarios requiring primary key constraints, it offers significant query performance advantages over the aggregation model, especially in aggregation queries and queries that need to filter large amounts of data using indexes.

-- Non-partitioned table
CREATE TABLE IF NOT EXISTS tbl_unique_merge_on_write
(
    `user_id` LARGEINT NOT NULL COMMENT "用户id",
    `username` VARCHAR(50) NOT NULL COMMENT "用户昵称",
    `register_time` DATE COMMENT "用户注册时间",
    `city` VARCHAR(20) COMMENT "用户所在城市",
    `age` SMALLINT COMMENT "用户年龄",
    `sex` TINYINT COMMENT "用户性别",
    `phone` LARGEINT COMMENT "用户电话",
    `address` VARCHAR(500) COMMENT "用户地址"
)
UNIQUE KEY(`user_id`, `username`)
-- Data volume of 3–5GB
DISTRIBUTED BY HASH(`user_id`) BUCKETS 10 
PROPERTIES (
-- In version 1.2.0, as a new feature, Merge-on-Write is disabled by default. Users can enable it by adding the following property
"enable_unique_key_merge_on_write" = "true" 
);

-- Partitioned table
CREATE TABLE IF NOT EXISTS tbl_unique_merge_on_write_p
(
    `user_id` LARGEINT NOT NULL COMMENT "用户id",
    `username` VARCHAR(50) NOT NULL COMMENT "用户昵称",
    `register_time` DATE COMMENT "用户注册时间",
    `city` VARCHAR(20) COMMENT "用户所在城市",
    `age` SMALLINT COMMENT "用户年龄",
    `sex` TINYINT COMMENT "用户性别",
    `phone` LARGEINT COMMENT "用户电话",
    `address` VARCHAR(500) COMMENT "用户地址"
)
UNIQUE KEY(`user_id`, `username`, `register_time`)
PARTITION BY RANGE(`register_time`) (
    PARTITION p00010101_1899 VALUES [('0001-01-01'), ('1900-01-01')), 
    PARTITION p19000101 VALUES [('1900-01-01'), ('1900-01-02')), 
    PARTITION p19000102 VALUES [('1900-01-02'), ('1900-01-03')),
    PARTITION p19000103 VALUES [('1900-01-03'), ('1900-01-04')),
    PARTITION p19000104_1999 VALUES [('1900-01-04'), ('2000-01-01')),
    FROM ("2000-01-01") TO ("2022-01-01") INTERVAL 1 YEAR, 
    PARTITION p30001231 VALUES [('3000-12-31'), ('3001-01-01')), 
    PARTITION p99991231 VALUES [('9999-12-31'), (MAXVALUE)) 
) 
-- Default data volume of 3-5G
DISTRIBUTED BY HASH(`user_id`) BUCKETS 10 
PROPERTIES ( 
-- In version 1.2.0, as a new feature, write-time compaction is disabled by default. Users can enable it by adding the following property.
"enable_unique_key_merge_on_write" = "true", 
-- Unit for dynamic partition scheduling. Can be specified as HOUR, DAY, WEEK, MONTH, or YEAR. These correspond to creating or deleting partitions by hour, day, week, month, or year, respectively.
"dynamic_partition.time_unit" = "MONTH",
-- Start offset for dynamic partitions, must be a negative number. Depending on the time_unit property, with the current day (week/month) as the reference, partitions before this offset will be deleted (TTL). If not specified, the default is -2147483648, meaning historical partitions will not be deleted.
"dynamic_partition.start" = "-3000",
-- End offset for dynamic partitions, must be a positive number. Depending on the time_unit property, with the current day (week/month) as the reference, partitions within this offset will be created in advance.
"dynamic_partition.end" = "10",
-- Prefix for dynamically created partition names (required).
"dynamic_partition.prefix" = "p",
-- Number of buckets for dynamically created partitions.
"dynamic_partition.buckets" = "10", 
"dynamic_partition.enable" = "true", 
-- Number of replicas for dynamically created partitions. If not specified, the default is 3, as set when the table was created.
"dynamic_partition.replication_num" = "3",
"replication_num" = "3"
);  

-- Partition creation view
-- The actual number of partitions created is determined by dynamic_partition.start, end, and the PARTITION BY RANGE settings.
show partitions from tbl_unique_merge_on_write_p;
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Mandatory specifications</div>



1. <div data-tips="true" data-tips-type="danger">The database character set must be set to UTF\-8, and only UTF\-8 is supported.</div>


2. <div data-tips="true" data-tips-type="danger">The number of replicas for a table must be 3 (if not specified, the default is 3).</div>


3. <div data-tips="true" data-tips-type="danger">The data volume for a single Tablet (number of Tablets = number of partitions × number of buckets × number of replicas) is theoretically unbounded. Except for small tables (hundreds of megabytes for dimension tables), ensure it is within the range of 1G to 10G:</div>


   1. <div data-tips="true" data-tips-type="danger">If the data volume for a single Tablet is too small, data aggregation is less effective and metadata management pressure increases.</div>


   2. <div data-tips="true" data-tips-type="danger">If the data volume is too large, it is not conducive to replica migration or restoration, and increases the cost of retrying failed Schema Change or materialization operations (the retry granularity for these operations is Tablet).</div>


4. <div data-tips="true" data-tips-type="danger">For data volumes exceeding 500 million, a partition and bucket strategy must be configured:</div>


   1. <div data-tips="true" data-tips-type="danger">Recommended bucket settings:</div>


   <div data-tips="true" data-tips-type="danger">   ```Plain
   i. 大表的单个 Tablet 存储数据大小在 1G-10G 区间，可防止过多的小文件产生。
   
   ii. 百兆左右的维表 Tablet 数量控制在 3-5 个，保证一定的并发数也不会产生过多的小文件。
   ```
      </div>
   

   2. <div data-tips="true" data-tips-type="danger">If partitioning is not possible and the data is growing rapidly, and dynamic partitioning by time cannot be performed, you can appropriately increase your Bucket count. Estimate your Bucket count based on the total data volume over your data Save period (180 days). It is recommended that the size of a single Bucket remains between 1 GB and 10 GB.</div>


   3. <div data-tips="true" data-tips-type="danger">Apply salting to the bucketing field, and use the same salting strategy when querying in business operations. This enables the use of bucket data pruning capabilities.</div>


   4. <div data-tips="true" data-tips-type="danger">Random bucketing of data:</div>


   <div data-tips="true" data-tips-type="danger">   ```Plain
   i. 如果 OLAP 表没有更新类型的字段，将表的数据分桶模式设置为 RANDOM，则可以避免严重的数据倾斜 (数据在导入表对应的分区的时候，单次导入作业每个 Batch 的数据将随机选择一个 Tablet 进行写入)。
   
   ii. 当表的分桶模式被设置为 RANDOM 时，因为没有分桶列，无法根据分桶列的值仅对几个分桶查询，对表进行查询的时候将对命中分区的全部分桶同时扫描，该设置适合对表数据整体的聚合查询分析而不适合高并发的点查询。
   
   iii. 如果 OLAP 表的是 Random Distribution 的数据分布，那么在数据导入的时候可以设置单分片导入模式（将 `load_to_single_tablet` 设置为 true），那么在大数据量的导入的时候，一个任务在将数据写入对应的分区时将只写入一个分片，这样将能提高数据导入的并发度和吞吐量，减少数据导入和 Compaction 导致的写放大问题，保障集群的稳定性。
   ```
      </div>
   

   5. <div data-tips="true" data-tips-type="danger">Dimension tables: For tables with slow growth, you can use a single partition and apply bucketing based on commonly used query conditions (where the data distribution of this field is relatively balanced).</div>


   6. <div data-tips="true" data-tips-type="danger">Fact tables.</div>


5. <div data-tips="true" data-tips-type="danger">For cases with a large number of historical partitions but little historical data, or where the data is unbalanced or infrequently queried, use the following method to place the data in special partitions.</div>


   <div data-tips="true" data-tips-type="danger">For historical data, if the data volume is small, you can create historical partitions (such as yearly or monthly partitions) and place all historical data into the corresponding partitions. For example, to create historical partitions: <code>FROM ("2000-01-01") TO ("2022-01-01") INTERVAL 1 YEAR</code>. For details, refer to:   </div>
   

   <div data-tips="true" data-tips-type="danger">   ```SQL
   ( 
       PARTITION p00010101_1899 VALUES [('0001-01-01'), ('1900-01-01')), 
       
       PARTITION p19000101 VALUES [('1900-01-01'), ('1900-01-02')), 
       
       ... 
       
       PARTITION p19000104_1999 VALUES [('1900-01-04'), ('2000-01-01')),
       
       FROM ("2000-01-01") TO ("2022-01-01") INTERVAL 1 YEAR, 
       
       PARTITION p30001231 VALUES [('3000-12-31'), ('3001-01-01')), 
       
       PARTITION p99991231 VALUES [('9999-12-31'), (MAXVALUE)) 
       
    )
   ```
      </div>
   

6. <div data-tips="true" data-tips-type="danger">A single table cannot have more than 6 materialized views.</div>


   1. <div data-tips="true" data-tips-type="danger">Materialized views on a single table are built in real time.</div>


   2. <div data-tips="true" data-tips-type="danger">On the Unique model, materialized views can only be used for key reordering and cannot perform data aggregation, because the aggregation model of the Unique model is Replace.</div>
