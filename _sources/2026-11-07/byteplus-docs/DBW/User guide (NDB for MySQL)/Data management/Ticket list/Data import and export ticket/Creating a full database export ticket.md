---
title: "Creating a full database export ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_a_full_database_export_ticket"
---

This topic describes how to create a full database export ticket for NDB for MySQL instances in the Database Workshop DBW console.

## Prerequisite

* An NDB for MySQL instance has been created, and an account with read and write permissions on the target database has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* The BytePlus sub\-user has been added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* The BytePlus sub\-user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

## Precautions

* The download link is valid for 30 days. After this period, the file will no longer be available for download. Please download the data promptly. If the link becomes invalid within the validity period, you can regenerate a new link on the ticket details page.

* Only one export task can be created at a time. Concurrent exports are not supported.

* For export tasks, the maximum size for a single table is 10 GiB, and the maximum total size for a single task is 50 GiB.

* The `information_schema` system database is not supported for export when creating a full database export ticket.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data import/export** \> **Data import/export**.

6. On the **Fill in the ticket** configuration wizard of the **Create data import/export ticket** control panel, configure the following parameters.

   |**Category** |**Parameter** |**Description** |**CSV** |**SQL** |
   |---|---|---|---|---|
   |**Basic information**<br><br> |**Creator** |Defaults to the currently logged\-in account and can not be modified. |✔️ |✔️ |
   ||**Database type** |This article is about creating a full database export ticket for NDB for MySQL. Therefore, select **Database type** as **NDB for MySQL**. |✔️ |✔️ |
   ||**Ticket type** |Select **Full database export**. |✔️ |✔️ |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning full database export tickets will run automatically once approved. This parameter can not be modified. |✔️ |✔️ |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |✔️ |✔️ |
   ||**Database** |From the drop\-down list, select the target database. |✔️ |✔️ |
   ||**Export all tables?**  |Select whether to export all tables as needed. |✔️ |✔️ |
   ||**Target table** |Select the tables you need to download from the drop\-down list. Multiple selections are supported.<br><br>This parameter can be configured when **Export all tables?**  is set to **No**. |✔️ |✔️ |
   ||**Export content** |Select the file content to export as needed.<br><br><br>* For CSV export, you need to select **Data**.<br><br>* For SQL export, you can select **Data and structures**, **Data**, or **Structure**. |Data only**Data** |Supports **data and structures, data, and structures** |
   ||**Export structure type** |Optional. Select the structure types to download as needed. Currently supports **Stored procedures and functions**, **Trigger**, and **Event**.<br><br>This parameter can be configured when selecting **Data and structures** or **Structure** for export content. |❌ |✔️ |
   ||**File type** |Supports **CSV** and **SQL**. |**CSV** |**SQL** |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. | |❌ |
   ||**Export all tables?**  |Select whether to export all tables as needed. |✔️ |✔️ |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include **utf8**, **utf8mb4**, **latin1**, and **ascii**.<br><br>It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option. |✔️ |✔️ |
   ||**Business background** |Fill in the business reason and usage scenario for the ticket as needed, so approvers can quickly understand its purpose, reduce communication costs, and support future audits. |✔️ |✔️ |

6. Click **Next step: Pre\-check**.

7. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view the **Permission check** pre\-check item.

   > **tip**

   > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

8. Click **OK**.
