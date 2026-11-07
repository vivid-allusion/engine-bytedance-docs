---
title: "Security rule management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Security_rule_management"
---

This topic describes how to manage security rules on the Database Workshop (DBW) console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Security control refers to the rules and measures established to protect data and resources in the database system. This feature enables you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. For more information, refer to [management](https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management)[management](https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management)[management](https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Your account has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* You have created a security rule set. For detailed steps, refer to [Creating a security rule set](https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only SQL statements executed in the SQL window of the data interaction platform or via tickets will be intercepted and take effect.

* Ensure that no conflicts exist among the security rules enabled in the security rule set. Otherwise, the security rules bound to your instance may become invalid.

* The system provides a default security rule set named `vedb_mysql default`. For details on the default security rules included in the default rule set and newly created rule sets, refer to [References](https://docs.byteplus.com/en/docs/DBW/Security_rule_management#.5Y-C6ICD5paH5qGj).

* A base rule can consist of multiple sub\-rules, which are executed sequentially.

* System rules can not be deleted or modified, only enabled or disabled. Custom security rules can not be restored once deleted. Proceed with caution.

* Custom SQL review security rules are currently not supported. For details on the system\-provided SQL review rules, refer to [References](https://docs.byteplus.com/en/docs/DBW/Security_rule_management#.5Y-C6ICD5paH5qGj).


<span id=".5Yib5bu65a6J5YWo6KeE5YiZ"></span>
## Create a security rule


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **View** in the **Actions** column of the target security rule set.

5. On the target security rule page, click **Create rule**.

6. In the **Create security rule**control panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Rule name** |Custom security rule name. The security rule name can not exceed 128 characters, and can not be empty. |
   |**Effective scenario** |Select the effective scenario for the security rule from the drop\-down list, supporting **Data interaction platform**, **Ticket management** and **SQL review**. |
   |**Basic rules** |A base rule can consist of multiple sub\-rules, which are executed sequentially. The specific configuration of the basic rules is as follows:<br><br><br>* You can set security rules based on **Factor**, **Fixed value \- Character**, **Fixed value \- Numeric**, **Fixed value \- Boolean**.<br><br>* When the base rule is satisfied, you can set whether to allow the SQL type to be executed in the data interaction platform or generate a ticket for execution for each sub\-rule. The settings vary depending on the effective scenario, as follows:<br><br>   * When **Effective scenario** selects **Data interaction platform**, you can choose **Prohibit the execution of this SQL type in the data interaction platform**, **Allow the execution of this SQL type in the data interaction platform**, or **Prohibit the execution of this SQL type in the data interaction platform and redirect to ticket execution**.<br><br>   * When **Effective scenario** selects **Ticket management**, you can choose **Prohibit the execution of this SQL type in ticket**, **Allow the execution of this SQL type in ticket**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can add an unlimited number of sub\-rules</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each subrule can contain up to three levels of conditions.</div><br> |
   |**Default rule** |Enable default rules as needed. When enabled, execute the default rule if none of the sub\-rules included in the basic rules are triggered. The setting varies depending on the effective scenario, as follows:<br><br><br>* When **Effective scenario** selects **Data interaction platform**, you can choose **Prohibit the execution of this SQL type in the data interaction platform**, **Allow the execution of this SQL type in the data interaction platform, or Prohibit the execution of this SQL type in the data interaction platform and redirect to ticket execution.** <br><br>* When **Effective scenario** selects **Ticket management**, you can choose **Prohibit the execution of this SQL type in ticket**, **Allow the execution of this SQL type in ticket**. |
   |**Rule preview** |This area displays the SQL statements generated by the rules you set, which you do not need to modify. |
   


<span id=".5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ"></span>
## Enable or disable a security rule

You can enable or disable rules within a security rule set as required.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **View** in the **Actions** column of the target security rule set.

5. On the target security rule set page, click the switch in the **Enable or not?**  column of the target rule.

6. In **Confirm enable?**  Or **Confirm close?**  dialog box, click **OK**.


<span id=".57yW6L6R5a6J5YWo6KeE5YiZ"></span>
## Edit a security rule

System rules can not be modified. Only custom security rules can be edited.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **View** in the **Actions** column of the target security rule set.

5. On the target security rule set page, click **Edit** in the **Actions** column of the target rule.

6. In the **Edit configuration item**dialog box, modify security rules.


<span id=".5Yig6Zmk5a6J5YWo6KeE5YiZ"></span>
## Delete a security rule

System rules can not be deleted. Custom security rules can not be restored once deleted. Proceed with caution.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **View** in the **Actions** column of the target security rule set.

5. On the target security rule set page, click **Delete** in the **Actions** column of the target rule.

6. In the **Confirm deletion** dialog box, click **OK**.


<span id=".5Y-C6ICD5paH5qGj"></span>
## References

The default security rules (system rules) in the security rule set are shown in the table below.


* Data interaction platform & Ticket management



|**Security rule name** |**Effective scenario** |**Enable by default?**  |**Default value** |
|---|---|---|---|
|Prohibit direct execution of `CREATE_TABLE` in the database interaction platform. Submit a ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `DROP_TABLE` in the database interaction platform. Submit a ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `TRUNCATE` in the database interaction platform. Submit a DDL ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `INSERT` in the database interaction platform. Submit a DML ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `UPDATE` on the SQL console. Submit a DML ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `DELETE` on the SQL console. Submit a DML ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `ALTER_TABLE` in the database interaction platform. Submit a DDL ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `KILL` in the database interaction platform. Submit a DML ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit the direct creation of stored procedures on the database interaction platform. Submit a DDL ticket for execution. |Data interaction platform |Enabled |None |
|Prohibit the execution of unrecognized SQL parsing exceptions [Continuing execution will cause security rules to fail]. |Data interaction platform |Enabled |None |
|Prohibit SQL with unresolved permissions from continuing execution [Continuing execution will cause security rules to fail]. |Data interaction platform |Enabled |None |
|All users need to check permissions. |Data interaction platform |Enabled |None |
|Only certain types of SQL execution are supported. |Data interaction platform |Not enabled |SHOW TABLES, SHOW CREATE TABLE, EXPLAIN, SELECT, DBATMAN HELP, DBATMAN SHOW |
|Only supports SQL execution where `select_type` is within the range. |Data interaction platform |Not enabled |SIMPLE, PRIMARY, DERIVED, UNION, UNION RESULT, SUBQUERY, DEPENDENT SUBQUERY, MATERIALIZED, DEPENDENT UNION |
|Only supports SQL execution where `index_type` is within the range. |Data interaction platform |Not enabled |index, range, ref, eq_ref, const, system, NULL |
|Only SQL statements scanning fewer than 100,000 rows are supported. Optimize the SQL statement. |Data interaction platform |Not enabled |100,000 |
|`SELECT` statements recommend specifying a WHERE condition. |Data interaction platform |Not enabled |None |
|A table must have a primary key. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Tables must have remarks. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Tables can not use foreign keys. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Restrict table name case sensitivity. |* Ticket management<br><br>* Data interaction platform |Not enabled |* Lower<br><br>* upper |
|Limit the table storage engine.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |InnoDB |
|Limit tables to partition settings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule is not restricted during <code>CreateTable </code>and <code>AlterTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|The table must contain certain columns.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Limit the table character set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |utf8mb4 |
|Limit table validation rules.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |utf8_general_ci, utf8_bin, utf8mb4_general_ci, utf8mb4_bin |
|Table names can not be keywords. |* Ticket management<br><br>* Data interaction platform |Not enabled |analyze, add, all, alter, and, before, between, bigint, binary, blob, both, by, call, cascade, case, change, char, character, check, collate, column, condition, as, asc, asensitive, connection, constraint, continue, convert, create, cross, current_date, current_time, current_timestamp, current_user, cursor, database, databases, day_hour, day_microsecond, day_minute, day_second, dec, decimal, declare, default, delayed, delete, desc, describe, deterministic, distinct, distinctrow, div, double, drop, dual, each, else, exit, explain, false, fetch, float, float4, float8, elseif, enclosed, escaped, exists, for, force, foreign, from, fulltext, goto, grant, group, having, high_priority, hour_microsecond, hour_minute, hour_second, if, ignore, in, index, infile, inner, inout, insensitive, insert, int, int1, int2, int3, int4, int8, integer, interval, into, is, iterate, join, key, keys, kill, label, leading, leave, left, like, limit, linear, lines, low_priority, localtime, localtimestamp, lock, long, longblob, longtext, loop, load, matchediumblob, mediumint, mediumtext, middleint, minute_microsecond, minute_second, mod, modifies, no_write_to_binlog, null, numeric, on, optimize, option, optionally, natural, not, or, order, ut, uter, outfile, precision, primary, procedure, urge, raid0, ange, read, reads, eal, references, regexp, release, ename, epeat, replace, require, restrict, return, evoke, ight, rlike, schema, schemas, second_microsecond, select, sensitive, separator, set, show, smallint, spatial, specific, sql, sqlexception, sqlstate, sqlwarning, sql_big_result, sql_calc_found_rows, sql_small_result, ssl, starting, traight_join, able, terminated, then, tinyblob, inyint, tinytext, o, trailing, trigger, true, ndo, union, unique, nlock, unsigned, pdate, usage, use, using, utc_date, tc_time, tc_timestamp, values, varbinary, x509, xor, year_month, zerofill, varchar, varcharacter, varying, when, where, while, with, write |
|Limit the number of table indexes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |7 |
|Limit the number of table fields.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |128 |
|Restrict the initial value of table auto\-increment. |* Ticket management<br><br>* Data interaction platform |Not enabled |1 |
|Restricts the primary key column to auto\-increment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Field names can not be keywords. |* Ticket management<br><br>* Data interaction platform |Not enabled |analyze, add, all, alter, and, before, between, bigint, binary, blob, both, by, call, cascade, case, change, char, character, check, collate, column, condition, as, asc, asensitive, connection, constraint, continue, convert, create, cross, current_date, current_time, current_timestamp, current_user, cursor, database, databases, day_hour, day_microsecond, day_minute, day_second, dec, decimal, declare, default, delayed, delete, desc, describe, deterministic, distinct, distinctrow, div, double, drop, dual, each, else, exit, explain, false, fetch, float, float4, float8, elseif, enclosed, escaped, exists, for, force, foreign, from, fulltext, goto, grant, group, having, high_priority, hour_microsecond, hour_minute, hour_second, if, ignore, in, index, infile, inner, inout, insensitive, insert, int, int1, int2, int3, int4, int8, integer, interval, into, is, iterate, join, key, keys, kill, label, leading, leave, left, like, limit, linear, lines, low_priority, localtime, localtimestamp, lock, long, longblob, longtext, loop, load, match, mediumblob, mediumint, mediumtext, middleint, minute_microsecond, minute_second, mod, modifies, no_write_to_binlog, null, numeric, on, optimize, option, optionally, natural, not, or, order, out, outer, outfile, precision, primary, procedure, purge, raid0, range, read, reads, real, references, regexp, release, rename, repeat, replace, require, restrict, return, revoke, right, rlike, schema, schemas, second_microsecond, select, sensitive, separator, set, show, smallint, spatial, specific, sql, sqlexception, sqlstate, sqlwarning, sql_big_result, sql_calc_found_rows, sql_small_result, ssl, starting, straight_join, table, terminated, then, tinyblob, tinyint, tinytext, to, trailing, trigger, true, undo, union, unique, unlock, unsigned, update, usage, use, using, utc_date, utc_time, utc_timestamp, values, varbinary, x509, xor, year_month, zerofill, varchar, varcharacter, varying, when, where, while, with, write |
|Restrict field name case sensitivity. |* Ticket management<br><br>* Data interaction platform |Not enabled |* lower<br><br>* upper |
|Can not set the character set of a column. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Columns must have comments. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Limit the length of `CHAR` type fields. |* Ticket management<br><br>* Data interaction platform |Not enabled |256 |
|Limit the length of `VARCHAR` type fields. |* Ticket management<br><br>* Data interaction platform |Not enabled |2,560 |
|All restricted columns must not be null (`not null`). |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Restrict the auto\-increment column name to ID. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Limit the auto\-increment column to unsigned. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Can not use `float/double `type. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Each column must have a default value. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Cannot set the validation set for columns. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|The ENUM type can not be used (`tinyint/char `is recommended instead). |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|The field is not enabled with the `Zerofill` attribute. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Index requires a name. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Restrict the format of `Unique` index names. |* Ticket management<br><br>* Data interaction platform |Not enabled |uk_\w+ |
|Restrict the format of normal index names. |* Ticket management<br><br>* Data interaction platform |Not enabled |idx_\w+ |
|Limit the number of columns included in a single index. |* Ticket management<br><br>* Data interaction platform |Not enabled |5 |
|Limit the number of columns included in a primary key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |2 |
|Limit the primary key column type. |* Ticket management<br><br>* Data interaction platform |Not enabled |int, bigint |
|Restricted columns can not use certain data types. |* Ticket management<br><br>* Data interaction platform |Not enabled |None |
|Fields in the index are required to be set to `not n "ull`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule only applies during <code>CreateTable</code>.</div><br> |* Ticket management<br><br>* Data interaction platform |Not enabled |None |



* SQL review



|**Security rule name** |**Enable by default?**  |**Level** |Default value |
|---|---|---|---|
|SQL syntax parsing error, check if the SQL statement is valid. |Enabled |* Low: recommendation.<br><br>* Medium: warning.<br><br>* High: (default) red line. |None |
|The SELECT statement recommends specifying a WHERE condition. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Limit the number of tables involved in UPDATE/DELETE statements |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |5 |
|UPDATE/DELETE statements detect if multi\-table join syntax is complete (missing ON clause in JOIN). |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|The UPDATE/DELETE statement recommends specifying a WHERE condition. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Field names in INSERT statements can not be duplicated. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|The field list and value list in the INSERT statement must match |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|The INSERT statement recommends specifying an INSERT field list. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|INSERT statements can not insert `NULL` values for `NOT NULL `columns. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|INSERT statements are not recommended to use `SYSDATE()` functions. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Limit total rows per `INSERT VALUES `clause in an INSERT statement. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |1,000 |
|INSERT statement checks if the table/field in `INSERT` exists. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|When performing UPDATE on multiple tables, check if the columns in SET specify the table prefix. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|UPDATE statements are not recommended to update the "creation time" column of the table. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |* create _time<br><br>* create_at |
|UPDATE statements are recommended to update the "modification time" column of the table. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |* update_time<br><br>* modify_time<br><br>* update_at<br><br>* modify_at |
|UPDATE statement detects the separator between multiple columns in the SET clause (AND is invalid). |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|UPDATE/DELETE statements check if the WHERE condition contains a subquery. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Limit the number of elements in the IN clause of a WHERE condition. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|UPDATE statement checks if the primary key is updated. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|UPDATE statement checks if the table/field in UPDATE exists. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|The UPDATE statement detects if the unique key is updated. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Limit the SELECT statement LIMIT size for `OFFSET`. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |2,000 |
|`GROUP BY` constants are not recommended for SELECT. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Limit the number of tables involved in SELECT statements |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |3 |
|SELECT statements are not recommended to use `*`. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|The SELECT statements are not recommended to use `GROUP BY` or `ORDER BY` on different tables. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `ORDER BY` on constants. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `ORDER BY` with multiple fields in different sorting directions. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `GROUP BY` expressions or functions. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `ORDER BY` expressions or functions. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `ORDER BY RAND()`. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `HAVING` clause. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|SELECT statements are not recommended to use `UNION`. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|WHERE conditions are not recommended to use leading wildcards for searches. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|Reverse queries (`NOT IN / NOT LIKE`) are not recommended in the WHERE condition. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|WHERE condition detects whether filtering conditions are connected via the OR operator. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
|WHERE condition detected a LIKE statement without wildcards. |Not enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |


&nbsp;

<span id=".55u45YWz5pON5L2c"></span>
## Related operation

[Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control): When enabling security control for an instance, set the security rule set.
