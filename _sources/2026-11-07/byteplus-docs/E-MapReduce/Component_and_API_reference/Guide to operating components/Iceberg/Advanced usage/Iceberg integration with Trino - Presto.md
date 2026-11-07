---
title: "Iceberg integration with Trino/Presto"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Iceberg_integration_with_Trino_or_Presto"
---

Operations on Iceberg tables can be performed in Trino or Presto. Volcano Engine E\-MapReduce (EMR) is configured by default with connectors for Trino (or Presto) and Iceberg. This document describes how to operate Iceberg tables in Trino; the same method can be used to operate them in Presto.

<span id="_1-前提条件"></span>
## 1 Prerequisites


1. Applicable to EMR version 1.2.0 and later (including version 1.2.0).

2. An EMR cluster has been created, and the Iceberg and Trino components are installed. There are two ways to install the Iceberg and Trino components:

   1. When creating an EMR cluster, select Iceberg and Trino as optional components. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

   2. For an existing EMR cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg and Trino services.


<span id="_2-操作步骤"></span>
## 2 Procedure

<span id="_2-1-打开-trino-客户端并使用-iceberg-连接器获取metastore"></span>
### 2.1 Open the Trino client and use the Iceberg connector to access the Metastore

Refer to [Basic usage](https://docs.byteplus.com/docs/undefined/69aa3921f1381a04fe1b4573), and add the Iceberg connection information after the Trino CLI command.

```Plain
--catalog iceberg --schema default
```


The parameter descriptions are as follows:


|Parameters |Note |
|---|---|
|catalog iceberg: |iceberg is the catalog name used for Iceberg |
|schema default |default is the schema name used for Iceberg |


<span id="_2-2-基本操作"></span>
### 2.2 Basic operations

For details, refer to the [Trino official website](https://trino.io/docs/current/connector/iceberg.html) or the [Presto official website](https://prestodb.io/docs/current/connector/iceberg.html).

<span id="_2-2-1-创建表"></span>
#### 2.2.1 Create a table

```sql
CREATE TABLE iceberg.default.customer_orders (
    order_id BIGINT,
    order_date DATE,
    account_number BIGINT,
    customer VARCHAR,
    country VARCHAR
 )
 WITH (
    format = 'ORC',
    partitioning = ARRAY['bucket(account_number, 10)','country']
 )
```


<span id="_2-2-2-写入数据"></span>
#### 2.2.2 Write data

```sql
INSERT INTO iceberg.default.customer_orders VALUES (2, CAST('2021-01-12' AS DATE), 670011, 'bcd', 'ca');
INSERT INTO iceberg.default.customer_orders VALUES (2, CAST('2021-01-12' AS DATE), 670012, 'bcde', 'cn');
```


<span id="_2-2-3-查询数据"></span>
#### 2.2.3 Query data

**Query statement example:** 

```sql
SELECT * FROM iceberg.default.customer_orders;
```


**Output example:** 

```Plain
order_id | order_date | account_number | customer | country
----------+------------+----------------+----------+---------
       1 | 2021-10-11 |        1002123 | abc      | us
       2 | 2021-01-12 |         670011 | bcd      | ca
       2 | 2022-02-11 |        9070011 | efg      | cn
       2 | 2022-01-01 |         560012 | zxc      | us
(4 rows)
```


**Add filter conditions:** 

```sql
SELECT * FROM iceberg.default.customer_orders WHERE account_number = 670012;
```


<span id="_2-2-4-查看执行计划"></span>
#### 2.2.4 View the execution plan

```sql
EXPLAIN ANALYZE SELECT * SELECT iceberg.default.customer_orders WHERE account_number = 670012;
```


<span id="_2-2-5-查看表信息"></span>
#### 2.2.5 View table information

```sql
DESC customer_orders;
```


<span id="_2-2-6-时间旅行（time-travel）"></span>
#### 2.2.6 Time travel

**View snapshots:** 

```sql
SELECT * FROM "customer_orders$snapshots"
```


**Output example:** 

```sql
committed_at              |     snapshot_id     |      parent_id      | operation |
---------------------------------------+---------------------+---------------------+-----------+------------------------------------------------------------------
 2022-01-13 13:34:00.657 Asia/Shanghai | 1942301704603642054 |                NULL | append    | hdfs://emr-master-1-1:8020/warehouse/tablespace/managed/hive/custom
 2022-01-13 13:39:18.665 Asia/Shanghai | 2127546335909550653 | 1942301704603642054 | append    | hdfs://emr-master-1-1:8020/warehouse/tablespace/managed/hive/custom
 2022-01-17 19:56:28.807 Asia/Shanghai | 6215604771056148566 | 2127546335909550653 | append    | hdfs://emr-master-1-1:8020/warehouse/tablespace/managed/hive/custom
 2022-01-17 19:57:12.160 Asia/Shanghai | 7079051850206849569 | 6215604771056148566 | append    | hdfs://emr-master-1-1:8020/warehouse/tablespace/managed/hive/custom
 2022-01-17 19:57:55.779 Asia/Shanghai | 3727192433427494890 | 7079051850206849569 | append    | hdfs://emr-master-1-1:8020/warehouse/tablespace/managed/hive/custom
(5 rows)
```


**Time travel query:** 

```sql
SELECT count(*) FROM "customer_orders@6215604771056148566";
 _col0
-------
     2
(1 row)

SELECT count(*) FROM "customer_orders@3727192433427494890";
 _col0
-------
     4
(1 row)
```


<span id="_2-2-7-回滚到特定版本"></span>
#### 2.2.7 Roll back to a specific version

```sql
CALL iceberg.system.rollback_to_snapshot('default', 'customer_orders', 3727192433427494890);
```


<span id="_2-2-8-分区"></span>
#### 2.2.8 Partitioning

```sql
SELECT * FROM "customer_orders$partitions";
```


```sql
partition               | record_count | file_count | total_size |
---------------------------------------+--------------+------------+------------+---------------------------------------------------------------------------------
 {account_number_bucket=9, country=us} |            1 |          1 |        714 | {order_id={min=2, max=2, null_count=0}, order_date={min=2022-01-01, max=2022-01-
 {account_number_bucket=2, country=ca} |            1 |          1 |        711 | {order_id={min=2, max=2, null_count=0}, order_date={min=2021-01-12, max=2021-01-
 {account_number_bucket=1, country=us} |            1 |          1 |        711 | {order_id={min=1, max=1, null_count=0}, order_date={min=2021-10-11, max=2021-10-
 {account_number_bucket=5, country=cn} |            1 |          1 |        716 | {order_id={min=2, max=2, null_count=0}, order_date={min=2022-02-11, max=2022-02-
```
