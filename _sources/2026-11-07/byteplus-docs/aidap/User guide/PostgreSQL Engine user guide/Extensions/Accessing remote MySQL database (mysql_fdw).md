---
title: "Accessing remote MySQL database (mysql_fdw)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-mysql_fdw"
---

This topic introduces the Actions to install and Configure the `mysql_fdw` extension plugin to connect and access the remote MySQL database from the PostgreSQL side.

<span id="2Uo72dQ2"></span>
## Background

`mysql_fdw` is an extension plugin based on the PostgreSQL Foreign Data Wrapper mechanism, used to connect and access a remote MySQL database from the PostgreSQL side. After configuration, tables in MySQL can be mapped as foreign tables in PostgreSQL, allowing queries and partial write operations to be performed almost like local tables.

In terms of capability boundaries, `mysql_fdw` supports basic `SELECT` as well as `INSERT`, `UPDATE`, `DELETE` operations. It also supports pushing down condition filtering, column pruning, JOIN, aggregation, sorting, and `LIMIT/OFFSET` to the MySQL side for execution when conditions are met, reducing data transfer and PostgreSQL local computing overhead.


<columns>
<columnsItem zoneid="nIEceX3Pkn">

**SERVER**

Define the remote MySQL address, port, and connection\-level options.

</columnsItem>
<columnsItem zoneid="wLnWh5L1xv">

**USER MAPPING**

Define the authentication method used by PostgreSQL users to access remote MySQL

</columnsItem>
<columnsItem zoneid="MrvGcUum1R">

**FOREIGN TABLE**

Defines the mapping relationship between the PostgreSQL table structure and the remote MySQL table.

</columnsItem>
</columns>


The following table summarizes the main capabilities and applicable boundaries of `mysql_fdw`:


|**capability** |**Supported or not** |**Decscription** |
|---|---|---|
|Basic read and write |Support |Support executing `SELECT`, `INSERT`, `UPDATE`, `DELETE` on external tables. |
|WHERE condition pushdown |Support |When expressions meet pushdown requirements, try to complete filtering on the MySQL side. |
|Column pruning |Support |Only return fields required by the query to reduce network transmission. |
|join pushdown |Partial support |Pushdown JOINs are supported between external tables on the same remote MySQL server, mainly supporting `inner`, `left`, and `right outer join`, but not `full outer`, `semi`, or `anti`. |
|aggregation pushdown |Partial support |Currently only `MIN()`, `MAX()`, `SUM()`, `AVG()`, and `COUNT()` can be pushed down within the safety range; `FILTER` and `ORDER BY` on aggregation are not pushed down. |
|order by pushdown |Support |pushdown sorting is supported, but note that MySQL and PostgreSQL have different `null` sorting behavior. |
|`Limit/offset` pushdown |Partial support |Supports pushing down `LIMIT` / `OFFSET`; however, MySQL does not support `OFFSET` without `LIMIT`, so such SQL may not be pushdown capable. |
|`TRUNCATE` |Conditional support |available in PostgreSQL 14 and later; `truncate ...` is not supported `cascade`, `restart identity` / `continue identity` are ignored and cannot be executed if there are foreign key references on the remote side. |


<span id="lQLH8bh2"></span>
## Prerequisites

Before starting configuration, ensure the following items are confirmed:


1. The PostgreSQL instance already meets the conditions to use the `mysql_fdw` extension and has permission to `execute CREATE EXTENSION`.

2. The network link from the host running PostgreSQL to the target MySQL instance is reachable, including routing, ACL, security groups, DNS, and others are all enabled.

3. The remote MySQL account is prepared, and it is recommended to create a dedicated account using the **least privilege** principle.

4. The target database's character set, port, authentication method, and whether SSL/TLS needs to be enabled have been confirmed.

5. If `TRUNCATE` is required, confirm that the PostgreSQL version is 14 or higher and that the remote table has no foreign key constraints.

6. For more accurate optimizer estimation, consider enabling `use_remote_estimate`, which means PostgreSQL will additionally send `EXPLAIN` requests to MySQL.


<div data-tips="true" data-tips-type="warning">Remote authentication information is saved in <code>USER MAPPING</code>. In production, it is recommended to use a separate low\-privilege account and prioritize enabling parameters such as <code>ssl_key</code>, <code>ssl_cert</code>, and <code>ssl_ca</code> to establish encrypted connections when conditions allow.</div>


<span id="BAAQ6oLT"></span>
## Install extension

If the `mysql_fdw` extension files are already deployed in the instance environment, the extension can be enabled directly in the target database:

```SQL
CREATE EXTENSION mysql_fdw;
```


If you need to disable this extension, execute:

```SQL
DROP EXTENSION mysql_fdw;
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The provided material mainly covers the extension enabling and usage methods and does not include binary installation steps for different operating systems or PostgreSQL distributions. If the current instance fails to execute <code>CREATE EXTENSION mysql_fdw;</code>, it usually means the extension component is not yet installed on the instance side. You need to complete the environment installation first or contact the instance administrator.</div>


<span id="ltS1e59Y"></span>
## Configuration item

After enabling the extension, the usual configuration sequence is "create external server → create user mapping → create external table."


1. ### Create external server <span id="RG8ZAcKa"></span>


```SQL
CREATE SERVER mysql_server
FOREIGN DATA WRAPPER mysql_fdw
OPTIONS (
  host '127.0.0.1',
  port '3306',
  character_set 'auto',
  fetch_size '100',
  use_remote_estimate 'false',
  sql_mode 'ANSI_QUOTES',
  reconnect 'false'
);
```


Common `SERVER`\-level parameters are as follows:


|**Name** |**Default value** |**Scope** |**Decscription** |
|---|---|---|---|
|`host` |`127.0.0.1` |SERVER |target MySQL address. |
|`port` |`3306` |SERVER |target MySQL port. |
|`fetch_size` |`100` |SERVER / TABLE |number of rows fetched from remote each time; table\-level can override this parameter. |
|`use_remote_estimate` |`false` |SERVER |Whether to execute `EXPLAIN` on the remote to obtain cost estimation to assist PostgreSQL optimizer in execution plan selection |
|`sql_mode` |`ANSI_QUOTES` |SERVER |Set MySQL’s `sql_mode` after connection is established. |
|`character_set` |`auto` |SERVER |connect character set, can be set to `auto`, `PGDatabaseEncoding`, or specify a character set. |
|`ssl_key / ssl_cert / ssl_ca / ssl_capath / ssl_cipher` |Empty |SERVER |used to configure SSL/TLS encrypted connections. |
|`reconnect` |`false` |SERVER |Whether to reconnect automatically after remote connection is lost |
|`truncatable` |`true` |SERVER / TABLE |Allow executing `TRUNCATE` on external tables, may be overridden at table level. |



2. ### Create user mapping <span id="k7h7HrhZ"></span>


```SQL
CREATE USER MAPPING FOR CURRENT_USER
SERVER mysql_server
OPTIONS (
  username 'fdw_user',
  password 'your_mysql_password'
);
```


`USER MAPPING` defines the authentication information used by PostgreSQL users to access remote MySQL. It is not recommended to directly reuse high\-privilege accounts in the production environment. It is advised to create a minimal permission account separately for federated access.


3. ### Create external table <span id="h6D0io5E"></span>


```SQL
CREATE FOREIGN TABLE mysql_orders_fdw (
  id bigint,
  name text,
  created_at timestamp
)
SERVER mysql_server
OPTIONS (
  dbname 'app_db',
  table_name 'orders',
  fetch_size '1000'
);
```


When creating an external table, the column structure defined on the PostgreSQL side should be kept as consistent as possible with the remote MySQL table. Otherwise, it may cause type conversion failure, precision loss, or abnormal query results.

Common table\-level parameters are as follows:


|**Name** |**Default value** |**Decscription** |
|---|---|---|
|`dbname` |Null |The remote MySQL database name. |
|`table_name` |Null |remote MySQL table name. |
|`fetch_size` |inherit server value |Override the server\-level batch fetch row settings. |
|`max_blob_size` |Null |Used to limit the pull size of large fields, suitable for performance control in large object scenarios. |
|`truncatable` |inherit server value |Independently control whether `truncate` is allowed on this external table. |



---



<span id="0GQxe6Se"></span>
## Use (provide specific command examples)

The following is a complete example process from connection configuration to accessing a remote table.

<span id="u6M3npU8"></span>
### Example 1: Query a remote MySQL table

```SQL
SELECT id, name, created_at
FROM mysql_orders_fdw
WHERE id < 100
ORDER BY created_at DESC
LIMIT 10;
```


If queries involve filtering, sorting, limiting the number of returned rows, etc., `mysql_fdw` will push down these operations to the MySQL side for execution when possible.

<span id="H2LEPfKa"></span>
### Example 2: Execute write operations on the external table

```SQL
INSERT INTO mysql_orders_fdw (id, name, created_at)
VALUES (1001, 'demo', now());

UPDATE mysql_orders_fdw
SET name = 'demo_v2'
WHERE id = 1001;

DELETE FROM mysql_orders_fdw
WHERE id = 1001;
```


Although `mysql_fdw` supports writing, it is still recommended to verify that field mappings, default values, triggers, generated columns, and constraint behaviors meet expectations before production use.

<span id="XaG2jREk"></span>
### Example 3: Checking plugin version and pushdown configuration

```SQL
SELECT mysql_fdw_version();
SELECT mysql_fdw_display_pushdown_list();
```


Among them:


* `mysql_fdw_version()` returns the current `mysql_fdw` version number.

* `mysql_fdw_display_pushdown_list()` shows the pushdown configurations in `mysql_fdw_pushdown.config`, useful for troubleshooting why a particular expression is not pushed down.


<span id="txGo3lsx"></span>
### Example 4: Verifying whether SQL is pushed down

```SQL
EXPLAIN
SELECT id, name
FROM mysql_orders_fdw
WHERE id BETWEEN 1 AND 100
ORDER BY id
LIMIT 20;
```


If the actual execution plan differs from expectations, first check:


1. Whether the SQL uses aggregates, expressions, or JOIN types unsupported for pushdown.

2. Whether there is an `OFFSET` without a `LIMIT` in the syntax.

3. Whether sorting semantics are affected by differences in `NULL` handling.

4. Check whether to further verify pushdown capability combined with `mysql_fdw_display_pushdown_list()`


<span id="JCat2kNW"></span>
## FAQs and troubleshooting


|**Problem appearance** |**Possible reasons** |**Trouble shooting suggestions** |
|---|---|---|
|Connection failed when executing query or creating table |PostgreSQL cannot connect to MySQL network or incorrect configuration of `host`, `port`, DNS, ACL, or security group |First verify network connectivity in the PostgreSQL environment, then check the connection address, port, and access control policy. |
|The query result sorting does not match the expectation |MySQL and PostgreSQL have different `null` sorting rules. |Avoid relying on implicit sorting results; for key query scenarios, redesign sorting conditions according to business semantics and focus on verifying result sets containing `NULL` data |
|Aggregation or pagination without pushdown results in significant performance degradation |The SQL uses aggregation forms, expressions, or `offset` usage currently unsupported for pushdown. |Prioritize rewriting SQL to forms like `MIN/MAX/SUM/AVG/COUNT` that can be pushed down; avoid using only `OFFSET` in pagination scenarios; check `mysql_fdw_display_pushdown_list()` if necessary. |
|`Truncate` execution failed |PostgreSQL versions below 14, foreign key references exist on the target table, or table\-level/service\-level `truncatable` is disabled. |confirm PostgreSQL version, foreign key relationships, and `truncatable` configuration; switch to `delete` method if conditions are not met. |
|Slow large field queries or high memory usage |Usage of `SELECT *` or unreasonable `fetch_size` setting, or remote contains large fields such as BLOB/TEXT |Query only required columns, optimize `fetch_size`, and control large field reading scale with `max_blob_size` according to the scenario. |
|The write result is inconsistent with the expectation |The remote side has generated columns, triggers, default values, or type mapping differences. |Perform joint debugging verification ahead of write scenarios, focusing on generated columns, time types, precision fields, and constraint handling logic. |
|authentication or security risk concerns |Remote account password is saved in `user mapping`, and the connection might be unencrypted. |Use a low\-privilege dedicated account, and prioritize configuring `ssl_*` related parameters to establish an encrypted connection when the environment allows. |


For more implementation details and capability boundaries, refer to [mysql_fdw upstream README](https://github.com/EnterpriseDB/mysql_fdw/blob/master/README.md).
