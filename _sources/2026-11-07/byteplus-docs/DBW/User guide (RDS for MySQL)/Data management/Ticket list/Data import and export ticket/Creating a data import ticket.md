---
title: "Creating a data import ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-data-import-ticket"
---

This topic explains how to create a data import ticket for an RDS for MySQL instance on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL and an account with read/write permissions to the target database have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The BytePlus sub\-user has been added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* The BytePlus sub\-user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5rOo5oSP5LqL6aG5"></span>
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


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data import/export** \> **Data import/export**.

6. On the **Fill in the ticket** configuration wizard of the **Create data import/export ticket** control panel, configure the following parameters.

   
   <Tabs>
   <Tab zoneid="oIqed6pXcW" title="Create an import CSV file ticket">
   <TabTitle>Create an import CSV file ticket</TabTitle>
   
   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. If not set, it defaults to empty. |
   ||**Database type** |This topic describes how to create a data import ticket for RDS for MySQL. Therefore, select **RDS for MySQL** as the **Database type**. |
   ||**Ticket type** |Select **Data import**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning data import tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **CSV**. |
   ||**Target table** |From the drop\-down list, select the target table. |
   ||**Upload file** |Click **Upload** to upload a CSV file, with a maximum size of 1GiB. |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   ||**Write method** |Select the file write method from the drop\-down list. The following options are currently supported:<br><br><br>* **INSERT INTO**: Data will be inserted using the `insert into` method. In case of data conflicts, an error will be reported, and the insertion will stop.<br><br>* **REPLACE_INTO**: When a duplicate record exists in the table, the existing data will be overwritten. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `UTF8`, `UTF8MB4`, `LATIN1`, and `ASCII`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.</div><br> |
   ||**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
   ||**Ticket remarks** |Optional. Customize your ticket remarks. We recommend aligning them with your business for easier tracking. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="bmjsX1c27l" title="Create an import SQL file ticket">
   <TabTitle>Create an import SQL file ticket</TabTitle>
   
   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. If not set, it defaults to empty. |
   ||**Database type** |This topic describes how to create a data import ticket for RDS for MySQL. Therefore, select **RDS for MySQL** as the **Database type**. |
   ||**Ticket type** |Select **Data import**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning data import tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **SQL**. |
   ||**Upload file** |Click **Upload** to upload a SQL file, with a maximum size of 1GiB. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `UTF8`, `UTF8MB4`, `LATIN1`, and `ASCII`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.</div><br> |
   ||**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
   ||**Ticket remarks** |Optional. Customize your ticket remarks. We recommend aligning them with your business for easier tracking. |
   
   
   
   
   
   </Tab>
   </Tabs>
   

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view the **Permission check** pre\-check item.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If pre\-check fails, you can click <strong>View details</strong> in the <strong>Result details</strong> column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.   </div>
   

9. Click **OK**.
