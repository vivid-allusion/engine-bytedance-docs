---
title: "List of reserved keywords"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords"
---

This topic summarizes reserved keywords in database name, account name, and schema name for RDS for PostgreSQL. These keywords cannot be used when naming a database, account, or schema.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only lowercase keywords are verified; keywords in all uppercase or mixed uppercase are allowed.</div>



|Reserved objects |Keywords |
|---|---|
|Account name, database name, and schema name |`all`，`analyse`，`analyze`，`and`，`any`，`array`，`as`，`asc`，`asymmetric`，`authorization`，`binary`，`both`，`case`，`cast`，`check`，`collate`，`collation`，`column`，`concurrently`，`constraint`，`create`，`cross`，`current_catalog`，`current_date`，`current_role`，`current_schema`，`current_time`，`current_timestamp`，`current_user`，`default`，`deferrable`，`desc`，`distinct`，`do`，`else`，`end`，`except`，`false`，`fetch`，`for`，`foreign`，`freeze`，`from`，`full`，`grant`，`group`，`having`，`ilike`，`in`，`initially`，`inner`，`intersect`，`into`，`is`，`isnull`，`join`，`lateral`，`leading`，`left`，`like`，`limit`，`localtime`，`localtimestamp`，`natural`，`not`，`notnull`，`null`，`offset`，`on`，`only`，`or`，`order`，`outer`，`overlaps`，`placing`，`primary`，`references`，`returning`，`right`，`select`，`session_user`，`similar`，`some`，`symmetric`，`table`，`tablesample`，`then`，`to`，`trailing`，`true`，`union`，`unique`，`user`，`using`，`variadic`，`verbose`，`when`，`where`，`window`，`with` |
|Account name |`byte_rds_proxy`，`byte_rds_repl`，`ccp_monitoring`，`dbw_admin`，`mpp_op_account`，`postgres`，`primaryuser`，`rds_shard` |
|Database name |`byte_mppdb`，`information_schema`，`postgres`，`template0`，`template1` |
|Schema name |`columnar`，`columnar_internal`，`information_schema`，`pg_catalog` |
