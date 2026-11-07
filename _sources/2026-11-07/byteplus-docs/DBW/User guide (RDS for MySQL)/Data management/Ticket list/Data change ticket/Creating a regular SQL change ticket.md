---
title: "Creating a regular SQL change ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql"
---

An SQL change modifies data in a database by using `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE` statements. During an SQL change, the data content in a database is changed, but the structure of the database remains unchanged. This topic describes how to create a regular SQL change ticket on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/role-permission-request).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitations


* Only instances with security controls enabled are supported for creating regular SQL change tickets for management.

* Only users added within DBW User management are allowed to create tickets.

* When executing data changes through regular SQL change tickets, the number of rows affected must not exceed 5 million; otherwise, the ticket pre\-check will fail. When data changes affect more than 5 million rows, please execute them through lock\-free data changes or lock\-free schema change tickets.

* When submitting multiple SQL statements at once, use semicolons (;) to separate them. For multiple SQL statements, each statement runs as a separate transaction. After the ticket is created, you can view the execution progress of each SQL statement in the ticket details.

* Supported SQL types include `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE`.

* Executing `ALTER` statements via regular SQL change tickets may cause table locking. It is recommended to create OnlineDDL tickets for lock\-free schema changes. For detailed steps, refer to [Creating a lock-free schema change ticket (OnlineDDL)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data changes** \> **Regular SQL change**.

6. On the control panel of **Create regular SQL change ticket**, configure the following parameter information.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   ||**Ticket type** |Default: **Regular SQL change**. This value cannot be modified. A regular SQL change modifies data in a database by using the `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE` statements. This type of change is typically used to modify the content of data in a database without altering the database structure. |
   ||**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier tracking. |
   |**Database & table selection** |**Database type** |Select **RDS for MySQL**. |
   ||**Instance** |From the drop\-down list, select the instance for which you want to create the ticket. |
   ||**Database** |From the drop\-down list, select the database for which you want to create the ticket. |
   |**Change configuration** |**Execute command** |Set an SQL statement as needed. Up to 1,000 SQL statements can be submitted in a single request. When submitting multiple statements, separate them with semicolons (;). SQL changes support `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE` statements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When multiple SQL statements are submitted in a single request, if any statement fails, all subsequent statements will be halted.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the number of SQL statements in a single submission exceeds 1,000, you can import them directly via the data interaction console. For details, see <a href="https://docs.byteplus.com/en/docs/DBW/creating-a-data-import-task-for-mysql?lang=en">Import Table Data</a>.</div><br> |
   |**Policy configuration** |**Execution method** |Select an execution method as required. Valid values:<br><br><br>* **Automatic execution after approval**: After the ticket is approved, the SQL statement is automatically executed.<br><br>* **Manually executed after approval**: After the ticket is approved, the creator must manually execute the SQL statement.<br><br>* **Scheduled execution after approval**: After the ticket is approved, the ticket is executed at a specified time. |
   ||**Execution start time**<br><br> |Set the ticket execution start time as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When selecting <strong>Scheduled execution after approval</strong> as the <strong>Execution method</strong>, you can set the <strong>Execution start time</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The scheduled time for structural changes must not overlap with the instance's maintenance window. For details about the maintenance window, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period?lang=en">Configuring maintenance window</a>.</div><br> |
   ||**Execution end time** |Enable and set the ticket execution end time as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Scheduled execution after approval</strong> is selected as the <strong>Execution method</strong> and an <strong>Execution start time</strong> is set, the end time must be later than the start time.</div><br> |
   

6. Click **Next step: Pre\-check**.

7. On the **Ticket pre\-check** configuration wizard page, you can view pre\-check items including **syntax check**, **security rule check**, **permission check**, and **number of rows affected (system statistical value, the actual number of rows affected is still subject to SQL execution**).

   * **Check passed**: All preset check items meet the requirements, with no risks or non\-compliance issues.

   * **Pending confirmation**: Indicates that non\-blocking issues or potential risks are detected, but they do not affect the core execution logic of the ticket. The system suggests paying attention to them, but allows you to continue. You must manually confirm and ignore the prompts to proceed with submitting the ticket.

   * **Failed**: Blocking issues exist. Continuing execution may cause failures, data loss, or system anomalies. You can click **View details** in the **Results details** column of a check item to see the specific reasons for the failure, then fix the issues and create a new ticket.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If pre\-check fails, you can click <strong>View details</strong> in the <strong>Result details</strong> column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The number of rows affected must not exceed 5 million, otherwise the pre\-check will fail. When the number of rows affected exceeds 5 million, please execute data changes via lock\-free data changes or lock\-free schema change tickets.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your account is the primary account, and both the syntax check and rows affected pre\-checks pass, but the security rule check or permission check fails, you can still click <strong>Confirm</strong> to create the ticket.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your account is a sub\-user, and the syntax check, rows affected pre\-check, and permission check all pass, with no high\-alert items failing in the security rule check, you can click <strong>Confirm</strong> to create the ticket directly.   </div>
   

8. Click **Submit ticket**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After the ticket is submitted, you can view detailed information such as the overall execution progress, the number of executed SQL statements, and the execution status, rows affected, and execution logs of each SQL statement on the **Ticket details** page in the **Execute ticket** configuration wizard. For more information, see [Manage data change tickets](https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql?lang=en).
