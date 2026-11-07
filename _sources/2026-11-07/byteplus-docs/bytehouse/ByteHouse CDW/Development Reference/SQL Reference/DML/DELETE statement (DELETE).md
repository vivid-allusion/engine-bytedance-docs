---
title: "DELETE statement (DELETE)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/delete-statement"
---

The DELETE statement is used to remove row data from specified columns in the target table.

<span id="a2e5f1eb"></span>
# Usage restrictions

Currently, only tables with unique keys support the use of DELETE statements. For other types of tables, please use the "ALTER TABLE \- DELETE" statement. For more details, refer to [Delete operations (DELETE)](https://docs.byteplus.com/docs/bytehouse/alter-statement#2c1cbd0d).

<span id="408df7a3"></span>
# **Syntax**

```SQL
DELETE FROM [db.]table WHERE expr;
```


<span id="e3d1cfba"></span>
# **Example**

```SQL
-- The engine guarantees the uniqueness of the unique key within a partition by default.

CREATE TABLE  test.unique_table
(
  `event_time` DateTime,
  `product_id` UInt64,
  `city` String,
  `category` String,
  `amount` UInt32,
  `revenue` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY toDate(event_time)
ORDER BY (city, category)
UNIQUE KEY product_id;

INSERT INTO  test.unique_table VALUES
('2020-10-29 23:40:00', 10001, 'Beijing', 'men wear', 5, 500),
('2020-10-29 23:40:00', 10002, 'Beijing', 'men wear', 2, 200),
('2020-10-29 23:40:00', 10003, 'Beijing', 'men wear', 1, 100);

-- Delete the data where revenue == 500 through the statement "DELETE FROM".
DELETE FROM  test.unique_table WHERE revenue = 500;
-- Delete the data where revenue >= 200 through the statement "DELETE FROM".
DELETE FROM  test.unique_table WHERE revenue >= 200;

-- The data where revenue >= 200 has been deleted in the query results
select * from  test.unique_table order by toDate(event_time), product_id;
┌──────────event_time─┬─product_id─┬─city────┬─category───────┬─amount─┬─revenue─┐
│ 2020-10-29 23:40:00 │      10003 │ Beijing │ men wear       │      1 │     100 │
└─────────────────────┴────────────┴─────────┴────────────────┴────────┴─────────┘
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you need to delete the entire partition's data, it is suggested to use the <code>DROP PARTITION</code> command to do so, as it is more efficient and faster. For operation details, refer to <a href="https://docs.byteplus.com/docs/bytehouse/alter-statement#fa617d8c">DROP PARTITION|PART</a>.</div>
