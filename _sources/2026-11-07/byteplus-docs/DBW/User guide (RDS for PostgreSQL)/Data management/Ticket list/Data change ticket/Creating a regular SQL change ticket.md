---
title: "Creating a regular SQL change ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Create_a_regular_SQL_change_ticket"
---

An SQL change is to modify the data in a database by executing `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT` and `DELETE` statements. During an SQL change, the data content in a database is changed, but the structure of the database remains unchanged. This topic describes how to create a regular SQL change ticket on the Database Workshop (DBW) console.

## Prerequisite

* An instance and account for RDS for PostgreSQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles).

## Limitations

* Only instances with security controls enabled are supported for creating regular SQL change tickets for management.

* Only users added within DBW User management are allowed to create tickets.

* When submitting multiple SQL statements at once, use semicolons (;) to separate them. For multiple SQL statements, each SQL statement is a separate transaction. After the ticket is created, you can view the execution progress of multiple SQL statements in the ticket details.

* Supported SQL types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`, and `DELETE`.

* Executing `ALTER` statements via regular SQL change tickets may cause table locking.

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
   |**Database & table selection**<br><br> |**Database type** |Select **RDS for PostgreSQL**. |
   ||**Ticket type** |Select **Regular SQL change**. SQL change is to modify the data in a database by executing `INSERT`, `UPDATE`, and `DELETE` statements. During a data change, the data content in a database is changed, but the structure of the database remains unchanged. |
   ||**Instance** |From the drop\-down list, select the instance for which you want to create the ticket. |
   ||**Database** |From the drop\-down list, select the database for which you want to create the ticket. |
   |**Change configuration** |**Execute command** |Set an SQL statement as needed. Up to 1,000 SQL statements can be submitted in a single request. When submitting multiple statements, separate them with semicolons (;). SQL changes support SQL `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT` and `DELETE` statements.<br><br>> **tip**<br><br><br>> When multiple SQL statements are submitted in a single request, if any statement fails, all subsequent statements will be halted.<br> |
   |**Policy configuration** |**Execution method**<br><br> |Select an execution method as required. Valid values:<br><br><br>* **Automatic execution after approval**: After the ticket is approved, the SQL statement is automatically executed.<br><br>* **Manually executed after approval**: After the ticket is approved, the creator must manually execute the SQL statement.<br><br>* **Scheduled execution after approval**: After the ticket is approved, the ticket is executed at a specified time. |
   ||**Execution start time** |Set the ticket execution start time as needed.<br><br>> **tip**<br><br><br><br>* > When selecting **Scheduled execution after approval** as the **Execution method**, you can set the **Execution start time**.<br><br><br>* > The scheduled time for structural changes must not overlap with the instance's maintenance window. For details about the maintenance window, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_maintenance_window?lang=en).<br> |
   ||**Execution end time** |Enable and set the ticket execution end time as needed.<br><br>> **tip**<br><br><br>> When **Scheduled execution after approval** is selected as the **Execution method** and an **Execution start time** is set, the end time must be later than the start time.<br> |
   |**Preview**<br><br> |**Approval workflow**<br><br> |The ticket follows a fixed approval workflow with three levels: primary, secondary, and tertiary. Approvers are configured when security control is enabled for the instance. After submitting the ticket, you cannot modify the approvers directly. To adjust the approvers, you can modify the instance's security control settings. For more information, see [Enable security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control). |
   ||**Business background** |Fill in the business reason and usage scenario for creating the ticket as needed. This helps approvers quickly understand the ticket's purpose, reduces communication costs, and supports subsequent audits. |

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard page, you can view pre\-check items including **syntax check**, **security rule check**, **permission check**, and **number of rows affected (system statistical value, the actual number of rows affected is still subject to SQL execution**).

   > **tip**

   * > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

   * > If your account is the primary account, and both the syntax check and rows affected pre\-checks pass, but the security rule check or permission check fails, you can still click **Confirm** to create the ticket.

   * > If your account is a sub\-user, and the syntax check, rows affected pre\-check, and permission check all pass, with no high\-alert items failing in the security rule check, you can click **Confirm** to create the ticket directly.

9. Click **Submit ticket**.

## Next steps

[Manage tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_ticket)
