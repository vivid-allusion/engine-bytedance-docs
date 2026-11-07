---
title: "StarRocks hybrid row-column storage table"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_hybrid_row-column_storage_table"
---

StarRocks is an OLAP database. Originally, data was stored in columns, which improves the performance of complex queries, such as aggregate queries. Starting from version 3.2.3, StarRocks also supports a hybrid row\-column table storage format. This enables high\-concurrency, low\-latency point queries based on primary keys, partial column updates, and other scenarios, while retaining the efficient analytical capabilities of the original columnar storage.

<span id="_1-整体架构"></span>
## 1 Overall architecture

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e935f255793a953fdb600ea030c43720.png) </span>

By using short\-circuit reads, certain optimization rules can be bypassed, reducing query path overhead.


* Queries on the FE side bypass the original planner.

* On the BE side, scheduling of the pipeline model is bypassed, and results are synchronized directly back to BE.


<span id="_2-短路读"></span>
## 2 Short\-circuit read

Short\-circuit reads can be used for both columnar storage and hybrid row\-column storage.


1. Ensure that short\-path queries are enabled in the system. After short\-path queries are enabled, queries that meet the conditions (used to determine whether it is a point query) will use the short path and directly query data stored by row.


```sql
SHOW VARIABLES LIKE '%enable_short_circuit%';
```



2. If short\-path queries are not enabled, you can execute the command `SET enable_short_circuit = true;` to set the variable `[enable_short_circuit](https://docs.starrocks.io/zh/docs/reference/System_variable/#enable_short_circuit323-%E5%8F%8A%E4%BB%A5%E5%90%8E)` to `true`.

3. The condition columns in the WHERE clause must include all primary key columns, and can also include other columns.


```sql
SELECT * FROM users WHERE id=1;
```


You can check the query plan to confirm whether the query uses the short path. If the query plan includes `Short Circuit Scan: true`, it means the query uses the short path.

```sql
MySQL [example_db] EXPLAIN SELECT * FROM users WHERE id=1;
+---------------------------------------------------------+
| Explain String                                          |
+---------------------------------------------------------+
| PLAN FRAGMENT 0                                         |
|  OUTPUT EXPRS:1: id | 2: country | 3: city | 4: revenue |
|   PARTITION: RANDOM                                     |
|                                                         |
|   RESULT SINK                                           |
|                                                         |
|   0:OlapScanNode                                        |
|      TABLE: users                                       |
|      PREAGGREGATION: OFF. Reason: null                  |
|      PREDICATES: 1: id = 1                              |
|      partitions=1/1                                     |
|      rollup: users                                      |
|      tabletRatio=1/6                                    |
|      tabletList=10184                                   |
|      cardinality=-1                                     |
|      avgRowSize=0.0                                     |
|      Short Circuit Scan: true                           | -- Short path query is effective
+---------------------------------------------------------+
17 rows in set (0.00 sec)
```


<span id="_3-行列混存"></span>
## 3 Hybrid row\-column storage

<span id="_3-1-创建行列混存表"></span>
### 3.1 Create a hybrid row\-column storage table


1. Enable the FE configuration item `enable_experimental_rowstore`.


```sql
ADMIN SET FRONTEND CONFIG ("enable_experimental_rowstore" = "true");
```



2. When creating a table, configure `PROPERTIES` with `"STORE_TYPE" = "column_with_row"`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Must be a primary key model table.</div>


* <div data-tips="true" data-tips-type="tip">The length of the <code>__row</code> column must not exceed 1 MB.</div>


* <div data-tips="true" data-tips-type="tip">Starting from version 3.2.4, column types now support BITMAP, HLL, JSON, ARRAY, MAP, and STRUCT.</div>


* <div data-tips="true" data-tips-type="tip">The table must contain additional columns besides the primary key column.</div>



```sql
CREATE TABLE users (
  id bigint not null,
  country string,
  city string,
  revenue bigint
)
PRIMARY KEY (id)
DISTRIBUTED BY HASH(id)
PROPERTIES ("storage_type" = "column_with_row");
```


<span id="_3-2-增删改数据"></span>
### 3.2 Insert, delete, and update data

As with columnar tables, you can add, delete, and modify data in hybrid row\-column tables using data import and DML statements. This section demonstrates using DML statements with the above hybrid row\-column table.


1. Insert data.


```sql
INSERT INTO users (id, country, city, revenue)
VALUES 
(1, 'USA', 'New York', 5000),
(2, 'UK', 'London', 4500),
(3, 'France', 'Paris', 6000),
(4, 'Germany', 'Berlin', 4000),
(5, 'Japan', 'Tokyo', 7000),
(6, 'Australia', 'Sydney', 7500);
```



1. Delete a row of data.


```sql
DELETE FROM users WHERE id = 6;
```



1. Update a row of data.


```sql
UPDATE users SET revenue = 6500 WHERE id = 4;
```


<span id="_3-3-查询数据"></span>
### 3.3 Query data

Here, a point query is used as an example. Point queries use the short path, that is, they directly query data stored by row, which can improve query performance.

The demonstration continues to use the above hybrid row\-column table. After the above table creation and data modification operations, the table should contain the following data:

```sql
MySQL [example_db] SELECT * FROM users ORDER BY id;
+------+---------+----------+---------+
| id   | country | city     | revenue |
+------+---------+----------+---------+
|    1 | USA     | New York |    5000 |
|    2 | UK      | London   |    4500 |
|    3 | France  | Paris    |    6000 |
|    4 | Germany | Berlin   |    6500 |
|    5 | Japan   | Tokyo    |    7000 |
+------+---------+----------+---------+
5 rows in set (0.03 sec)
```
