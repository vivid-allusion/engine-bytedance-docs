---
title: "Insert overwrite"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/Insert-Overwrite"
---

The `INSERT OVERWRITE ...` statement is used to overwrite a table or specific partitions of a table, writing data as an atomic operation. When replacing partitions, imported data that does not match the specified partitions is automatically filtered.

<span id="8b4a8ac9"></span>
### Caution


* When executing the `INSERT OVERWRITE` statement, a partition lock or table lock must be acquired. The write task for each partition or table is executed serially, meaning the concurrency for writing to a single partition or table is 1 and cannot be adjusted.

* Do not write data to the same table simultaneously using `INSERT OVERWRITE` and real\-time write methods ([INSERT INTO](https://docs.byteplus.com/en/docs/bytehouse/insert-statement#insert-into), [DELETE](https://docs.byteplus.com/en/docs/bytehouse/delete-statement), [UPDATE](https://docs.byteplus.com/en/docs/bytehouse/update-statement)), otherwise data written in real time will be discarded.


<span id="cf497426"></span>
### Basic **syntax**

```SQL
INSERT OVERWRITE TABLE table_name
    [ PARTITION (p1,... | *) ]
    [ (COLUMN [,...]) ]
    { VALUES ([,...] ), ([,...]) | QUERY }
```


**Parameter description**


|Parameter |Required |Configuration description |
|---|---|---|
|`table_name` |Yes |The name of the target table to be overwritten. |
|`PARTITION` |No |Specify the partitions to be overwritten (single partition / multiple partitions); if not specified, **the entire table** will be overwritten. |
|`COLUMN` |No |The columns of the target table to be written; one or more columns can be specified. When specifying multiple columns, use commas to separate them and enclose them in parentheses.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If COLUMN is not specified, the system will use the field order defined in the CREATE TABLE statement by default.</div><br> |
|`VALUES` |Yes |The list of values to be written, suitable for overwriting with a small amount of fixed data. Choose either `QUERY` or VALUES. |
|`QUERY` |Yes |The `query` to be written, suitable for batch data overwriting (imported from other tables). Choose either `VALUES` or QUERY. |


<span id="0e354d80"></span>
### Example 1: Single partition key table

This section demonstrates the use of INSERT OVERWRITE in scenarios with a single partition key table.

The table creation statement example is as follows:

```SQL
-- 1. Create a test database (create if it does not exist)
CREATE DATABASE IF NOT EXISTS test_db;

-- 2. Switch to the test database (subsequent operations are performed in this database by default)
USE test_db;

-- 3. Create a single partition key table
CREATE TABLE IF NOT EXISTS single_part_sales (
    id Int32,
    sales_amount DECIMAL(10,2),
    dt String
) ENGINE = CnchMergeTree() 
ORDER BY (id) 
PARTITION BY (dt);

-- 4. Insert initial data
INSERT INTO single_part_sales 
VALUES 
    (1, 150.50, '20240101'), 
    (2, 200.00, '20240101'),
    (3, 300.25, '20240102'), 
    (4, 180.75, '20240102');

-- 5. View initial data (confirm successful insertion)
SELECT * FROM single_part_sales;

-- 6. Create a source table (stores new data to be overwritten)
CREATE TABLE IF NOT EXISTS source_sales (
    id Int32,
    sales_amount DECIMAL(10,2),
    dt String
) ENGINE = CnchMergeTree()
ORDER BY (id);

-- 7. Insert new data into the source table (used to overwrite the target table)
INSERT INTO source_sales 
VALUES 
    (5, 250.00, '20240101'),
    (6, 320.50, '20240101');
```



* Single partition key + SELECT overwrite

   ```SQL
   -- Use INSERT OVERWRITE + SELECT to overwrite the dt='20240101' partition of the target table
   INSERT OVERWRITE test_db.single_part_sales 
   PARTITION ('20240101') 
   SELECT id, sales_amount, dt FROM test_db.source_sales WHERE dt='20240101';
   
   -- View the overwritten data (only the dt='20240101' partition is replaced, dt='20240102' remains unchanged)
   SELECT * FROM single_part_sales;
   ```
   

* Single partition key + VALUES overwrite

   ```SQL
   -- Use INSERT OVERWRITE + VALUES to overwrite the dt='20240102' partition
   INSERT OVERWRITE test_db.single_part_sales 
   PARTITION ('20240102')  
   VALUES 
       (7, 400.00, '20240102'),
       (8, 150.25, '20240102');
   
   -- View the overwritten data (the dt='20240102' partition is replaced)
   SELECT * FROM single_part_sales;
   ```
   

* Single partition key + multiple partitions overwrite

   ```SQL
   -- Overwrite two partitions simultaneously
   INSERT OVERWRITE test_db.single_part_sales 
   PARTITION ('20240101', '20240102')
   VALUES 
       (9, 500.00, '20240101'), 
       (10, 350.75, '20240101'), 
       (11, 200.50, '20240102'),
       (12, 450.00, '20240102');
   
   -- View the overwritten data (both partitions are replaced)
   SELECT * FROM single_part_sales;
   ```
   


<span id="156441ea"></span>
### Example 2: Multiple partition key table

This section demonstrates the use of INSERT OVERWRITE in scenarios with a multiple partition key table.

The table creation statement example is as follows:

```SQL
-- This example uses the test_db database created in Example 1

--- 1. Create a table with multiple partition keys
CREATE TABLE IF NOT EXISTS multi_part_sales (
    id Int32,
    sales_amount DECIMAL(10,2),
    dt String,
    region String
) ENGINE = CnchMergeTree()
ORDER BY (id)
PARTITION BY (dt, region);

-- 2. Insert initial data
INSERT INTO multi_part_sales 
VALUES 
    (1, 150.50, '20240101', 'north'),  
    (2, 200.00, '20240101', 'north'),  
    (3, 300.25, '20240101', 'south'), 
    (4, 180.75, '20240102', 'north');  

-- 3. View initial data
SELECT * FROM multi_part_sales;

-- 4. Create the source table
CREATE TABLE IF NOT EXISTS source_multi_sales (
    id Int32,
    sales_amount DECIMAL(10,2),
    dt String,
    region String
) ENGINE = CnchMergeTree()
ORDER BY (id);

-- 5. Insert new data
INSERT INTO source_multi_sales 
VALUES 
    (5, 250.00, '20240101', 'north'),
    (6, 320.50, '20240101', 'north'),
    (7, 400.75, '20240101', 'south'),
    (8, 280.00, '20240102', 'north');
```



* Multiple partition keys + multiple partitions overwrite

   ```SQL
   INSERT OVERWRITE multi_part_sales 
   PARTITION (('20240101', 'north'), ('20240101', 'south'))
   SELECT id, sales_amount, dt, region FROM test_db.source_multi_sales 
   WHERE dt='20240101' AND region IN ('north', 'south');
   
   -- View the overwritten data (only the specified two partitions are replaced, the third partition remains unchanged)
   SELECT * FROM multi_part_sales;
   ```
   

* Multiple partition keys + specified columns overwrite

   When specifying columns, all partition key columns must be included.

   ```SQL
   INSERT OVERWRITE multi_part_sales 
   PARTITION (('20240102', 'north')) 
   (dt, region, id, sales_amount)   
   SELECT dt, region, id, sales_amount 
   FROM test_db.source_multi_sales;
   
   -- View the overwritten data (only the specified columns of the target partition are replaced)
   SELECT * FROM multi_part_sales;
   ```
   

* Overwrite the entire table

   ```SQL
   -- Overwrite the entire table
   INSERT OVERWRITE test_db.multi_part_sales 
   SELECT 
       id + 10 AS id, 
       sales_amount * 1.1 AS sales_amount, 
       dt,
       region 
   FROM test_db.source_multi_sales; 
   
   -- View the result of overwriting the entire table (all old partition data is replaced with processed data from the source table)
   SELECT * FROM multi_part_sales;
   ```
