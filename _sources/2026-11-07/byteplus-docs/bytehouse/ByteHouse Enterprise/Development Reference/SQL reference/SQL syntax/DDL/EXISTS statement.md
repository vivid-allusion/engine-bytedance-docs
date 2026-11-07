---
title: "EXISTS statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-exists-statement"
---

Use the EXISTS statement to check whether a table or database exists. After executing this statement, a single `UInt8` type column is returned. If the table or database does not exist, it contains a value `0`. If the table exists in the specified database, it contains a value `1`.

<span id="54ec8f35"></span>
## **Grammar**

```SQL
EXISTS [TEMPORARY] [TABLE|DICTIONARY] [db.]name
```


<span id="7508a584"></span>
## **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a table
DROP TABLE IF EXISTS sample_db.sample_able ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_able ON CLUSTER sample_cluster (
  id UInt32,
  name String DEFAULT '',
  CONSTRAINT constraint1 CHECK id > 10
)
ENGINE=MergeTree()
ORDER BY id;

-- 3. Check if a table exists
exists table sample_db.sample_able;
```
