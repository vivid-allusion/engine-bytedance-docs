---
title: "Paimon Partial Update"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Paimon_Partial_Update"
---

<span id="284eb7c8"></span>
## 1. Overview

Partial Update mainly refers to directly updating certain field values in a table, rather than all field values. Updates can be made using an Update statement, typically by reading the entire row of data first, then updating some field values, and finally writing back. This approach is extremely inefficient in large\-scale real\-time data lake scenarios.

Flink Paimon's **Partial Update** is a table engine feature for streaming data processing, designed to concurrently update partial columns of the same table through multiple streams, ultimately achieving complete data updates. This article provides a detailed introduction to this feature, its characteristics, and applicable scenarios:

The functionalities of Partial Update include the following aspects:


1. **Partial Update**: Partial Update allows multiple Flink stream tasks to concurrently update different columns of the same table, eventually merging these partial updates into a complete row of data. For example, Stream A updates Columns A and B, Stream B updates Columns C and D, eventually resulting in a row containing all columns.

2. **Concurrent multi\-stream writing**: Multiple Flink streaming tasks can be merged into one job via UNION ALL to write into the same Paimon table, avoiding the compaction task split issues caused by concurrent writing from multiple jobs.

3. **No need for full join**: The traditional wide table construction often requires dual\-stream or multi\-stream joins, while Partial Update avoids join operations, reducing state pressure on Flink tasks and simplifying task maintenance.

4. **Support for Changelog subscription**: Compatible with Lookup or Full\-Compaction Changelog Producers, enabling access to complete data change logs.

5. **Support for Sequence Groups**: Through the sequence group mechanism, Partial Update can address the disorder issues during multi\-stream updates. Each stream can define its own sequence group, ensuring that only updates meeting the criteria are effective.


<span id="dffc3364"></span>
## 2. Applicable Scenarios

Here are common scenarios for partial column updates:


1. **Multi\-stream real\-time dynamic updates**: Suitable for scenarios requiring frequent updates of certain fields, such as user behavior information updates in user tag tables, supporting real\-time analysis and decision\-making in advertising or recommendation systems.

2. **Large wide table assembly**: When merging data from multiple source tables into a single large wide table, partial column updates can be utilized to avoid performance overhead caused by full join operations. For example, e\-commerce platforms may need to merge data from order tables, payment tables, merchandise tables, and others into a wide table for downstream analysis.

3. **Data Correction**: Suitable for scenarios requiring data amendments, where partial updates can accurately target and update specific fields, effectively reducing update overhead.

4. **High\-frequency Concurrent Writing**: Supports high\-frequency concurrent writing, suitable for scenarios that require real\-time updates of a large number of rows but only involve a few columns, such as real\-time log processing or monitoring data updates.

5. **Performance Optimization**: When updating a few columns, partial updates can significantly enhance performance, especially in cases involving a large number of rows, reducing unnecessary computation and storage overhead.


<span id="491f7568"></span>
## 3. Usage example

Before using, note the Flink version requirement:


* Flink version must be \>= 1.16, with specific functionalities supported as follows:

   * Flink 1.16 includes Paimon version 0.6, which does not support `collect`, `merge_map` and other aggregation functions. If needed, it is recommended to upload a higher version of the Paimon community Connector.

   * Flink 1.17 is recommended for use. Built\-in Paimon 0.8.2 byte\-enhanced version functions, also supports syntax such as stored procedures.


<span id="9150e20f"></span>
### 3.1 Business Description

The following is an example of using Partial Update, such as having common dimension table logic for building user master data. There are three tables related to user information upstream:


1. User Basic Information: Username, basic details, etc., after user registration, which are the main data of the user table.

2. User Channel Information: The channels through which users log in, such as github/google account/phone... etc., a user may bind multiple channels to log in.

3. User Membership Information: After a user registers for membership, there may be a membership information table; a user may have one or zero membership information.


When we are doing business layering, we may need to build master data centered around the user, including various dimensions of user information, to support subsequent processing of downstream flow and batch tasks.

At this point, the structure of the three upstream tables, simplified as follows (using simulated data sources, which might actually be Kafka, MySQL\-CDC, Paimon, and other various data upstreams):

```SQL
-- Basic user information
CREATE TABLE `paimon_pu`.`paimon_pu`.`user_info` (
    uid INT,
    username STRING, -- Username
    reg_time TIMESTAMP(3), -- Registration time
    PRIMARY KEY (uid) NOT ENFORCED
);

-- User login channels
CREATE TABLE `paimon_pu`.`paimon_pu`.`user_logintype` (
    uid INT,
    logintype STRING, -- Login channel type, e.g., github/google ...
    bind_time TIMESTAMP(3),
    PRIMARY KEY (uid, logintype) NOT ENFORCED
);

-- User VIP membership information
CREATE TABLE `paimon_pu`.`paimon_pu`.`user_vip_info` (
    uid INT,
    is_valid BOOLEAN, -- Whether the VIP membership is valid
    start_time TIMESTAMP(3), -- VIP membership start time
    end_time TIMESTAMP(3), -- VIP membership end time
    PRIMARY KEY (uid) NOT ENFORCED
);
```


Test scripts as follows can be used to insert test data:

```SQL
-- Insert basic user information
INSERT INTO `paimon_pu`.`paimon_pu`.`user_info` VALUES 
(1001, 'Alice', TIMESTAMP '2023-01-15 10:30:00'),
(1002, 'Bob', TIMESTAMP '2023-03-22 14:20:00'),
(1003, 'Charlie', TIMESTAMP '2023-05-18 09:15:00'),
(1004, 'David', TIMESTAMP '2023-07-01 16:45:00'),
(1005, 'Emma', TIMESTAMP '2023-09-30 11:25:00');

-- Insert user login channel data (a user may have multiple login channels)
INSERT INTO `paimon_pu`.`paimon_pu`.`user_logintype` VALUES 
(1001, 'github', TIMESTAMP '2023-01-15 10:35:00'),
(1001, 'google', TIMESTAMP '2023-01-16 15:20:00'),
(1002, 'wechat', TIMESTAMP '2023-03-22 14:25:00'),
(1003, 'github', TIMESTAMP '2023-05-18 09:20:00'),
(1003, 'google', TIMESTAMP '2023-05-19 10:30:00'),
(1004, 'wechat', TIMESTAMP '2023-07-01 16:50:00'),
(1005, 'github', TIMESTAMP '2023-09-30 11:30:00');

-- Insert user VIP membership information
INSERT INTO `paimon_pu`.`paimon_pu`.`user_vip_info` VALUES 
(1001, true, TIMESTAMP '2023-02-01 00:00:00', TIMESTAMP '2023-12-31 23:59:59'),
(1002, true, TIMESTAMP '2023-04-01 00:00:00', TIMESTAMP '2023-10-31 23:59:59'),
(1003, true, TIMESTAMP '2023-06-01 00:00:00', TIMESTAMP '2024-05-31 23:59:59'),
(1005, true, TIMESTAMP '2023-10-01 00:00:00', TIMESTAMP '2024-09-30 23:59:59');
```


<span id="0090c0ec"></span>
### 3.2 Business Modeling

We model our business operations following the described approach:

```SQL
-- User wide table, serving as a common dimension table that includes all data from the three user-related tables
CREATE TABLE IF NOT EXISTS `paimon_pu`.`paimon_pu`.`ods_user_wide_info` (
    uid INT,
    -- Basic user information
    username STRING, -- Username
    reg_time TIMESTAMP(3), -- Registration time
    -- Login channel information, stored in a nested structure with de-duplication by channel name
    logintypes ARRAY<ROW<logintype STRING, bind_time TIMESTAMP(3)>>,
    last_bind_time TIMESTAMP(3), 
    -- VIP membership information
    vip_is_valid BOOLEAN, -- Whether the VIP membership is valid
    vip_start_time TIMESTAMP(3), -- VIP membership start time
    vip_end_time TIMESTAMP(3), -- VIP membership end time
    PRIMARY KEY (uid) NOT ENFORCED
) WITH (
    'merge-engine' = 'partial-update',
    -- For downstream stream reads, use either 'lookup' or 'full-compaction'
    'changelog-producer' = 'lookup', 
    'fields.last_bind_time.sequence-group' = 'logintypes',
    'fields.logintypes.aggregate-function' = 'nested_update',
    'fields.logintypes.nested-key' = 'logintype'
);
```


Key Design:


1. `merge-engine`: Uses `partial-update`

2. `sequence-group`: Uses `last_login_time` as the sequence group field, and if this timestamp version increases, it aggregates the `logintypes` field

3. `aggregate-function`: The aggregation function uses `nested_update` in sub\-fields, with `logintype` as the nested primary key, performing deduplication and updates


This allows for users who have linked multiple channels to place the user's linked channels as an array in the nested field `logintypes`.

<span id="fcef94d1"></span>
### 3.3 Partial Update

The following Flink SQL reads partial columns from three data sources, setting other unchanged data to NULL, ensuring that each data flow only updates part of the data, and finally combines the three streams with UNION ALL into one stream, written into the downstream Partial Update table:

```SQL
INSERT INTO `paimon_pu`.`paimon_pu`.`ods_user_wide_info`
SELECT
  uid, username, reg_time, logintypes, last_bind_time, vip_is_valid, vip_start_time, vip_end_time
FROM (
    SELECT 
      uid, 
      username,
      reg_time, 
      CAST (NULL AS ARRAY<ROW<logintype STRING, bind_time TIMESTAMP(3)>>) AS logintypes,
      CAST (NULL AS TIMESTAMP(3)) AS last_bind_time,
      CAST (NULL AS BOOLEAN) AS vip_is_valid,
      CAST (NULL AS TIMESTAMP(3)) AS vip_start_time,
      CAST (NULL AS TIMESTAMP(3)) AS vip_end_time
    FROM `user_info`
    
    UNION ALL 
    
    SELECT 
      uid, 
      CAST (NULL AS STRING) AS username,
      CAST (NULL AS TIMESTAMP(3)) AS reg_time,
      ARRAY[ROW(logintype, bind_time)] AS logintypes, 
      bind_time AS last_bind_time,
      CAST (NULL AS BOOLEAN) AS vip_is_valid,
      CAST (NULL AS TIMESTAMP(3)) AS vip_start_time,
      CAST (NULL AS TIMESTAMP(3)) AS vip_end_time
    FROM `user_logintype`
    
    UNION ALL 
      
    SELECT 
      uid, 
      CAST (NULL AS STRING) AS username,
      CAST (NULL AS TIMESTAMP(3)) AS reg_time,
      CAST (NULL AS ARRAY<ROW<logintype VARCHAR, bind_time TIMESTAMP(3)>>) AS logintypes,
      CAST (NULL AS TIMESTAMP(3)) AS last_bind_time,
      is_valid AS vip_is_valid,
      start_time AS vip_start_time,
      end_time AS vip_end_time
    FROM `user_vip_info`
);
```


<span id="fe1ce73b"></span>
### 3.4 Result Verification

You can explore and query data using SQL\-like queries, but note that such SQL queries cannot be directly executed in Flink SQL tasks for debugging. Instead, relevant Insert statements need to be written to the downstream data print for proper debugging.

```SQL
-- User wide table used as a print sink, containing data from the previous three tables as a common dimension table
CREATE TABLE IF NOT EXISTS `print_result` (
    uid INT,
    -- Basic user information
    username STRING, -- Username
    reg_time TIMESTAMP(3), -- Registration time
    -- Login channel information, flattening nested array of multiple login channels, de-duplicated by channel name
    logintype STRING,
    bind_time TIMESTAMP(3),
    -- VIP membership information
    vip_is_valid BOOLEAN, -- Whether the VIP membership is valid
    vip_start_time TIMESTAMP(3), -- VIP membership start time
    vip_end_time TIMESTAMP(3), -- VIP membership end time
    PRIMARY KEY (uid) NOT ENFORCED
) WITH (
    'connector' = 'print'
);

-- Use UNNEST to flatten the array
-- Note: This type of query cannot be executed directly in Flink SQL CLI; it must be used with an INSERT into a print sink
INSERT INTO `print_result` 
SELECT uid, username, reg_time, logintype, bind_time, vip_is_valid, vip_start_time, vip_end_time
FROM `paimon_pu`.`paimon_pu`.`ods_user_wide_info`, UNNEST(logintypes) AS lt(logintype, bind_time);
```


The query results show that the batch job was processed successfully.

<span id="d057bc30"></span>
## 4. Detailed Features

<span id="e05ae7e2"></span>
### 4.1 Feature Usage

By specifying `'merge-engine' = 'partial-update'`, users can gradually complete record column updates through multiple updates. This is achieved by updating the value fields one by one using the latest data under the same. However, null values are not overwritten during this process. For instance, assume Paimon receives three records:


* `<1, 23.0, 10, NULL>`

* `<1, NULL, NULL, 'This is a book'>`

* `<1, 25.2, NULL, NULL>`


Assuming the first column is the primary key, the final result will be `<1, 25.2, 10, 'This is a book'>`.

For stream queries, a `partial-update` merge engine must be used with either `lookup` or `full-compaction` (see [Changelog output mechanism](https://docs.byteplus.com/docs/flink/Connector_Paimon#79d03b88)). It is worth noting that `input` also supports generating Changelogs, but only returns input records and cannot return updated data.

Additionally, by default, partial updates cannot accept deletion records. You may consider one of the following solutions:


* Configure 'ignore\-delete' to ignore deleted records.

* Configure 'sequence\-group' to revoke parts of a column.


<span id="306bc449"></span>
### 4.2 Sequence Group

Sequence fields may not address the disorder issue of partial update tables with multiple stream updates as the sequence fields could be overwritten by the latest data from another stream during multiple updates. Therefore, we have introduced the sequence group mechanism for partial update tables. It can solve:


1. the disorder during multi\-stream updates. Each stream defines its own sequence group.

2. Real partial updates, not just non\-null updates, such as scenarios requiring null value coverage.


Please see the example:

```SQL
CREATE TABLE t (
    k INT,
    a INT,
    b INT,
    g_1 INT,
    c INT,
    d INT,
    g_2 INT,
    PRIMARY KEY (k) NOT ENFORCED
) WITH (
    'merge-engine' = 'partial-update',
    'fields.g_1.sequence-group' = 'a,b',
    'fields.g_2.sequence-group' = 'c,d'
);

-- Insert initial row
INSERT INTO t VALUES (1, 1, 1, 1, 1, 1, 1);

-- g_2 is NULL, so c and d should not be updated
INSERT INTO t VALUES (1, 2, 2, 2, 2, 2, CAST(NULL AS INT));

-- Expected output: 1, 2, 2, 2, 1, 1, 1

-- g_1 is not greater (equal to existing), so a and b should not be updated
INSERT INTO t VALUES (1, 3, 3, 1, 3, 3, 3);

-- Expected output: 1, 2, 2, 2, 3, 3, 3
```


For `fields.<field-name>.sequence-group`, valid comparison data types include: DECIMAL, TINYINT, SMALLINT, INTEGER, BIGINT, FLOAT, DOUBLE, DATE, TIME, TIMESTAMP, and TIMESTAMP_LTZ.

<span id="2552f0cf"></span>
### 4.3 Partial Update supports aggregation

You can specify aggregation functions for input fields, and all functions supported in [Paimon Aggregation Table](https://docs.byteplus.com/docs/flink/Paimon_Aggregation_Table) can be used. Please see the example:

```SQL
CREATE TABLE t (
    k INT,
    a INT,
    b INT,
    c INT,
    d INT,
    PRIMARY KEY (k) NOT ENFORCED
) WITH (
    'merge-engine' = 'partial-update',
    
    -- Group 'a' updates are sequenced by field 'b'
    'fields.a.sequence-group' = 'b',
    -- 'b' keeps the first non-null value it receives
    'fields.b.aggregate-function' = 'first_value',

    -- Group 'c' updates are sequenced by field 'd'
    'fields.c.sequence-group' = 'd',
    -- 'd' uses sum aggregation
    'fields.d.aggregate-function' = 'sum'
);

-- Input: (1,1,1,null,null) --> 'b' = 1, so 'a' = 1 (first insert)
INSERT INTO t VALUES (1, 1, 1, CAST(NULL AS INT), CAST(NULL AS INT));

-- Input: (1,null,null,1,1) --> 'd' = 1, so 'c' = 1, 'd' = 1
INSERT INTO t VALUES (1, CAST(NULL AS INT), CAST(NULL AS INT), 1, 1);

-- Input: (1,2,2,null,null) --> 'b' already has first_value = 1 → 'a' does not update
INSERT INTO t VALUES (1, 2, 2, CAST(NULL AS INT), CAST(NULL AS INT));

-- Input: (1,null,null,2,2) --> 'd' = 1 + 2 = 3, so 'c' = 2
INSERT INTO t VALUES (1, CAST(NULL AS INT), CAST(NULL AS INT), 2, 2);

-- Final expected result:
-- k | a | b | c | d
-- 1 | 2 | 1 | 2 | 3
```


Flink Paimon's Partial Update is an efficient multi\-stream concurrent update mechanism, suitable for scenarios such as wide table construction, real\-time data widening, and stream\-batch integration. Its core advantage lies in avoiding full join operations, reducing state pressure, and solving the disorder problems of updates from multiple streams through sequence grouping mechanisms. For business scenarios requiring efficient updates and expansion of data, trying the Partial Update feature is recommended. Additionally, please pay attention to the [Paimon official documentation](https://paimon.apache.org/docs/0.8/primary-key-table/merge-engine/).

<span id="05c48b90"></span>
## 5. Common Issues

<span id="c3bd4e22"></span>
### 5.1 Partial Update tables do not support stream reading

**Problem description**: Errors occur when streaming tasks consume from Partial Update tables upstream as follows, `java.lang.RuntimeException: Partial update streaming reading is not supported.` `You can use 'lookup' or 'full-compaction' changelog producer to support streaming reading.` `('input' changelog producer is also supported, but only returns input records.)`

**Solution**: Partial Update tables cannot stream read if no changelog is produced. It's recommended to subscribe to changelog using `lookup` or `full-compaction` modes. Additionally, if the `input` output mode is used, it is generally impossible to obtain the actual change log; in this case, what is obtained is the insertion of original content from upstream.
