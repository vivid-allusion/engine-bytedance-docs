---
title: "DELETE statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-delete-statement"
---

To delete data in ByteHouse, use the `ALTER DELETE` method. For more operation details, please refer to [Delete operation (DELETE)](https://docs.byteplus.com/docs/bytehouse/ce-alter-statement#a18841cd).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For HaMergeTree tables, <code>DELETE WHERE</code> can only be performed on local tables and is not supported on distributed tables.</div>


* <div data-tips="true" data-tips-type="warning">The <code>DELETE WHERE</code> syntax is supported only in ByteHouse Enterprise Edition v2.4 and above.</div>


* <div data-tips="true" data-tips-type="warning">Executing the <code>DELETE WHERE</code> syntax triggers a full table scan and rewrites all data blocks containing data, which can easily impose significant load pressure on the cluster. Frequent execution is strictly prohibited.</div>


* <div data-tips="true" data-tips-type="warning">For tables with cold storage enabled, the <code>DELETE WHERE</code> syntax should be used with caution to avoid greater performance loss and increased cluster pressure.</div>


* <div data-tips="true" data-tips-type="warning">To delete a large amount of data when using HaUniqueMergeTree and HaMergeTree tables, it is recommended to use FAST DELETE. For details, please refer to <a href="https://docs.byteplus.com/docs/bytehouse/ce-alter-statement#ad0c725f">FAST DELETE</a>.</div>



<span id="625b5350"></span>
## Syntax

```SQL
ALTER TABLE [tableIdentifier] DELETE [IN PARTITION partition_id] WHERE filter_expr;
```


**Parameter description**:

IN PARTITION: Optional. It specifies the target partition for the deletion operation. It supports specifying partition ID or partition name. When the table contains a large amount of data or has many parts, it is recommended to add this condition to perform the delete operation at the partition level for faster and more stable execution.

<span id="a616e119"></span>
## Example

```SQL
-- 1. Create a test database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create test tables
DROP TABLE IF EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
) ENGINE = HaMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
PARTITION BY partition_column
ORDER BY (`order_by_column`);

CREATE TABLE sample_db.sample_table
    AS sample_db.sample_table_local
    ENGINE = Distributed(sample_cluster, sample_db, sample_table_local, hour);

-- 3. Insert data
INSERT INTO sample_db.sample_table_local ON CLUSTER sample_cluster
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Delete data
ALTER TABLE sample_db.sample_table_local ON CLUSTER sample_cluster 
    DELETE WHERE browser = 'firefox';
    
-- 5. Query whether the deletion is successful
SELECT * 
FROM clusterAllReplicas(sample_cluster, system.mutations) 
WHERE 
   database = 'sample_db' 
   AND table = 'sample_table_local';
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the returned value of the <code>is_done</code> field is 1, it indicates that the delete operation has been executed successfully.</div>
