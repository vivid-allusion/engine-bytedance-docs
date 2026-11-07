---
title: "Creating a regular SQL change ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_a_regular_SQL_change_ticket"
---

An SQL change modifies data in a database by using `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE` statements. During an SQL change, the data content in a database is changed, but the structure of the database remains unchanged. This topic describes how to create a regular SQL change ticket on the Database Workshop (DBW) console.

## Prerequisite

* An instance and account for NDB for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

## Limitations

* You can only create regular SQL change tickets for instances with security control enabled.

* Only users added within DBW User management are allowed to create tickets.

* When executing data changes through regular SQL change tickets, the number of rows affected must not exceed 5 million; otherwise, the ticket pre\-check will fail. When data changes affect more than 5 million rows, please execute them through lock\-free data changes or lock\-free schema change tickets.

* When submitting multiple SQL statements at once, use semicolons (;) to separate them. For multiple SQL statements, each SQL statement is a separate transaction. After the ticket is created, you can view the execution progress of multiple SQL statements in the ticket details.

* Supported SQL types include `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE`.

* Executing `ALTER` statements via regular SQL change tickets may cause table locking. It is recommended to create OnlineDDL tickets for lock\-free schema changes. For detailed steps, refer to [Creating a lock-free schema change ticket (OnlineDDL)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-schema-change-ticket-OnlineDDL).

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
   |**Database & table selection** |**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |Select **Regular SQL change**. An SQL change modifies data in a database by using `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE` statements. It typically changes the data content but not the database structure. |
   ||**Instance** |From the drop\-down list, select the instance for which you want to create the ticket. |
   ||**Database** |From the drop\-down list, select the database for which you want to create the ticket. |
   |**Change configuration** |**Execute command** |Set an SQL statement as needed. Up to 1,000 SQL statements can be submitted in a single request. When submitting multiple statements, separate them with semicolons (;). SQL changes support `CREATE`, `ALTER`, `UPDATE`, `INSERT`, `REPLACE`, and `DELETE` statements.<br><br>> **tip**<br><br><br><br>* > When multiple SQL statements are submitted in a single request, if any statement fails, all subsequent statements will be halted.<br><br><br>* > When the number of SQL statements in a single submission exceeds 1,000, you can import them directly via the data interaction console. For detailed steps, see [Import table data](https://docs.byteplus.com/en/docs/DBW/Creating_a_data_import_task?lang=en).<br> |
   |**Policy configuration**<br><br> |**Execution method** |Select an execution method as required. Valid values:<br><br><br>* **Automatic execution after approval**: After the ticket is approved, the SQL statement is automatically executed.<br><br>* **Manually executed after approval**: After the ticket is approved, the creator must manually execute the SQL statement.<br><br>* **Scheduled execution after approval**: After the ticket is approved, the ticket is executed at a specified time. |
   ||**Execution start time** |Set the ticket execution start time as needed.<br><br>> **tip**<br><br><br><br>* > When selecting **Scheduled execution after approval** as the **Execution method**, you can set the **Execution start time**.<br><br><br>* > The scheduled time for structural changes must not overlap with the instance's maintenance window. For details about the maintenance window, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window?lang=en).<br> |
   ||**Execution end time** |Enable and set the ticket execution end time as needed.<br><br>> **tip**<br><br><br>> When **Scheduled execution after approval** is selected as the **Execution method** and an **Execution start time** is set, the end time must be later than the start time.<br> |
   |**Preview**<br><br> |**Approval workflow**<br><br> |Tickets use a fixed three\-level approval workflow. Approvers are configured when security control is enabled for the instance. After submitting the ticket, they cannot be modified directly. To adjust approvers, you can modify the instance's security control settings. For details, see [Enable security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control). |
   ||**Business background** |Fill in the business reason and usage scenario for creating the ticket as needed, so approvers can quickly understand the ticket's purpose, reduce communication costs, and support subsequent audits. |

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard page, you can view pre\-check items including **syntax check**, **security rule check**, **permission check**, and **number of rows affected (system statistical value, the actual number of rows affected is still subject to SQL execution**).

   * **Check passed**: All preset check items meet the requirements, with no risks or non\-compliance issues.

   * **Pending confirmation**: Indicates that non\-blocking issues or potential risks are detected, but they do not affect the core execution logic of the ticket. The system suggests paying attention to them, but allows you to continue. You must manually confirm and ignore the prompts to proceed with submitting the ticket.

   * **Failed**: Blocking issues exist. Continuing execution may cause failures, data loss, or system anomalies. You can click **View details** in the **Results details** column of a check item to see the specific reasons for the failure, then fix the issues and create a new ticket.

   > **tip**

   * > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

   * > The number of rows affected must not exceed 5 million, otherwise the pre\-check will fail. When the number of rows affected exceeds 5 million, please execute data changes via lock\-free data changes or lock\-free schema change tickets.

   * > If your account is the primary account, and both the syntax check and rows affected pre\-checks pass, but the security rule check or permission check fails, you can still click **Confirm** to create the ticket.

   * > If your account is a sub\-user, and the syntax check, rows affected pre\-check, and permission check all pass, with no high\-alert items failing in the security rule check, you can click **Confirm** to create the ticket directly.

9. Click **Submit ticket**.

## Next steps

After submitting the ticket, you can view real\-time details such as the overall execution progress, the number of executed SQL statements, and the execution status, rows affected, and execution logs of each SQL statement on the **Execute ticket** configuration wizard page in **Ticket details**. For more information, see [Manage data change tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets?lang=en).
