---
title: "List of forbidden keywords"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords"
---

This topic summarizes the reserved database keywords of NDB for MySQL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The super account name supports the use of <code>root</code> and <code>admin</code>.</div>



|Parameter |Keyword description |
|---|---|
|Only `UserName` |`mysql.infoschema`、`mysql.session`、`mysql.sys`、`internal_admin_user`、`dbw_admin` |
|Only `DatabaseName` |`information_schema`、`mysql`、`performance_schema`、`sys`、`ndb_meta_info`、`__bytehtap__`、`innodb_memcache` |
|`UserName` or `DatabaseName` |`accessible`、`add`、`all`、`alter`、`analyze`、`and`、`as`、`asc`、`asensitive` |
||`before`、`between`、`bigint`、`binary`、`blob`、`both`、`by` |
||`call`、`cascade`、`case`、`change`、`char`、`character`、`check`、`collate`、`column`、`condition`、`constraint`、`continue`、`convert`、`create`、`cross`、`cube`（Only MySQL 8.0）、`current_date`、`current_time`、`current_timestamp`、`current_user`、`cursor`、`current_role` |
||`database`、`databases`、`day_hour`、`day_microsecond`、`day_minute`、`day_second`、`dec`、`decimal`、`declare`、`default`、`delayed`、`delete`、`desc`、`describe`、`deterministic`、`distinct`、`distinctrow`、`div`、`double`、`drop`、`dual`、`dumpfile` |
||`each`、`else`、`elseif`、`enclosed`、`escaped`、`exists`、`exit`、`explain` |
||`false`、`fetch`、`float`、`float4`、`float8`、`for`、`force`、`foreign`、`from`、`fulltext`、`function`（Only MySQL 8.0） |
||`generated`、`get`、`grant`、`group` |
||`having`、`high_priority`、`hour_microsecond`、`hour_minute`、`hour_second` |
||`if`、`ignore`、`in`、`index`、`infile`、`inner`、`inout`、`insensitive`、`insert`、`int`、`int1`、`int2`、`int3`、`int4`、`int8`、`integer`、`interval`、`into`、`io_after_gtids`、`io_before_gtids`、`is`、`iterate`、`ilike` |
||`join` |
||`key`、`keys`、`kill` |
||`lag`（Only MySQL 8.0）、`leading`、`leave`、`left`、`like`、`limit`、`linear`、`lines`、`load`、`localtime`、`localtimestamp`、`lock`、`long`、`longblob`、`longtext`、`loop`、`low_priority` |
||`master_bind`、`master_ssl_verify_server_cert`、`match`、`maxvalue`、`mediumblob`、`mediumint`、`mediumtext`、`middleint`、`minute_microsecond`、`minute_second`、`mod`、`modifies` |
||`natural`、`no_write_to_binlog`、`not`、`null`、`numeric` |
||`on`、`optimize`、`optimizer_costs`、`option`、`optionally`、`or`、`order`、`out`、`outer`、`outfile` |
||`partition`、`precision`、`primary`、`procedure`、`purge` |
||`range`、`read`、`read_write`、`reads`、`real`、`references`、`regexp`、`release`、`rename`、`repeat`、`replace`、`require`、`resignal`、`restrict`、`return`、`revoke`、`right`、`rlike`、`row`（Only MySQL 8.0）、`rows`（Only MySQL 8.0） |
||`schema`、`schemas`、`second_microsecond`、`select`、`sensitive`、`separator`、`set`、`show`、`signal`、`smallint`、`spatial`、`specific`、`sql`、`sql_big_result`、`sql_calc_found_rows`、`sql_small_result`、`sqlexception`、`sqlstate`、`sqlwarning`、`ssl`、`starting`、`stored`、`straight_join`、`stats_extended` |
||`table`、`terminated`、`then`、`tinyblob`、`tinyint`、`tinytext`、`to`、`trailing`、`trigger`、`true`、`tablesample`、`tidb_current_tso` |
||`undo`、`union`、`unique`、`unlock`、`unsigned`、`update`、`usage`、`use`、`using`、`utc_date`、`utc_time`、`utc_timestamp` |
||`values`、`varbinary`、`varchar`、`varcharacter`、`varying`、`virtual` |
||`when`、`where`、`while`、`with`、`write` |
||`xor` |
||`year_month` |
||`zerofill` |
