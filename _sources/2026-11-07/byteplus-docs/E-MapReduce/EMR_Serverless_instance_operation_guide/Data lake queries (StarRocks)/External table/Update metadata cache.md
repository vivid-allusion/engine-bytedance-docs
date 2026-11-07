---
title: "Update metadata cache"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Update_metadata_cache"
---

By default, StarRocks caches the metadata of Hive and Hudi, and automatically updates the cached metadata asynchronously to improve query performance. In addition, after a table schema is changed or updated, you can also use [REFRESH EXTERNAL TABLE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/REFRESH_EXTERNAL_TABLE/) to manually update the metadata, ensuring that StarRocks generates an optimal query plan at the earliest opportunity.

This document describes how to manually update the cached metadata.

<span id="_1-语法"></span>
## 1 Syntax

```sql
REFRESH EXTERNAL TABLE [external_catalog.][db_name.]<table_name>
[PARTITION ('partition_name', ...)]
```



|**Parameter** |**Required** |**Note** |
|---|---|---|
|external_catalog |No |Name of Hive catalog or Hudi catalog. |
|db_name |No |Name of the database where the Hive table or Hudi table resides. |
|table_name |Yes |Hive table or Hudi table name. |
|partition_name |No |Partition name in Hive table or Hudi table. If specified, updates the cached metadata of the specified partition in the Hive table or Hudi table. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only users with <code>ALTER_PRIV</code> permission can execute this statement to update the cached metadata.</div>


<span id="_2-示例"></span>
## 2 Examples

Example 1: Update the cached metadata of Hive table `hive_table`.

```sql
REFRESH EXTERNAL TABLE hive_catalog.hive_db.hive_table;
```


Or

```sql
USE hive_catalog.hive_db;
REFRESH EXTERNAL TABLE hive_table;
```


Example 2: Update the cached metadata of partitions `p1` and `p2` in Hudi table `hudi_table`.

```sql
REFRESH EXTERNAL TABLE hudi_catalog.hudi_db.hudi_table
PARTITION ('p1', 'p2');
```
