---
title: "Security rule management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/security-rule-management_"
---

This topic describes how to manage security rules on the Database Workshop (DBW) console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Security control refers to the rules and measures established to protect data and resources in the database system. This feature enables you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. For more information, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Your account must be a DBW administrator. If not, add it as a DBW administrator. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* You have created a security rule set. For detailed steps, refer to [Creating a security rule set](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only SQL statements executed in the SQL window of the data interaction platform or via tickets will be intercepted and take effect.

* Ensure that no conflicts exist among the security rules enabled in the security rule set. Otherwise, the security rules bound to your instance may become invalid.

* The system provides a default security rule set named `postgres default`. For details on the default security rules included in the default rule set and newly created rule sets, refer to [References](https://docs.byteplus.com/en/docs/DBW/security-rule-management_#.5Y-C6ICD5paH5qGj).

* System rules do not support deletion and modification, and only support modification and disabling.


<span id=".5p-l55yL5a6J5YWo6KeE5YiZ"></span>
## View security rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the top menu bar of the **Security rule set** page, select **Database type** as **RDS for PostgreSQL**.

5. Click **View** in the **Actions** column of the target security rule set.

6. On the target security rule set details page, you can view the following information:

   * View information about the security rule set, including the **Security rule set ID**, **Rule set type**, and **Number of associated instances**.

   * View security rule information, including **Data interaction platform**, **Ticket management**, and **SQL review** types. You can also view the **Security rule ID**, **Security rule name**, **Rule type**, **Enable or not?** , **Last modified time** for each security rule.


<span id=".5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ"></span>
## Enable or disable a security rule

You can enable or disable rules within a security rule set as required.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the top menu bar of the **Security rule set** page, select **Database type** as **RDS for PostgreSQL**.

5. Click **View** in the **Actions** column of the target security rule set.

6. On the target security rule set details page, click the switch in the **Enable or not?**  column of the target rule.

7. In **Confirm enable?**  Or **Confirm close?**  dialog box, click **OK**.


<span id=".5Y-C6ICD5paH5qGj"></span>
## References

The default security rules (system rules) in the security rule set are shown in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Interception takes effect only for SQL statements in the SQL window of the data interaction platform, SQL statements executed through tickets, or SQL reviews.</div>



* Data interaction platform

   
   |**Security rule name** |**Enable by default?**  |**Level** |Default value |
   |---|---|---|---|
   |Prohibit direct execution of `ALTER_TABLE` in the database interaction platform. |Enabled |High (red line) |None |
   |Do not execute the `pg_terminate_backend` function directly in the database interaction platform. |Enabled |High (red line) |None |
   |Prohibit direct creation of stored procedures in the database interaction platform. |Enabled |High (red line) |None |
   |Prohibit the execution of unrecognized SQL parsing exceptions [Continuing execution will cause security rules to fail]. |Enabled |High (red line) |None |
   |Prohibit SQL with unresolved permissions from continuing execution [Continuing execution will cause security rules to fail]. |Enabled |High (red line) |None |
   |All users need to check permissions. |Enabled |High (red line) |None |
   |Prohibit direct execution of `CREATE_TABLE` in the database interaction platform. |Enabled |Medium (warning) |None |
   |Prohibit direct execution of `DROP_TABLE` in the database interaction platform. |Enabled |Medium (warning) |None |
   |Forbid direct execution of `INSERT` in the database interaction platform. |Enabled |Medium (warning) |None |
   |Prohibit direct execution of `UPDATE` on the SQL console. |Enabled |High (red line) |None |
   |Prohibit direct execution of `DELETE` on the SQL console. |Enabled |High (red line) |None |
   |Limit the number of tables involved in `UPDATE/DELETE` statements. |Disable |Medium (warning) |5 |
   |`UPDATE/DELETE` statements detect if multi\-table join syntax is complete (missing `ON` clause in `JOIN`). |Disable |Medium (warning) |None |
   |`The UPDATE/DELETE `statement recommends specifying a `WHERE `condition. |Disable |Medium (warning) |None |
   |Field names in `INSERT` statements can not be duplicated. |Disable |Medium (warning) |None |
   |The field list and value list in the `INSERT` statement must match. |Disable |Medium (warning) |None |
   |The `INSERT` statement recommends specifying an `INSERT` field list. |Disable |Medium (warning) |None |
   |`INSERT `statements can not insert `NULL `values for `NOT NULL `columns. |Disable |Medium (warning) |None |
   |`INSERT` statements are not recommended to use `SYSDATE()` functions. |Disable |Medium (warning) |None |
   |Limit the total number of rows per `INSERT VALUES` clause in an `INSERT` statement. |Disable |Medium (warning) |1,000 |
   |`INSERT` statement checks if the table/field in `INSERT` exists. |Disable |Medium (warning) |None |
   |When performing `UPDATE` on multiple tables, check if the columns in `SET` specify the table prefix. |Disable |Medium (warning) |None |
   |`UPDATE` statements are not recommended to update the "creation time" column of the table. |Disable |Medium (warning) |* create_time<br><br>* create_at |
   |`UPDATE` statements are recommended to update the "modification time" column of the table. |Disable |Medium (warning) |update_time,modify_time,update_at,modify_at |
   |`UPDATE` statement detects the separator between multiple columns in the `SET` clause (`AND` is invalid). |Disable |Medium (warning) |None |
   |`UPDATE/DELETE` statements check if the `WHERE` condition contains a subquery. |Disable |Medium (warning) |None |
   |Limit the number of elements in the `IN` clause of a `WHERE` condition. |Disable |Medium (warning) |1,000 |
   |`UPDATE` statement checks if the primary key is updated. |Disable |Medium (warning) |None |
   |`UPDATE` statement checks if the table/field in `UPDATE` exists. |Disable |Medium (warning) |None |
   |`The UPDATE `statement detects if the unique key is updated. |Disable |Medium (warning) |None |
   |Limit the `SELECT` statement `LIMIT` size for `OFFSET`. |Disable |Medium (warning) |2,000 |
   |The `SELECT` statement should contain the `WHERE` condition. |Disable |Medium (warning) |None |
   |`GROUP BY` constants are not recommended for `SELECT`. |Disable |Medium (warning) |None |
   |Limit the number of tables involved in `SELECT` statements |Disable |Medium (warning) |3 |
   |`SELECT` statements are not recommended to use `*`. |Disable |Medium (warning) |None |
   |The `SELECT` statements are not recommended to use `GROUP BY` or `ORDER BY` on different tables. |Disable |Medium (warning) |None |
   |The `SELECT` statements are not recommended to use `ORDER BY` on constants. |Disable |Medium (warning) |None |
   |`SELECT` statements are not recommended to use `ORDER BY` with multiple fields in different sorting directions. |Disable |Medium (warning) |None |
   |`SELECT` statements are not recommended to use `GROUP BY` expressions or functions. |Disable |Medium (warning) |None |
   |`SELECT` statements are not recommended to use `ORDER BY` expressions or functions. |Disable |Medium (warning) |None |
   |`SELECT` statements are not recommended to use `ORDER BY RAND()`. |Disable |Medium (warning) |None |
   |`SELECT` statements are not recommended to use `HAVING` clause. |Disable |Medium (warning) |None |
   |`SELECT` statements are not recommended to use `UNION`. |Disable |Medium (warning) |None |
   |`WHERE `conditions are not recommended to use leading wildcards for searches. |Disable |Medium (warning) |None |
   |Reverse queries (`NOT IN / NOT LIKE`) are not recommended in the `WHERE` condition. |Disable |Medium (warning) |None |
   |`WHERE` condition detects whether filtering conditions are connected via the `OR` operator. |Disable |Medium (warning) |None |
   |`WHERE` condition detected a `LIKE` statement without wildcards. |Disable |Medium (warning) |None |
   

* SQL review

   
   |**Security rule name** |**Enable by default?**  |**Level** |Default value |
   |---|---|---|---|
   |Limit the number of tables involved in `UPDATE/DELETE` statements. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |5 |
   |`UPDATE/DELETE` statements detect if multi\-table join syntax is complete (missing `ON` clause in `JOIN`). |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`The UPDATE/DELETE `statement recommends specifying a `WHERE `condition. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |Field names in `INSERT` statements can not be duplicated. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. | |
   |The field list and value list in the `INSERT` statement must match. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. | |
   |The `INSERT` statement recommends specifying an `INSERT` field list. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. | |
   |`INSERT `statements can not insert `NULL `values for `NOT NULL `columns. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |true |
   |`INSERT` statements are not recommended to use `SYSDATE()` functions. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. | |
   |Limit the total number of rows per `INSERT VALUES` clause in an `INSERT` statement. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |1,000 |
   |`INSERT` statement checks whether the table and field of `INSERT` exist. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`UPDATE` statements are recommended to update the "modification time" column of the table. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |`update_time`、`modify_time`、`update_at`、`modify_at` |
   |`UPDATE` statement detects the separator between multiple columns in the `SET` clause (`AND` is invalid). |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`UPDATE/DELETE` statements check if the `WHERE` condition contains a subquery. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |Limit the number of elements in the `IN` clause of a `WHERE` condition. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |1,000 |
   |`UPDATE` statement checks if the primary key is updated. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |When performing `UPDATE` on multiple tables, check if the columns in `SET` specify the table prefix. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`UPDATE` statements are not recommended to update the "creation time" column of the table. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |`create_time`, `create_at` |
   |`UPDATE` statement checks if the table/field in `UPDATE` exists. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`The UPDATE `statement detects if the unique key is updated. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |SQL syntax parsing error, check if the SQL statement is valid. |Enabled |* Low: recommendation.<br><br>* Medium: warning.<br><br>* High: (default) red line. |None |
   |Limit the `SELECT` statement `LIMIT` size for `OFFSET`. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |2,000 |
   |The `SELECT` statement should contain the `WHERE` condition. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |true |
   |`GROUP BY` constants are not recommended for `SELECT`. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |Limit the number of tables involved in `SELECT` statements |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |3 |
   |`SELECT` statements are not recommended to use `ORDER BY` expressions or functions. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`SELECT` statements are not recommended to use `ORDER BY RAND()`. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`SELECT` statements are not recommended to use `HAVING` clause. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`SELECT` statements are not recommended to use `*`. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |The `SELECT` statements are not recommended to use `GROUP BY` or `ORDER BY` on different tables. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |The `SELECT` statements are not recommended to use `ORDER BY` on constants. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`SELECT` statements are not recommended to use `ORDER BY` with multiple fields in different sorting directions. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`SELECT` statements are not recommended to use `GROUP BY` expressions or functions. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`SELECT` statements are not recommended to use `UNION`. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`WHERE `conditions are not recommended to use leading wildcards for searches. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |Reverse queries (`NOT IN` and `NOT LIKE`) are not recommended in the `WHERE` condition. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`WHERE` condition detects whether filtering conditions are connected via the `OR` operator. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   |`WHERE` condition detected a `LIKE` statement without wildcards. |Enabled |* Low: recommendation.<br><br>* Medium: (default) warning.<br><br>* High: red line. |None |
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [Data change ticket management](https://docs.byteplus.com/en/docs/DBW/data_change_ticket)

* [SQL review ticket management](https://docs.byteplus.com/en/docs/DBW/sql_review_ticket)
