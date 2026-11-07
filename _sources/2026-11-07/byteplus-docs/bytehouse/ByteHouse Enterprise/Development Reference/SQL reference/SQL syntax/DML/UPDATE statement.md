---
title: "UPDATE statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-update-statement"
---

You can use this basic query format to update data. For details, please refer to [The update operation (UPDATE)](https://docs.byteplus.com/docs/bytehouse/ce-alter-statement#5af6af32).

<span id="31fef4de"></span>
## Grammar

```SQL
ALTER TABLE [db.]table UPDATE column1 = expr1 [, ...] [IN PARTITION partition_id] WHERE filter_expr;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>ALTER TABLE</code> prefix makes this syntax different from most other systems that support SQL. Its purpose is to indicate that, unlike similar queries in OLTP databases, this is a heavy operation and is not designed for frequent use.</div>


**Parameter description**:

[IN PARTITION partition_id]: If the table contains a large amount of data or has many partitions, it is recommended to add this condition and perform the update operation at the partition level for faster and more stable performance.

**Limitations**:


1. `filter_expr` must be of type `UInt8`. This query updates the value of the specified column to the value of the corresponding expression in the row, for those rows where the value of `filter_expr` is not zero. Use the `CAST` operator to map the numerical value to the type of the column. Update of columns used to calculate the primary key or partition key is not supported.

2. A query can contain several commands separated by commas.

3. By default, query processing for this statement is asynchronous.


<span id="04fb0234"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table (cluster-level)
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE if not exists sample_db.sample_table ON CLUSTER sample_cluster (
    uint8 UInt8,
    bool UInt8  
) ENGINE = MergeTree()
ORDER BY uint8;

-- 3. Insert test data
INSERT INTO sample_db.sample_table (uint8, bool) VALUES
(20, 0),
(21, 0),
(22, 0);

-- 4. Verify initial data
SELECT * FROM sample_db.sample_table ORDER BY uint8;

-- 5. Run ALTER UPDATE (update the bool field to 1 for rows where uint8 is 21)
ALTER TABLE sample_db.sample_table
UPDATE bool = 1
WHERE uint8 = 21;

-- 6. Verify the update result
SELECT * FROM sample_db.sample_table ORDER BY uint8;
```


&nbsp;
