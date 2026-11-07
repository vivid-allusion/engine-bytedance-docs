---
title: "Creating an SQL result set export ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_an_SQL_result_set_export_ticket"
---

This topic describes how to create an SQL result set export ticket for an NDB for MySQL instance in the Database Workshop DBW console.

## Prerequisite

* The NDB for MySQL instance is created and an account with read and write permissions on the target database is created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* The BytePlus sub\-user has been added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* The BytePlus sub\-user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

## Precautions

* The download link is valid for 30 days. After this period, the file will no longer be available for download. Please download the data promptly. If the link becomes invalid within the validity period, you can regenerate a new link on the ticket details page.

* Only one export task can be created at a time. Concurrent exports are not supported.

* For export tasks, the maximum size for a single table is 10 GiB, and the maximum total size for a single task is 50 GiB.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data import/export** \> **Data import/export**.

6. On the **Fill in the ticket** configuration wizard of the **Create data import/export ticket** control panel, configure the following parameters.

   **Export CSV file tickets**

|**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |Select **SQL result set export**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning full database export tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **CSV**. |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`.<br><br>> **tip**<br><br><br>> It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.<br> |
   ||**Export executed SQL** |Enter `select` statements to query data from multiple tables. When entering multiple SQL statements, the total text size is limited to a maximum of 4 GiB. |
   ||**Business background** |Fill in the business reason and usage scenario for creating the ticket as needed, so that the approver can quickly understand the purpose of the ticket, reduce communication costs, and use it for subsequent audits. |

   **Export SQL file tickets**

|**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |Select **SQL result set export**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning full database export tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **SQL**. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`.<br><br>> **tip**<br><br><br>> It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.<br> |
   ||**Export executed SQL** |Enter select statements to query data from multiple tables. When entering multiple SQL statements, the total text size is limited to a maximum of 4 GiB. |
   ||**Business background** |Fill in the business reason and usage scenario for creating the ticket as needed, so that the approver can quickly understand the purpose of the ticket, reduce communication costs, and use it for subsequent audits. |

6. Click **Next step: Pre\-check**.

7. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view pre\-check items, including **Syntax** and **Permission**.

   > **tip**

   > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

8. Click **OK**.
