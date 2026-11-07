---
title: "Creating a lock-free data change ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_a_lock-free_data_change_ticket"
---

Database Workshop (DBW) provides the lock\-free data change feature, which splits single SQL statements into multiple batches for execution. This feature is suitable for large\-scale data modification scenarios, such as historical data cleanup and bulk data backups, enhancing database performance and scalability. This topic describes how to create a lock\-free data change ticket on the DBW console.

## Prerequisite

* An instance and account for veDB for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

## Limitations

* When creating a lock\-free data change ticket, the selected table must have a non\-null unique index or primary key.

* When creating a lock\-free data change ticket, the SQL text can only contain one SQL statement.

* Only instances with security control enabled are supported for creating data change tickets for management.

* Only users added within DBW User management are allowed to create tickets.

* Supported SQL types include `UPDATE`, `INSERT_SELECT` and `DELETE`. Specific restrictions for each SQL type are detailed in the table below.

   |**SQL type** |**Description** |
   |---|---|
   |* `UPDATE`<br><br>* `DELETE` |* `UPDATE` or `DELETE` statements can only be executed for a single table.<br><br>* `UPDATE` and `DELETE` statements cannot contain subquery filters.<br><br>* `LIMIT` clauses are not supported. The column where the primary key resides cannot be specified in an `UPDATE` statement. |
   |`INSERT_SELECT` |`SELECT `clauses can only be executed for a single table. The `SELECT` part cannot contain `LIMIT`, `ORDER BY`, or `GROUP BY` clauses. |

## Applicable scenarios

* The target table is large and no indexes are used in the UPDATE statement.

* A single SQL transaction involves huge amounts of data and exceeds the limit of Binlog.

* The historical data needs to be cleared.

* A large amount of data needs to be backed up.

## Advantages

Lock\-free data changes enhance database performance and scalability, as detailed below:

* High Performance: Lock\-free data changes do not lock tables during data reads, reducing locking overhead and improving system processing performance and concurrency.

* Strong scalability: Lock\-free data changes avoid locks, improving system scalability. The system can process more concurrent users and transactions.

## Principles

* Executes a single SQL statement in batches: DBW splits a single SQL statement into multiple batches for execution. By default, batches are processed in ascending order of the primary key until all rows are scanned.

* A sleep (pause) time is provided for buffering after executing each batch.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data changes** \> **Lock\-free data change**.

6. On the control panel of **Create lock\-free data change ticket**, configure the following parameter information.

   |**Parameter** ||**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   |**Database & table selection** |**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |Select **Lock\-free data change**. SQL change is to modify the data in a database by executing `UPDATE`, `INSERT_SELECT` and `DELETE` statements. During a data change, the data content in a database is changed, but the structure of the database remains unchanged. |
   ||**Instance** |From the drop\-down list, select the instance for which you want to create the ticket. |
   ||**Database** |From the drop\-down list, select the database for which you want to create the ticket. |
   |**Change configuration** |**Execute command**<br><br> |Set an SQL statement as needed. SQL changes support SQL `UPDATE`, `INSERT` and `DELETE` statements.<br><br>> **tip**<br><br><br>> A lock\-free data change ticket can contain only one SQL statement.<br> |
   |**Policy configuration**<br><br> |**Execution method** |Select an execution method as required. Valid values:<br><br><br>* **Automatic execution after approval**: After the ticket is approved, the SQL statement is automatically executed.<br><br>* **Manually executed after approval**: After the ticket is approved, the creator must manually execute the SQL statement.<br><br>* **Scheduled execution after approval**: After the ticket is approved, the ticket is executed at a specified time. |
   ||**Execution start time** |Set the ticket execution start time as needed.<br><br>> **tip**<br><br><br><br>* > When selecting **Scheduled execution after approval** as the **Execution method**, you can set the Execution start time.<br><br><br>* > The scheduled time for structural changes must not overlap with the instance's maintenance window. For details about the maintenance window, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window?lang=en).<br> |
   ||**Execution end time** |Enable and set the ticket execution end time as needed.<br><br>> **tip**<br><br><br>> When **Scheduled execution after approval** is selected as the **Execution method** and an **Execution start time** is set, the end time must be later than the start time.<br> |
   ||**Batch execution** |Set the following information as needed:<br><br><br>* **Rows per batch**: Default value is 1,000. Must be greater than or equal to 1,000.<br><br>* **Sleep time per 10,000 rows**: Default value is 0.5s. Must be greater than or equal to 0. Unit: seconds (s).<br><br>* (Optional) **Enable primary\-replica lag check?** : Enable or disable the primary\-replica lag check as needed. When enabled, the task will be interrupted if the primary\-replica lag exceeds the configured threshold.<br><br><br>> **tip**<br><br><br><br>* > By default, batches are processed in ascending order of the primary key until all rows are scanned.<br><br><br>* > Disabling the primary\-replica lag check may result in excessive latency, affecting failover operations.<br> |
   |**Preview**<br><br> |**Approval workflow** |Tickets use a fixed three\-level approval workflow: level one, level two, and level three. Approvers are configured when instance security control is enabled. After submitting a ticket, you cannot modify them directly. To adjust approvers, modify the instance's security control settings. For more information, see [Enable security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control). |
   ||**Business background** |Fill in the business reason and use case for creating the ticket as needed. This helps approvers quickly understand the ticket's purpose, reduces communication costs, and supports future audits. |

6. Click **Next step: Pre\-check**.

7. On the **Ticket pre\-check** configuration wizard page, you can view pre\-check items including **syntax check**, **security rule check**, **permission check**, and **number of rows affected (system statistical value, the actual number of rows affected is still subject to SQL execution**).

   * **Check passed**: All preset check items meet the requirements, with no risks or non\-compliance issues.

   * **Pending confirmation**: Indicates that non\-blocking issues or potential risks are detected, but they do not affect the core execution logic of the ticket. The system suggests paying attention to them, but allows you to continue. You must manually confirm and ignore the prompts to proceed with submitting the ticket.

   * **Failed**: Blocking issues exist. Continuing execution may cause failures, data loss, or system anomalies. You can click **View details** in the **Results details** column of a check item to see the specific reasons for the failure, then fix the issues and create a new ticket.

   > **tip**

   * > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

   * > If your account is the primary account, and both the syntax check and rows affected pre\-checks pass, but the security rule check or permission check fails, you can still click **Confirm** to create the ticket.

   * > If your account is a sub\-user, and the syntax check, rows affected pre\-check, and permission check all pass, with no high\-alert items failing in the security rule check, you can click **Confirm** to create the ticket directly.

8. Click **Submit ticket**.

## Next steps

After submitting the ticket, you can view real\-time details such as the overall execution progress, the number of executed SQL statements, and the execution status, rows affected, and execution logs of each SQL statement on the **Execute ticket** configuration wizard page in **Ticket details**. For more information, see [Manage data change tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets?lang=en).
