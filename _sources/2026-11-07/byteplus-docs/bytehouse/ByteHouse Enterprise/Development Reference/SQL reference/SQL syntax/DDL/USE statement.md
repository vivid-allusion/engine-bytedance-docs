---
title: "USE statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-use-statement"
---

Set the current database for the session. If the database is not explicitly specified before the table name with a dot in the query, the current database is used to search for the table.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using the HTTP protocol, it is not possible to perform this query because there is no concept of session.</div>


<span id="019772b0"></span>
## **Grammar**

```SQL
USE [databaseIdentifier];
```


<span id="feb0c48a"></span>
## **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Use a database
USE sample_db;
```
