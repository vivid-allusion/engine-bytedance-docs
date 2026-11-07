---
title: "Paimon Dimension Table Lookup"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Paimon_Dimension_Table_Lookup"
---

<span id="1b881bc5"></span>
## 1. Overview

<span id="3e7f062d"></span>
### 1.1 Dimension Table Queries

In Flink SQL tasks, real\-time dimension table expansion is a common streaming computing scenario, where real\-time data streams are correlated with external dimension tables in real\-time without the need for additional state management; it offers simple semantics and supports high QPS throughput. Common dimension table query scenarios include but are not limited to:


1. **User Behavior Analysis**: User behavior logs are associated with usernames, basic information, and historical actions.

2. **Real\-Time Recommendation Systems**: Users' real\-time actions are associated with feature data in the recommendation model to produce personalized results.

3. **Financial Risk Control**: Transaction data is associated with a risk control rule library, detecting and alerting on unusual transaction behaviors in real time.

4. **IoT Monitoring**: Device data is associated with device configurations or status information for real\-time monitoring and timely fault detection.


<span id="a8a524b0"></span>
### 1.2 The Advantage of Using Paimon as a Dimension Table

Widening dimension tables generally requires the introduction of high QPS point checks from remote storage (such as MySQL, HBase, Redis, etc.), which increases operational complexity. In certain business scenarios, dimension table data also needs to support downstream stream\-batch read\-write operations, possibly introducing additional channels such as Dump Hive, Dump MQ, further expanding its application scope and complexity. Paimon, as a storage system based on the LSM\-Tree, supports stream\-batch read\-write operations and can very well support scenarios for dimension table queries.

Using Paimon tables directly as dimension tables has the following advantages:


* **Good performance**: Based on the LSM\-Tree storage structure, it provides high data lookup efficiency.

* **Rich scenarios**: Supports stream\-batch read\-write, simplifying the maintenance chain of dimension tables.

* **Lower cost**: Does not require exclusive computing resources, directly builds multi\-level cache based on remote storage (HDFS, TOS), local files, and local memory to optimize read performance.


<span id="bca9a785"></span>
## 2. Basic example

The following examples primarily use Flink SQL development method, and due to the length of this article, specific operational steps are not discussed in detail here, but can be referred to [Paimon with Fileystem Catalog](https://docs.byteplus.com/docs/flink/Paimon_with_Fileystem_Catalog).

<span id="d22da4ac"></span>
### 2.1 Create dimension table

In the following SQL, we have constructed a dim_orders table as the dimension table for order information. The primary key and bucket key of the order table are both order_id, i.e., the order id. In the process of real\-time dimension table expansion tasks, we will associate based on the order id to obtain related order information.

```SQL
CREATE CATALOG paimon_dim
WITH
  (
    'type' = 'paimon',
    'warehouse' = 'tos://flink-cwz-paimon/paimon_dim'
  );
  
CREATE DATABASE IF NOT EXISTS paimon_dim.dim_test;

-- Create dimension table for order data
CREATE TABLE IF NOT EXISTS
  `paimon_dim`.`dim_test`.`dim_orders` (
    `order_id` INT,
    `order_name` STRING,
    `order_product_id` INT,
    `order_customer_id` INT,
    `order_status` STRING,
    `create_date` TIMESTAMP,
    `create_ts` INT,
    PRIMARY key (`order_id`) NOT ENFORCED
  )
WITH
  (
    'bucket' = '20',
    'bucket-key' = 'order_id',
    -- To control data volume, records older than 2 days based on creation date will expire
    'record-level.expire-time' = '2 d',
    'record-level.time-field' = 'create_ts'
  );
```


<span id="bafe74ba"></span>
### 2.2 Real\-time Update of Dimension Table

Once the dimension table is created, we can continuously update the data in the dimension table to represent the normal order change operations.

```SQL
CREATE CATALOG paimon_dim
WITH
  (
    'type' = 'paimon',
    'warehouse' = 'tos://flink-cwz-paimon/paimon_dim'
  );
  
CREATE DATABASE IF NOT EXISTS paimon_dim.dim_test;

-- Create dimension table
CREATE TABLE IF NOT EXISTS
  `paimon_dim`.`dim_test`.`dim_orders` (
    `order_id` INT,
    `order_name` STRING,
    `order_product_id` INT,
    `order_customer_id` INT,
    `order_status` STRING,
    `create_date` TIMESTAMP,
    `create_ts` INT,
    PRIMARY key (`order_id`) NOT ENFORCED
  )
WITH
  (
    'bucket' = '20',
    'bucket-key' = 'order_id',
    -- To control data volume, expire data older than 2 days based on creation date
    'record-level.expire-time' = '2 d',
    'record-level.time-field' = 'create_ts'
  );
```


<span id="8b821c54"></span>
### 2.3 Simulate Real\-time Data Stream

First, we use `datagen` to simulate a real\-time data stream. Note that here we use `create_date` as the processing time.

```SQL
-- Simulate data stream
CREATE TABLE
  datagen_source (
    `product_id` INT,
    `product_name` STRING,
    `product_category_id` INT,
    `product_order_id` INT,
    `product_status` STRING,
    `create_date` AS proctime ()
  )
WITH
  ('connector' = 'datagen');
  
-- Downstream wide table after real-time data enrichment, using print to output to console for testing
CREATE TABLE
  print_sink (
    `product_id` INT,
    `product_name` STRING,
    `product_category_id` INT,
    `product_order_id` INT,
    `product_status` STRING,
    `create_date` TIMESTAMP,
    `order_name` STRING,
    `orders_customer_id` INT,
    `order_status` STRING
  )
WITH
  ('connector' = 'print');
```


<span id="6ee7ea30"></span>
### 2.4 Real\-time lookup join

The following SQL statement defines a real\-time expanded view `trade_orde_view`, by associating the streaming data source `datagen_source` with the Paimon dimension table `dim_orders` to achieve real\-time data expansion.

```SQL
-- Filter and write downstream data with non-null order_name after real-time enrichment
INSERT INTO
  print_sink
SELECT
  gen.product_id, gen.product_name, gen.product_category_id,
  gen.product_order_id, gen.product_status, gen.create_date,
  orders.order_name, orders.order_customer_id, order_status
FROM
  datagen_source AS gen
  JOIN `paimon_dim`.`dim_test`.`dim_orders`
  FOR SYSTEM_TIME AS OF gen.create_date AS orders
  ON gen.product_order_id = orders.order_id
WHERE
  orders.order_name IS NOT NULL;
```


The specific logic for linking dimension tables is explained as follows:


* **Dimension table**: `paimon_dim.dim_test.dim_orders` is the Paimon dimension table defined in the above text.

* Time semantics: FOR SYSTEM_TIME AS OF gen.create_date indicates looking up the snapshot data of the dimension table at the moment of create_date based on the create_date field in the stream data.

* **Join condition**: `gen.product_order_id = orders.order_id` means associating the `product_order_id` in stream data with the `order_id` in the dimension table.


<span id="6d54f491"></span>
## Optimization Tips

<span id="82efad20"></span>
### 3.1 Lookup Retry with Delay

If a record from the `datagen_source` table (main table) cannot complete the Join operation due to the corresponding data in the `orders` table (dimension table) not being ready, consider using Flink's [Lookup Retry with Delay Strategy](https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/table/sql/queries/hints/#3-enable-delayed-retry-strategy-for-lookup). This feature is only applicable to Flink\-1.16\-byted and higher versions.

```SQL
-- Use hint for Lookup retry
SELECT /*+ LOOKUP('table'='orders', 'retry-predicate'='lookup_miss', 'retry-strategy'='fixed_delay', 'fixed-delay'='1s', 'max-attempts'='600') */
  gen.product_id, gen.product_name, gen.product_category_id,
  gen.product_order_id, gen.product_status, gen.create_date,
  orders.order_name, orders.order_customer_id, order_status
FROM
  datagen_source AS gen
  JOIN `paimon_dim`.`dim_test`.`dim_orders`
  FOR SYSTEM_TIME AS OF gen.create_date AS orders
  ON gen.product_order_id = orders.order_id;
```


<span id="44499e26"></span>
### 3.2 Asynchronous Lookup Delayed Retry

The issue with synchronous retry is that one record blocks subsequent records, causing the entire job to be stalled. You might consider using asynchronous (async) + allow_unordered to avoid blocking; this way, records missing from the Join will no longer block other records.

```SQL
-- Use hint for Lookup retry
SELECT /*+ LOOKUP('table'='orders', 'retry-predicate'='lookup_miss', 'output-mode'='allow_unordered', 'retry-strategy'='fixed_delay', 'fixed-delay'='1s', 'max-attempts'='600') */
  gen.product_id, gen.product_name, gen.product_category_id,
  gen.product_order_id, gen.product_status, gen.create_date,
  orders.order_name, orders.order_customer_id, order_status
FROM
  datagen_source AS gen
  JOIN `paimon_dim`.`dim_test`.`dim_orders` /*+ OPTIONS('lookup.async'='true', 'lookup.async-thread-number'='16') */
  FOR SYSTEM_TIME AS OF gen.create_date AS orders
  ON gen.product_order_id = orders.order_id;
```


<span id="312deb98"></span>
### 3.3 Dynamic Partitioning

In traditional data warehouses, each partition typically maintains the latest complete data, hence these partition tables only need to be linked to the latest partitions. Paimon specifically developed the `max_pt` feature for this scenario.

```SQL
-- If the orders table is a full partition with daily snapshots
CREATE TABLE IF NOT EXISTS
  `paimon_dim`.`dim_test`.`dim_orders` (
    `order_id` INT,
    `order_name` STRING,
    `order_product_id` INT,
    `order_customer_id` INT,
    `order_status` STRING,
    `create_date` TIMESTAMP,
    `create_ts` INT,
    `dt` STRING,
    PRIMARY key (`order_id`, `dt`) NOT ENFORCED
  ) PARTITIONED BY (dt);
```


In this case, use `max_pt` to select the most recent partition for dimension table joining.

```SQL
-- Use hint to select the latest partition
SELECT 
  gen.product_id, gen.product_name, gen.product_category_id,
  gen.product_order_id, gen.product_status, gen.create_date,
  orders.order_name, orders.order_customer_id, order_status
FROM
  datagen_source AS gen
  JOIN `paimon_dim`.`dim_test`.`dim_orders` 
  /*+ OPTIONS('lookup.dynamic-partition'='max_pt()', 'lookup.dynamic-partition.refresh-interval'='1 h') */
  -- Use dynamic partition lookup to select the latest partition and refresh every 1 hour
  FOR SYSTEM_TIME AS OF gen.create_date AS orders 
  ON gen.product_order_id = orders.order_id;
```


<span id="db9dab05"></span>
### 3.5 Caching Strategies

In different Look Join scenarios, there are partial caching and full caching strategies, offering developers better performance tuning options.

<span id="bee82445"></span>
#### 3.5.1 Partial Caching

Partial caching mode caches the data files that are hit on\-demand during the Join process, as illustrated:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1648db0627454ba6ad9eaf4f07df351f~tplv-goo7wpa0wc-image.image) </span>

Enable it through the WITH parameter `'lookup.cache'='auto'` in the table creation statement, when fulfilling the following two conditions:


* The associated table is a primary key table with a fixed bucket mode.

* The primary key of the associated table aligns with the Join Key.


At this point, the Partial Cache mode is automatically selected. If these two conditions are not met, Full Cache mode will be chosen.

Partial cache can utilize the ordered nature of primary keys in the LSM\-Tree, enabling on\-demand loading of cached dimension table data, avoiding full data loading and quicker task initialization.

> Note: Only primary key table's primary key association scenarios are supported; if the associated Key is not a primary key, it cannot be used.


<span id="10ca2d56"></span>
#### 3.5.1 Full Cache

Full cache will batch load all data from the Paimon table into RocksDB, enabling successful Lookup even when the associated Key is not a primary key:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7435428e340a44d8b094cf79f524b4f5~tplv-goo7wpa0wc-image.image) </span>

To activate, use parameter `'lookup.cache'='full'`

Full Cache mode supports both primary key and non\-primary key associations for primary key tables, as well as associations for non\-primary key tables. The downside, however, is longer initial load times and noticeable cold start phenomena.

<span id="3f1acf10"></span>
### 3.6 Bucket Shuffle

Paimon version of the BytePlus Engine has provided the community with the Bucket Shuffle feature, significantly enhancing the performance of Lookup Join on large\-scale dimensional tables. The principle of Bucket Shuffle is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d1687cf4ff9496eb17b82f116003d94~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a5dd2f7cacb4103a05323570cac320b~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
Bucket Shuffle feature not enabled</div>


<div style="text-align: center">
Bucket Shuffle feature enabled</div>


It can be seen that during the Lookup Join process using Bucket Shuffle, main data undergoes Hash grouping based on the Join Key, which allows caching of corresponding Bucket data in each group, significantly reducing memory usage and decreasing the chance of cache eviction. It supports larger\-scale dimensional tables. Method to enable is as follows, set in hint: `'shuffle' = 'true'`:

```SQL
-- 使用 hint 选择最新分区
SELECT /*+ LOOKUP('table'='orders', 'shuffle'='true') */ 
  gen.product_id, gen.product_name, gen.product_category_id,
  gen.product_order_id, gen.product_status, gen.create_date,
  orders.order_name, orders.order_customer_id, order_status
FROM
  datagen_source AS gen
  JOIN `paimon_dim`.`dim_test`.`dim_orders` 
  FOR SYSTEM_TIME AS OF gen.create_date AS orders 
  ON gen.product_order_id = orders.order_id;
```


Applicable scenarios:


* Fixed bucket tables: both Primary Key tables and Append tables (non\-Primary Key tables) are supported

* Join Key must include all the Bucket Keys


<span id="c52daa9f"></span>
## Parameter Details

Here are the common settings for WITH parameters when creating dimension tables:


|**Parameter** |**Description** |**Data Type** |**Required** |**Default Value** |**Remarks** |
|---|---|---|---|---|---|
|lookup.cache\-max\-memory\-size |Paimon dimension table memory cache size. |String |No |256 MB |This parameter value affects both the dimension table cache size and the cache size of lookup changelog\-producer; both mechanisms' cache sizes are configured by this parameter. |
|lookup.cache |Paimon Dimension Table Cache Mode |Enum |No |AUTO |The parameters support AUTO and FULL enumeration values, and will give priority to the Partial Cache mode when conditions are met |
|lookup.continuous.discovery\-interval |Dimension table data refresh interval |Duration |No |10s |Specify the refresh interval for incremental data in the dimension table |
|lookup.cache\-max\-disk\-size |Maximum space usage for local cache of the dimension table |MemorySize |No |Unlimited |Set the maximum local disk space usage for specified dimension tables and Lookup Compaction, currently applicable only to Partial Cache scenarios |
|lookup.local\-file\-type |Dimension table file type |Enum |No |HASH |Only for Partial Cache scenarios, supports two modes: HASH and SORT. Sort mode initializes faster |
