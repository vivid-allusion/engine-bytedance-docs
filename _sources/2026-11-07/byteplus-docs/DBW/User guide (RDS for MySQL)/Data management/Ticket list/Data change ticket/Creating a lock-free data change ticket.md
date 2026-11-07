---
title: "Creating a lock-free data change ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-sql-change-ticket-for-mysql"
---

Database Workshop (DBW) provides the lock\-free data change feature, which splits single SQL statements into multiple batches for execution. This feature is suitable for large\-scale data modification scenarios, such as historical data cleanup and bulk data backups, enhancing database performance and scalability. This topic describes how to create a lock\-free data change ticket on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitations


* When creating a lock\-free data change ticket, the selected table must have a non\-null unique index or primary key.

* When creating a lock\-free data change ticket, the SQL text can only contain one SQL statement.

* Only instances with security control enabled are supported for creating data change tickets for management.

* Only users added within DBW User management are allowed to create tickets.

* Supported SQL types include `UPDATE`, `INSERT_SELECT` and `DELETE`. Specific restrictions for each SQL type are detailed in the table below.

   
   |**SQL type** |**Description** |
   |---|---|
   |* `UPDATE`<br><br>* `DELETE` |* `UPDATE` or `DELETE` statements can only be executed for a single table.<br><br>* `UPDATE` and `DELETE` statements cannot contain subquery filters.<br><br>* `LIMIT` clauses are not supported.<br><br>* The column where the primary key resides cannot be specified in an `UPDATE` statement. |
   |`INSERT_SELECT` |* `SELECT `clauses can only be executed for a single table.<br><br>* The `SELECT` part cannot contain `LIMIT`, `ORDER BY`, or `GROUP BY` clauses. |
   


<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenarios


* The target table is large and no indexes are used in the UPDATE statement.

* A single SQL transaction involves huge amounts of data and exceeds the limit of Binlog.

* The historical data needs to be cleared.

* A large amount of data needs to be backed up.


<span id=".5LyY5Yq_"></span>
## Advantages

Lock\-free data changes enhance database performance and scalability, as detailed below:


* High Performance: Lock\-free data changes do not lock tables during data reads, reducing locking overhead and improving system processing performance and concurrency.

* Strong scalability: Lock\-free data changes avoid locks, improving system scalability. The system can process more concurrent users and transactions.


<span id=".5omn6KGM5Y6f55CG"></span>
## Principles


* Executes a single SQL statement in batches: DBW splits a single SQL statement into multiple batches for execution. By default, batches are processed in ascending order of the primary key until all rows are scanned.

* A sleep (pause) time is provided for buffering after executing each batch.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data changes** \> **Lock\-free data change**.

6. On the control panel of **Create lock\-free data change ticket**, configure the following parameter information.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Basic information**<br><br> |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   ||**Ticket type** |Select **Lock\-free data change**. A data change is to modify the data in a database by executing `UPDATE`, `INSERT_SELECT` and `DELETE` statements. During a data change, the data content in a database is changed, but the structure of the database remains unchanged. |
   ||**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier tracking. |
   |**Database & table selection** |**Database type** |Select **RDS for MySQL**. |
   ||**Instance** |From the drop\-down list, select the instance for which you want to create the ticket. |
   ||**Database** |From the drop\-down list, select the database for which you want to create the ticket. |
   |**Change configuration** |**Execute command** |Set an SQL statement as needed. SQL changes support SQL `UPDATE`, `INSERT` and `DELETE` statements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A lock\-free data change ticket can contain only one SQL statement.</div><br> |
   |**Policy configuration**<br><br>&nbsp;<br><br> |**Execution method**<br><br> |Select an execution method as required. Valid values:<br><br><br>* **Automatic execution after approval**: After the ticket is approved, the SQL statement is automatically executed.<br><br>* **Manually executed after approval**: After the ticket is approved, the creator must manually execute the SQL statement.<br><br>* **Scheduled execution after approval**: After the ticket is approved, the ticket is executed at a specified time. |
   ||**Execution start time** |Set the ticket execution start time as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When selecting <strong>Scheduled execution after approval</strong> as the <strong>Execution method</strong>, you can set the <strong>Execution start time</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The scheduled time for structural changes must not overlap with the instance's maintenance window. For details about the maintenance window, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br> |
   ||**Execution end time** |Enable and set the ticket execution end time as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Scheduled execution after approval</strong> is selected as the <strong>Execution method</strong> and an <strong>Execution start time</strong> is set, the end time must be later than the start time.</div><br> |
   ||**Batch execution** |Set the following information as needed:<br><br><br>* **Rows per batch**: Default value is 1,000. Must be greater than or equal to 1,000.<br><br>* **Sleep time per 10,000 rows**: Default value is 0.5s. Must be greater than or equal to 0. Unit: seconds (s).<br><br>* (Optional) **Enable primary\-replica lag check?** : Enable or disable the primary\-replica lag check as needed. When enabled, the task will be interrupted if the primary\-replica lag exceeds the configured threshold.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">By default, batches are processed in ascending order of the primary key until all rows are scanned.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Disabling the primary\-replica lag check may result in excessive latency, affecting failover operations.</div><br> |
   

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard page, you can view pre\-check items including **syntax check**, **security rule check**, **permission check**, and **number of rows affected (system statistical value, the actual number of rows affected is still subject to SQL execution**).

   * **Check passed**: All preset check items meet the requirements, with no risks or non\-compliance issues.

   * **Pending confirmation**: Indicates that non\-blocking issues or potential risks are detected, but they do not affect the core execution logic of the ticket. The system suggests paying attention to them, but allows you to continue. You must manually confirm and ignore the prompts to proceed with submitting the ticket.

   * **Failed**: Blocking issues exist. Continuing execution may cause failures, data loss, or system anomalies. You can click **View details** in the **Results details** column of a check item to see the specific reasons for the failure, then fix the issues and create a new ticket.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If pre\-check fails, you can click <strong>View details</strong> in the <strong>Result details</strong> column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your account is the primary account, and both the syntax check and rows affected pre\-checks pass, but the security rule check or permission check fails, you can still click <strong>Confirm</strong> to create the ticket.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your account is a sub\-user, and the syntax check, rows affected pre\-check, and permission check all pass, with no high\-alert items failing in the security rule check, you can click <strong>Confirm</strong> to create the ticket directly.   </div>
   

8. Click **Submit ticket**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After submitting the ticket, you can view real\-time details such as the overall execution progress, the number of executed SQL statements, and the execution status, rows affected, and execution log of each SQL statement on the **Ticket details** page under the **Execute ticket** configuration wizard. For more information, see [Manage data change tickets](https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql?lang=en).
