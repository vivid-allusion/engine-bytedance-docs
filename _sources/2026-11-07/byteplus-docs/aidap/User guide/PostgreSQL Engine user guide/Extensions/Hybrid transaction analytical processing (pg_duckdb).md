---
title: "Hybrid transaction analytical processing (pg_duckdb)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_duckdb"
---

The pg_duckdb extension integrates the high\-performance DuckDB analytics engine into PostgreSQL, enabling high\-speed analytical queries on relational data and files in formats such as Parquet and CSV stored in object storage like TOS within the current database environment, and delivering HTAP capabilities.

With this extension, you can **accelerate real\-time analysis**. For complex aggregate queries on large\-scale tables, it delivers dozens to hundreds of times performance gains via DuckDB's columnar vectorized engine, eliminating the need to ETL data into dedicated analytical databases.

**Scope**

Workspaces using the PostgreSQL engine created after April 20, 2026.

<span id="IYirJF1l"></span>
## Install and enable

Enabling the pg_duckdb extension involves two core steps: creating a workspace with AP acceleration enabled and having the database owner (DB Owner) create the extension in the database.


1. **Create a workspace with AP acceleration enabled**: create a workspace with AP acceleration enabled by calling the [CreateWorkspace](https://docs.byteplus.com/en/docs/aidap/CreateWorkspace) API.

2. **Create the extension by DB Owner**: After instance restart, connect to the target database using an account with database `CREATE` privileges (generally the database owner), and execute the following command to create the extension.


```SQL
CREATE EXTENSION pg_duckdb;
```


Once executed successfully, the pg_duckdb extension is enabled in that database.

<div data-tips="true" data-tips-type="default"><strong>Permission</strong> description</div>


<div data-tips="true" data-tips-type="default"><code>CREATE EXTENSION</code> requires the database <code>CREATE</code> permission, usually restricted to the database owner (DB Owner) or superuser. Normal users cannot perform this operation.</div>


<span id="7vsgL4eN"></span>
## Core functions and operations

After enabling the extension, all users can access its provided functions. The core operations include enforcing queries using the DuckDB engine and accessing external object storage data.

<span id="bPViUoSS"></span>
### Accelerate query using the DuckDB engine

For tables that already exist in PostgreSQL, you can force queries to execute through the DuckDB engine by setting parameters to improve analytical performance.

**Procedure:** 


1. **Set session parameters**: set the following two parameters before executing the query.


```SQL
-- Force subsequent queries to use the DuckDB engine
SET duckdb.force_execution = true;
```



2. **Execute analysis queries**: write your SQL query as usual. For example, perform aggregation statistics by date on the `orders` table.


```SQL
-- Example: query daily order count and total revenue
SELECT
    order_date,
    COUNT(*) AS number_of_orders,
    SUM(amount) AS total_revenue
FROM
    orders
GROUP BY
    order_date
ORDER BY
    order_date;
```



3. **Verifying execution plan**: you can use the `EXPLAIN` command to confirm whether the query is executed by the DuckDB engine.


```SQL
EXPLAIN SELECT COUNT(*) FROM your_large_table;
```


If the returned execution plan contains `Custom Scan (DuckDBScan)` and `DuckDB Execution Plan`, it indicates the query has been successfully handled by DuckDB.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">何时使用<strong><code>duckdb.force_execution</code></strong><strong>?</strong></div>



* <div data-tips="true" data-tips-type="default">When your query mainly involves complex aggregations, multi\-table joins, or other analysis (AP) operations, enable this option for optimal performance.</div>


* <div data-tips="true" data-tips-type="default">For simple point lookups or transactional (TP) operations, there is no need to enable it. Use the native PostgreSQL engine instead.</div>


* <div data-tips="true" data-tips-type="default">This parameter only takes effect during the current session and is invalid after the session is closed.</div>



<span id="mPzGmxFH"></span>
### Create DuckDB columnar tables

You can create **temporary tables** managed by the DuckDB engine in PostgreSQL. These tables use columnar storage, ideal for temporary, high\-performance data analysis.

```SQL
-- Create a temporary columnar table managed by DuckDB
CREATE TEMP TABLE orders_columnstore (
    id BIGINT,
    item TEXT,
    price NUMERIC(10, 2),
    order_date DATE
) USING duckdb;

-- Data can be inserted into this table later for efficient queries
INSERT INTO orders_columnstore VALUES (1, 'widget', 19.99, '2026-04-20');

SELECT * FROM orders_columnstore;
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, USING duckdb syntax only supports creating TEMP (temporary) tables.</div>


<span id="MgjkDcHQ"></span>
### Manage and view

You can use the following command to view all pg_duckdb\-related configuration parameters.

```SQL
SELECT name, setting, short_desc
FROM pg_settings
WHERE name LIKE 'duckdb.%'
ORDER BY name;
```


<span id="R1BURZsO"></span>
### reading data lakes

pg_duckdb supports directly reading external files. Common functions include:


* `read_parquet`

* `read_json`

* `read_csv`


these functions can all use external files as query input sources, suitable for directly querying file data in Object Storage or data lakes.

<span id="YSpUZ5Sw"></span>
#### Basic usage

the return type of these three functions is `setof duckdb.row`.

`path` parameter supports:


* Single path

* path array (`text[]`)

* glob mode


It can read remote files as well as local files. However, reading local files usually requires the instance to have the corresponding permission enabled.

The simplest query method is to directly expand all columns:

```SQL
SELECT * FROM read_parquet('s3://bucket/orders/*.parquet');
```


To reference specific columns, first alias the function result, then access the column via `r['column_name']`:

```SQL
SELECT    r['order_id'],    r['amount']FROM    read_parquet('s3://bucket/orders/*.parquet') rWHERE    r['amount'] > 100;
```


<span id="ESJYW88U"></span>
#### read_parquet

Used to read Parquet files.

Function signature:

```SQL
read_parquet(path TEXT or TEXT[], ...) -> SETOF duckdb.row
```


Sample:

```SQL
SELECT * FROM read_parquet('s3://bucket/data/orders.parquet');SELECT    r['id'],    r['name']FROM    read_parquet('s3://bucket/data/orders.parquet') rWHERE    r['age'] > 21;SELECT    r['file_row_number'],    r['filename']FROM    read_parquet(        's3://bucket/data/iris.parquet',        file_row_number => true,        filename => true    ) r;
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">optional parameters are basically consistent with duckdb native <code>read_parquet</code>.</div>


* <div data-tips="true" data-tips-type="default">Supports reading multiple Parquet files at once through glob.</div>



<span id="mkklCMH7"></span>
#### read_csv

Used for reading CSV files.

Function signature:

```SQL
read_csv(path TEXT or TEXT[], ...) -> SETOF duckdb.row
```


Sample:

```SQL
SELECT * FROM read_csv('s3://bucket/data/orders.csv');SELECT    r['id'],    r['name']FROM    read_csv('s3://bucket/data/orders.csv') rWHERE    r['age'] > 21;SELECT    r['sepal.length'],    r['filename']FROM    read_csv(        's3://bucket/data/iris.csv',        filename => true,        header => true    ) r;
```


> **Decscription**


> * optional parameters are basically consistent with duckdb native `read_csv`.

> * The current `columns` parameter is not supported.

> * `nullstr` must be passed as `TEXT[]`.


<span id="x012c296"></span>
#### read_json

used to read JSON files.

Function signature:

```SQL
read_json(path TEXT or TEXT[], ...) -> SETOF duckdb.row
```


Sample:

```SQL
SELECT * FROM read_json('s3://bucket/data/table.json');SELECT    r['a'],    r['b'],    r['c']FROM    read_json('s3://bucket/data/table.json') rWHERE    r['c'] > 50.4;
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Optional parameters are basically consistent with native DuckDB <code>read_json</code>.</div>


* <div data-tips="true" data-tips-type="default">The current <code>columns</code> parameter is not supported.</div>



<span id="gulYqTlM"></span>
### Instructions


* If specific columns need to be referenced, the read function must be assigned an alias and columns accessed via `r['col']`.

* path supports multiple file paths and wildcard batch file reading.


<span id="HCMg9dH1"></span>
## Permissions and compliance


* **Extension usage permissions**: after installing the pg_duckdb extension, **all users** in the database have permission to connect and use the DuckDB engine to execute queries without additional authorization.

* **External data access**: when accessing external data sources (e.g., TOS, S3) through the extension, data security is ensured by the access credentials (AK/SK) you provide and the underlying cloud service's own IAM policies. The extension itself does not store these credentials and uses them only in the current session. Ensure the credentials you use follow the principle of least privilege.


<span id="HhnIwuED"></span>
## FAQ

**Q1: How to determine if my query was successfully executed by the DuckDB engine?**  A: Add `EXPLAIN` before your SQL query. If the returned execution plan includes `Custom Scan (DuckDBScan)` and `DuckDB Execution Plan`, it means the DuckDB engine is in use. Otherwise, the query is still executed by the native PostgreSQL engine.

**Q2: ** **`CREATE TABLE ...`**  **`USING duckdb`** ** why can it only create temporary tables?**  A: This is the design of the current version. DuckDB tables are mainly for temporary high\-performance analysis, with a data lifecycle tied to the current database session.
