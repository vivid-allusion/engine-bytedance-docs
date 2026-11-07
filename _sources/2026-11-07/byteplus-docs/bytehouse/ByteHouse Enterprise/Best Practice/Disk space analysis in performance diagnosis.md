---
title: "Disk space analysis in performance diagnosis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/disk-space-analysis-in-performance-diagnosis"
---

The usage rate of ByteHouse Cluster's space is one of the key monitoring items in DataRanger's Technical Support. Lack of cluster storage space can lead to severe consequences, such as data being unable to be written, backed up, or lengthy storage expansion tasks. This article introduces how to view the disk space usage of the ByteHouse Cluster using SQL statements.

<span id="2dc89d5d"></span>
# **Example environment**

The following example uses the node 192.18. *.*  as the base environment; please change the corresponding parameters according to your scenes during actual use. If you do not know how to get the name of the node, you can obtain it by the following methods.


* Using SQL statements: You can run the following statement to get the name of all nodes in the cluster.


```SQL
SELECT * FROM system.clusters;
```


<span id="09b98503"></span>
# **Viewing table disk space usage**

By viewing the size of table data, you can identify the disk space occupied by the table, thereby providing a valid basis for optimizing your database performance and planning storage resources effectively.


* ### **View table data details**   <span id="view-table-data-details"></span>


View the situation of active data in each table under the `192.18.*.*` node.

```SQL
SELECT
    `database`,
    table,
    formatReadableSize(sum(data_compressed_bytes) AS size) AS compressed, --Size of compressed data
    formatReadableSize(sum(data_uncompressed_bytes) AS usize) AS uncompressed, --Size of uncompressed data
    round(usize / size, 2) AS compr_rate, --Compression rate
    sum(rows) AS rows, --Total number of rows
    count() AS part_count --Number of parts
FROM clusterAllReplicas('', system.parts)
WHERE (active = 1) AND (table LIKE '%') AND (`database` LIKE '%') 
AND host() = '192.18.*.*'
GROUP BY
    `database`,
    table
ORDER BY size DESC;
```



* ### **View replica table data details**   <span id="view-replica-table-data-details"></span>


View the table data in each replica.

```SQL
SELECT
    hostname() AS h,
   `database` ,
    table,
    count(*) AS data_part_cnt, --Total amount of data parts
    sum(rows) AS total_rows, --Total number of rows
    formatReadableSize(sum(bytes_on_disk)) AS total_compressed_bytes, --Size of compressed data
    sum(data_uncompressed_bytes) AS total_uncompressed_bytes  --Size of uncompressed data
FROM clusterAllReplicas('', system.parts) 
WHERE active = 1
GROUP BY h, `database`, table
ORDER BY total_rows DESC;
```



* ### **View the ranking of table disk space usage**   <span id="view-the-ranking-of-table-disk-space-usage"></span>


View the top ten tables in the cluster by disk space usage.

```SQL
SELECT
    `database`,
    table,
    sum(bytes_on_disk) AS bytes_on_disk
FROM clusterAllReplicas('', system.parts)
WHERE active AND (`database` != 'system')
GROUP BY
    `database`,
    table
ORDER BY bytes_on_disk DESC
LIMIT 10;
```


<span id="1bb90e6a"></span>
## View storage information of each column in the table

**Search template**

```SQL
SELECT
    `database`,
    table,
    column,
    formatReadableSize(sum(column_data_compressed_bytes) AS size) AS compressed,
    formatReadableSize(sum(column_data_uncompressed_bytes) AS usize) AS uncompressed,
    round(usize / size, 2) AS compr_rate,
    sum(rows) rows_cnt,
    round(sum(column_data_uncompressed_bytes)/sum(rows) ,2) avg_row_size
FROM clusterAllReplicas('', system.parts_columns) 
WHERE (active = <active_type>) AND (table LIKE '')  
   AND host() = ''
GROUP BY
    `database`,
    table,
    column
ORDER BY size DESC;
```


**Parameter description**


|**Param** |**Description** |
|---|---|
|cluster_name |Cluster name |
|table_name |Target table name.<br><br>When the value is %, it matches all tables. |
|node_name |Target cluster node name. |
|active_type |Is the data active?<br><br><br>* 0: Inactive.<br><br>* 1: Active. |


**Example**

View `192.18.*.*` node's `query_log` table for columns storing active data.

```SQL
SELECT
    `database`,
    table,
    column,
    formatReadableSize(sum(column_data_compressed_bytes) AS size) AS compressed,
    formatReadableSize(sum(column_data_uncompressed_bytes) AS usize) AS uncompressed,
    round(usize / size, 2) AS compr_rate,
    sum(rows) rows_cnt,
    round(sum(column_data_uncompressed_bytes)/sum(rows) ,2) avg_row_size
FROM clusterAllReplicas('', system.parts_columns) 
WHERE (active = 1) 
AND (table LIKE 'query_log')  
AND host() = '192.18.*.*'
GROUP BY
    `database`,
    table,
    column
ORDER BY size DESC;
```


<span id="b5396f33"></span>
## View table partition information

**Search template**

```SQL
SELECT 
    partition AS `patition`,
    sum(rows) AS `total_number_of_rows`,
    formatReadableSize(sum(data_uncompressed_bytes)) AS `original_size`,
    formatReadableSize(sum(data_compressed_bytes)) AS `compression_size`,
    round((sum(data_compressed_bytes) / sum(data_uncompressed_bytes)) * 100, 0) AS `compression_rate`
FROM clusterAllReplicas('', system.parts)
WHERE (database IN ('')) 
AND (table IN ('')) 
AND (partition LIKE '')
GROUP BY partition
ORDER BY partition ASC
```


**Parameter description**


|**Param** |**Description** |
|---|---|
|cluster_name |Cluster name |
|database_name |Database name. |
|table_name |Table name. |
|partition_prefix |Partition prefix. |


**Example**

View the partition information for the test table in the `test table in the` database with partition prefix `2019-12-`.

```SQL
SELECT 
    partition AS `patition`,
    sum(rows) AS `total_number_of_rows`,
    formatReadableSize(sum(data_uncompressed_bytes)) AS `original_size`,
    formatReadableSize(sum(data_compressed_bytes)) AS `compression_size`,
    round((sum(data_compressed_bytes) / sum(data_uncompressed_bytes)) * 100, 0) AS `compression_rate`
FROM clusterAllReplicas('', system.parts)
WHERE (`database` IN ('')) 
AND (table IN ('test')) 
AND (partition LIKE '2019-12-%')
GROUP BY partition
ORDER BY partition ASC
```


<span id="5940a1d8"></span>
## **View** the size of datapart data

In ByteHouse, the `system.part` table stores `datapart` state, size, creation time, and other information. You can learn `datapart` details through this table.

<span id="2f1d9840"></span>
### **View the size of active datapart data**

The active `datapart` is the data currently being actively used in the table. Understanding the size of active data can help you identify the actual data size of the table, thus identifying the disk space occupied by the table.

View the active data partition information of all non\-system tables on the `192.18.*.*` node.

```SQL
SELECT 
    `database`, 
    table, 
    count(*) AS data_part_cnt,  --The number of active data partitions
    sum(rows) AS total_rows,  --The total number of rows
    formatReadableSize(sum(bytes_on_disk)) AS total_compressed_bytes, --The total compressed data size on disk
    sum(data_uncompressed_bytes) AS total_uncompressed_bytes --The total uncompressed data size
FROM clusterAllReplicas('', system.parts )
WHERE active = 1 AND `database` != 'system' 
AND host() = '192.18.*.*'
GROUP BY `database`, table 
ORDER BY total_rows DESC;
```


<span id="e8202197"></span>
### **View the size of inactive datapart data**

Inactive `datapart` may contain outdated or data marked for deletion. If this data is no longer needed, it is advisable to clean it up promptly to reduce disk usage.

View the inactive data partition information of all non\-system tables on the `192.18.*.*` node.

```SQL
SELECT 
    `database`, 
    table, 
    count(*) AS data_part_cnt, --The number of inactive data partitions
    sum(rows) AS total_rows,  --The total number of rows
    formatReadableSize(sum(bytes_on_disk)) AS total_compressed_bytes,  --The total size of compressed data on disk
    sum(data_uncompressed_bytes) AS total_uncompressed_bytes  --The total size of uncompressed data
FROM clusterAllReplicas('', system.parts )
WHERE active = 0 
AND `database` != 'system' 
AND host() = '192.18.*.*'
GROUP BY `database`, table;
```


<span id="95967f80"></span>
## Projection occupies disk space size

Projections in ByteHouse are a data structure used to optimize query performance, similar to materialized views, storing pre\-calculated aggregates or data transformation results. Understanding the size of Projections helps assess their impact on disk space.

View the disk space occupied by the Projections on the `192.18.*.*` node for the `test` table.

```SQL
SELECT
    database,
    table,
    name,
    formatReadableSize(sum(data_compressed_bytes) AS size) AS compressed, --Size of compressed data
    formatReadableSize(sum(data_uncompressed_bytes) AS usize) AS uncompressed, --Size of uncompressed data
    round(usize / size, 2) AS compr_rate, --Compression ratio
    sum(rows) AS rows,  --Total number of rows
    count() AS part_count  --Total number of parts
FROM clusterAllReplicas('', system.projection_parts )
WHERE (table = 'test') 
AND (active = 1) AND host() = '192.18.*.*'
GROUP BY
    database,
    table,
    name
ORDER BY size DESC;
```


View the disk space occupied by each Projection column on the `192.18.*.*` node for the `test` table.

```SQL
SELECT
    database,
    table,
    column,
    formatReadableSize(sum(column_data_compressed_bytes) AS size) AS compressed, --Size of compressed data
    formatReadableSize(sum(column_data_uncompressed_bytes) AS usize) AS uncompressed, --Size of uncompressed data
    round(usize / size, 2) AS compr_rate --Compression ratio
FROM clusterAllReplicas('', system.projection_parts_columns )
WHERE (active = 1) AND (table LIKE 'test') 
AND host() = '192.18.*.*'
GROUP BY
    database,
    table,
    column
ORDER BY size DESC;
```
