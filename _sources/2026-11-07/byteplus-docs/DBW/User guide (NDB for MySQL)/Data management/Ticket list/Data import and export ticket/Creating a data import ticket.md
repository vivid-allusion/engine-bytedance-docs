---
title: "Creating a data import ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_a_data_import_ticket"
---

This topic describes how to create a data import ticket for a veDB MySQL instance on the Database Workshop (DBW) console.

## Prerequisite

* The NDB for MySQL instance is created and an account with read and write permissions on the target database is created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* The BytePlus sub\-user has been added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* The BytePlus sub\-user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

## Precautions

* Only one import task can be created at a time. Concurrent imports are not supported.

* System databases do not support data imports.

* Before importing data, verify that the source and target table structures match, including column names, data types, lengths, and order. If structures differ, manually adjust or convert the data to avoid data loss, truncation, or task failure.

* Only CSV and SQL files are supported for upload, with a maximum size of 1 GiB. Excel files are not supported.

* An import task may fail under the following conditions:

   * Insufficient database account permissions.

   * The target database or table is deleted or renamed during import.

   * Target instance restart or configuration change during import.

   * The character set of the import file is not `utf8`, `utf8mb4`, `latin1`, or `ascii`.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data import/export** \> **Data import/export**.

6. On the **Fill in the ticket** configuration wizard of the **Create data import/export ticket** control panel, configure the following parameters.

   **Create an import CSV file ticket**

|**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |Select **Data import**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning data import tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **CSV**. |
   ||**Target table** |From the drop\-down list, select the target table. |
   ||**Upload file** |Click **Upload** to upload a CSV file, with a maximum size of 1GiB. |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   ||**Write method** |Select the file write method from the drop\-down list. The following options are currently supported:<br><br><br>* **INSERT INTO**: Data will be inserted using the `insert into` method. In case of data conflicts, an error will be reported, and the insertion will stop.<br><br>* **REPLACE_INTO**: When a duplicate record exists in the table, the existing data will be overwritten. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `UTF8`, `UTF8MB4`, `LATIN1`, and `ASCII`.<br><br>> **tip**<br><br><br>> It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.<br> |
   ||**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
   ||**Business background** |Fill in the business reason and usage scenario for the ticket as needed, so that the approver can quickly understand the purpose of the ticket, reduce communication costs, and support subsequent audits. |

   **Create an import SQL file ticket**

|**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |Select **Data import**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning data import tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **CSV**. |
   ||**Target table** |From the drop\-down list, select the target table. |
   ||**Upload file** |Click **Upload** to upload a CSV file, with a maximum size of 1GiB. |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   ||**Write method** |Select the file write method from the drop\-down list. The following options are currently supported:<br><br><br>* **INSERT INTO**: Data will be inserted using the `insert into` method. In case of data conflicts, an error will be reported, and the insertion will stop.<br><br>* **REPLACE_INTO**: When a duplicate record exists in the table, the existing data will be overwritten. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `UTF8`, `UTF8MB4`, `LATIN1`, and `ASCII`.<br><br>> **tip**<br><br><br>> It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.<br> |
   ||**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
   ||**Business background** |Fill in the business reason and usage scenario for the ticket as needed, so that the approver can quickly understand the purpose of the ticket, reduce communication costs, and support subsequent audits. |

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view the **Permission check** pre\-check item.

   > **tip**

   > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

9. Click **OK**.
