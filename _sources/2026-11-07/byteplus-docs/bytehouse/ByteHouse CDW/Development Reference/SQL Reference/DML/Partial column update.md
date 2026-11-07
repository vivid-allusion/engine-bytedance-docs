---
title: "Partial column update"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/partial-column-update"
---

ByteHouse CDW supports partial column updates on unique\-key tables, suitable for: Data update operations from multiple data sources, each updating parts of the rows from different columns; performing ETL operations on existing data to update parts of the columns. This article introduces the working principles and usage examples of partial column updates.

<span id="bab0d8ea"></span>
# Function overview

Partial column updates use **function column**`_update_columns_` to specify which columns are to be updated.


* The contents in `_update_columns_` are the columns that need updating, separated by **commas between column names**. During analysis, **the engine does not process special characters before and after column names**, such as spaces, Tab, newline characters, and does not support regular expressions.

* `_update_columns_` supports two modes: proactive specification and automatic analysis. **When proactively specified**  **`_update_columns_`**  ** as **  **`''`**  **, it implies updating all columns**.


The column update method of `_update_columns_` follows these rules:


* For non\-Map type: If a column belongs to `_update_columns_`, it’s updated directly, allowing updates to default values.

* Map Type: `When partial_update_enable_merge_map = true`, update the old keys with old values, write new keys directly, and keep the original values for the keys not updated; When false, replace value directly.

* Nullable Type: When using the `REPLACE_IF_NOT_NULL` semantics, writing null retains the old value.


<span id="0fad8bbd"></span>
# Working principle

Partial Column Update involves the following steps:


1. Locate the existing data position based on the incremental data and unique key index.

2. Read the relevant columns of the existing data (the red sections in the example diagram below).

3. Set the delete bitmap column of the corresponding row of the existing data to 1, marking it for deletion.

4. Incremental data generation.


Below is an example, where the table in the example is partition\-level unique, PK is the partition key, UK is the unique key, and the delete bitmap is the marking for deletion column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51eb2e170b2440b598652033eddef3ce~tplv-goo7wpa0wc-image.image) </span>

Data in the Delete bitmap column marked as 1 are marked deleted, after writing incremental data and through partial column updates, the latest data is:

```SQL
2020-10-29，1，m，1001
2020-10-29，2，n，1002
2020-10-30，1，z，2001
2020-10-30，2，k，0
```


<span id="8a252774"></span>
# Examples


* **partial_update_enable_merge_map = false**

   ```SQL
   -- The engine by default guarantees the uniqueness of the unique key within the partition
   CREATE TABLE t8 (
     k Int32,
     c1 Int32,
     c2 Nullable(Float64),
     c3 Nullable(String),
     c4 Nullable(Int64),
     m1 Map(String, Int32),
     a1 Array(String))
   ENGINE = CnchMergeTree
   UNIQUE KEY k ORDER BY k SETTINGS enable_unique_partial_update = 1, 
   partial_update_enable_merge_map = 0;
   
   -- It can be not set explicitly. The default value of enable_unique_partial_update at the session level is 1
   SET enable_unique_partial_update = 1; 
   
   -- If update_columns is not specified, it will automatically parse and fill update_columns as 'k,c1,c2,m1,a1',
   -- which is equivalent to INSERT INTO t8 (k, c1, c2, m1, a1, update_columns) VALUES (1, 10, 3.14, {'k1':1}, ['hello'], 'k,c1,c2,m1,a1');
   INSERT INTO t8 (k, c1, c2, m1, a1) VALUES (1, 10, 3.14, {'k1':1}, ['hello']);
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐
   │ 1 │ 10 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k1':1} │ ['hello'] │
   └───┴────┴──────┴──────┴──────┴──────────┴───────────┘
   
   -- When specifying update_columns explicitly, the bold font represents the updated columns
   INSERT INTO t8 (k, c1, m1, a1, _update_columns_) VALUES (1, 20, {'k2':2}, ['world'], 'k,c1,m1,a1');
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐
   │ 1 │ 20 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k2':2} │ ['world'] │
   └───┴────┴──────┴──────┴──────┴──────────┴───────────┘
   
   -- When update_columns is specified explicitly, the columns that are not in update_columns will not be updated even if there is data for them
   INSERT INTO t8 (k, c1, m1, a1, _update_columns_) VALUES (1, 200, {'k2':20}, ['world20'], 'k');
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐
   │ 1 │ 20 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k2':2} │ ['world'] │
   └───┴────┴──────┴──────┴──────┴──────────┴───────────┘
   
   -- If update_columns is not specified, it will automatically parse and fill update_columns as 'k,c1,c3,m1',
   -- which is equivalent to INSERT INTO t8 (k, c1, c3, m1, update_columns) VALUES (1, 0, 'foo', {'k3':3}, 'k,c1,c3,m1');
   INSERT INTO t8 (k, c1, c3, m1) VALUES (1, 0, 'foo', {'k3':3});
   ┌─k─┬─c1─┬───c2─┬─c3──┬───c4─┬─m1───────┬─a1────────┐
   │ 1 │  0 │ 3.14 │ foo │ ᴺᵁᴸᴸ │ {'k3':3} │ ['world'] │
   └───┴────┴──────┴─────┴──────┴──────────┴───────────┘
   
   -- When update_columns is explicitly specified as '', it means updating all columns.
   INSERT INTO t8 (k, c1, c2, c3, c4, m1, a1, _update_columns_) VALUES (1, 10, 31.4, 'goo', 15, {'k4': 4}, ['hello', 'world'], '');
   ┌─k─┬─c1─┬───c2─┬─c3──┬─c4─┬─m1───────┬─a1────────────────┐
   │ 1 │ 10 │ 31.4 │ goo │ 15 │ {'k4':4} │ ['hello','world'] │
   └───┴────┴──────┴─────┴────┴──────────┴───────────────────┘
   
   -- A more flexible usage: Specify update_columns at the row level
   INSERT INTO t8 (k, c1, c2, c3, c4, m1, a1, _update_columns_) FORMAT JSONEachRow {"k":"1", "c1": "100", "_update_columns_":"k,c1"} {"k":"1", "c2": "314.0", "_update_columns_":"k,c2"};
   ┌─k─┬──c1─┬──c2─┬─c3──┬─c4─┬─m1───────┬─a1────────────────┐
   │ 1 │ 100 │ 314 │ goo │ 15 │ {'k4':4} │ ['hello','world'] │
   └───┴─────┴─────┴─────┴────┴──────────┴───────────────────┘
   ```
   

* **partial_update_enable_merge_map = true**

   ```SQL
   -- The engine guarantees the uniqueness of the unique key within a partition by default.
   CREATE TABLE t8m (
     k Int32,
     c1 Int32,
     c2 Nullable(Float64),
     c3 Nullable(String),
     c4 Nullable(Int64),
     m1 Map(String, Int32),
     a1 Array(String))
   ENGINE = CnchMergeTree
   UNIQUE KEY k ORDER BY k SETTINGS enable_unique_partial_update = 1, 
   partial_update_enable_merge_map = 1;
   
   -- No need to set it explicitly. The default value of enable_unique_partial_update at the session level is 1.
   SET enable_unique_partial_update = 1; 
   
   -- If _update_columns_ is not specified, it will be automatically parsed and filled with 'k,c1,c2,m1,a1'.
   -- This is equivalent to INSERT INTO t8m (k, c1, c2, m1, a1, _update_columns_) VALUES (1, 10, 3.14, {'k1':1}, ['hello'], 'k,c1,c2,m1,a1');
   INSERT INTO t8m (k, c1, c2, m1, a1) VALUES (1, 10, 3.14, {'k1':1}, ['hello']);
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐
   │ 1 │ 10 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k1':1} │ ['hello'] │
   └───┴────┴──────┴──────┴──────┴──────────┴───────────┘
   
   -- When specifying _update_columns_ explicitly, the bold - faced text indicates the updated columns.
   INSERT INTO t8m (k, c1, m1, a1, _update_columns_) VALUES (1, 20, {'k2':2}, ['world'], 'k,c1,m1,a1');
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1──────────────┬─a1────────┐
   │ 1 │ 20 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k1':1,'k2':2} │ ['world'] │
   └───┴────┴──────┴──────┴──────┴─────────────────┴───────────┘
   
   -- When _update_columns_ is specified explicitly, columns not included in _update_columns_ will not be updated even if there is data for them.
   INSERT INTO t8m (k, c1, m1, a1, _update_columns_) VALUES (1, 200, {'k2':20}, ['world20'], 'k');
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1──────────────┬─a1────────┐
   │ 1 │ 20 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k1':1,'k2':2} │ ['world'] │
   └───┴────┴──────┴──────┴──────┴─────────────────┴───────────┘
   
   -- If _update_columns_ is not specified, it will be automatically parsed and filled with 'k,c1,c3,m1'.
   -- This is equivalent to INSERT INTO t8m (k, c1, c3, m1, _update_columns_) VALUES (1, 0, 'foo', {'k3':3}, 'k,c1,c3,m1');
   INSERT INTO t8m (k, c1, c3, m1) VALUES (1, 0, 'foo', {'k3':3});
   ┌─k─┬─c1─┬───c2─┬─c3──┬───c4─┬─m1──────────────────────┬─a1────────┐
   │ 1 │  0 │ 3.14 │ foo │ ᴺᵁᴸᴸ │ {'k1':1,'k2':2,'k3':3} │ ['world'] │
   └───┴────┴──────┴─────┴──────┴─────────────────────────┴───────────┘
   
   -- When _update_columns_ is explicitly set to an empty string, it means all columns will be updated.
   INSERT INTO t8m (k, c1, c2, c3, c4, m1, a1, _update_columns_) VALUES (1, 10, 31.4, 'goo', 15, {'k4': 4}, ['hello', 'world'], '');
   ┌─k─┬─c1─┬───c2─┬─c3──┬─c4─┬─m1─────────────────────────────┬─a1────────────────┐
   │ 1 │ 10 │ 31.4 │ goo │ 15 │ {'k1':1,'k2':2,'k3':3,'k4':4} │ ['hello','world'] │
   └───┴────┴──────┴─────┴────┴────────────────────────────────┴───────────────────┘
   
   -- A more flexible approach: Specify _update_columns_ at the row level.
   INSERT INTO t8m (k, c1, c2, c3, c4, m1, a1, _update_columns_) FORMAT JSONEachRow {"k":"1", "c1": "100", "_update_columns_":"k,c1"} {"k":"1", "c2": "314.0", "_update_columns_":"k,c2"};
   ┌─k─┬──c1─┬──c2─┬─c3──┬─c4─┬─m1─────────────────────────────┬─a1────────────────┐
   │ 1 │ 100 │ 314 │ goo │ 15 │ {'k1':1,'k2':2,'k3':3,'k4':4} │ ['hello','world'] │
   └───┴─────┴─────┴─────┴────┴────────────────────────────────┴───────────────────┘
   ```
   

* **REPLACE_IF_NOT_NULL semantics**

   ```SQL
   -- The engine guarantees the uniqueness of the unique key within a partition by default.
   CREATE TABLE t8n (
     k Int32,
     c1 Int32,
     c2 Nullable(Float64) REPLACE_IF_NOT_NULL,
     c3 Nullable(String),
     c4 Nullable(Int64),
     m1 Map(String, Int32),
     a1 Array(String))
   ENGINE = CnchMergeTree
   UNIQUE KEY k ORDER BY k SETTINGS enable_unique_partial_update = 1, 
   partial_update_enable_merge_map = 1;
   
   -- No need to set it explicitly. The default value of enable_unique_partial_update at the session level is 1.
   SET enable_unique_partial_update = 1; 
   
   -- If _update_columns_ is not specified, it will be automatically parsed and filled with 'k,c1,c2,c3,m1,a1'.
   -- This is equivalent to INSERT INTO t8n (k, c1, c2, c3, m1, a1, _update_columns_) VALUES (1, 10, 3.14, 'foo', {'k1':1}, ['hello'], 'k,c1,c2,c3,m1,a1');
   INSERT INTO t8n (k, c1, c2, c3, m1, a1) VALUES (1, 10, 3.14, 'foo', {'k1':1}, ['hello']);
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1───────┬─a1────────┐
   │ 1 │ 10 │ 3.14 │ foo │ ᴺᵁᴸᴸ │ {'k1':1} │ ['hello'] │
   └───┴────┴──────┴──────┴──────┴──────────┴───────────┘
   
   -- If _update_columns_ is not specified, it will be automatically parsed and filled with 'k,c2,c3,m1,a1'.
   -- When writing null to c2, based on the REPLACE_IF_NOT_NULL semantics, the old value is retained.
   -- When writing null to c3, the data column is updated to null. The bold-faced text indicates the updated columns.
   INSERT INTO t8n (k, c2, c3, m1, a1) VALUES (1, null, null, {'k2':2}, ['world']);
   ┌─k─┬─c1─┬───c2─┬─c3───┬───c4─┬─m1──────────────┬─a1────────┐
   │ 1 │ 10 │ 3.14 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ │ {'k1':1,'k2':2} │ ['world'] │
   └───┴────┴──────┴──────┴──────┴─────────────────┴───────────┘
   ```
   

* **Insert on duplicate key syntax**

   ```SQL
   -- Attention：
   -- 1. It is necessary to enable partial column update, that is, set enable_unique_partial_update = 1.
   -- 2. The conversion done by the on duplicate action should ensure that:
       -- The data types before and after the conversion are the same, or the columns before and after the conversion are both numeric types.
   :) CREATE TABLE mysql_test_on_duplicate_action (
       `a` Int32,
       `b` Int32
   )
   ENGINE = CnchMergeTree
   ORDER BY a
   UNIQUE KEY a
   SETTINGS enable_unique_partial_update = 1;
   
   :) insert into mysql_test_on_duplicate_action values (1, 1);
   :) select * from mysql_test_on_duplicate_action;
   ┌─a─┬─b─┐
   │ 1 │ 1 │
   └───┴───┘
   
   :) insert into mysql_test_on_duplicate_action on duplicate key update b=4 values (1, 2), (2, 3);
   :) select * from mysql_test_on_duplicate_action;
   ┌─a─┬─b─┐
   │ 1 │ 4 │
   │ 2 │ 3 │
   └───┴───┘
   ```
