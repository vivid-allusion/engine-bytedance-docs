---
title: "Importing table data"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_a_data_import_task"
---

DBW supports importing data into tables via the SQL window. This topic explains how to import data into a table using the data interaction platform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for veDB for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* Make sure that the account you use to import data has read/write permissions on the target database.


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

* For instance with security control enabled, a ticket must be submitted to import data. For detailed steps, refer to [Data import/export ticket management](https://docs.byteplus.com/en/docs/DBW/Data_import_and_export_ticket).


<span id=".5pON5L2c5q2l6aqk"></span>
## Import data via the menu


1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Import**.

4. In the **Data import** dialog box, configure the parameters as required. The system supports importing CSV and SQL files with configurable parameters.

   * When you select **CSV** for **File type**, you need to configure the relevant parameters as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**File type** |This example uses **CSV** as a demonstration. |
      |**Target database** |No selection is required for the current target database. |
      |**Target table** |No selection is required for the current target table. |
      |**Upload file** |Click **Upload** to upload a CSV file, with a maximum size of 1GiB. |
      |**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
      |**Write method** |Select the file write method from the drop\-down list. The following options are currently supported:<br><br><br>* **INSERT INTO**: Data will be inserted using the `insert into` method. In case of data conflicts, an error will be reported, and the insertion will stop.<br><br>* **REPLACE_INTO**: When a duplicate record exists in the table, the existing data will be overwritten. |
      |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
      |**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
      |**Remarks** |Optional. Describe the import task. |
      

   * When selecting **SQL** for **File type**, you need to configure the relevant parameters as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**File type** |This example uses **SQL** as a demonstration. |
      |**Target database** |No selection is required for the current target table. |
      |**Upload file** |Click **Upload** to upload a SQL file, with a maximum size of 1GiB. |
      |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
      |**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Checked by default. When errors are ignored and exceptions occur, the system will skip the current statement by default. |
      |**Remarks** |Optional. Describe the import task. |
      

5. Click **OK**.


<span id="QI2BqSOb"></span>
## Create a data import task


1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. In the upper right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export ** tab, click **Data import**.

4. In the **Data import ** dialog box, configure the parameters as needed.

   * When you select **CSV** for **File type**, you need to configure the relevant parameters as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**File type** |This example uses **CSV** as a demonstration. |
      |**Target database** |From the drop\-down list, select the target database. |
      |**Target table** |From the drop\-down list, select the target table. |
      |**Upload file** |Click **Select file** to upload a CSV file, with a maximum size of 1GiB. |
      |**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
      |**Write method** |Select the file write method from the drop\-down list. The following options are currently supported:<br><br><br>* **INSERT INTO**: Data will be inserted using the `insert into` method. In case of data conflicts, an error will be reported, and the insertion will stop.<br><br>* **REPLACE_INTO**: When a duplicate record exists in the table, the existing data will be overwritten. |
      |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
      |**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
      |**Remarks** |Optional. Describe the import task. |
      

   * When selecting **SQL** for **File type**, you need to configure the relevant parameters as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**File type** |This example uses **SQL** as a demonstration. |
      |**Target database** |From the drop\-down list, select the target database. |
      |**Upload file** |Click **Select file ** to upload a SQL file, with a maximum size of 1GiB. |
      |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
      |**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Checked by default. When errors are ignored and exceptions occur, the system will skip the current statement by default. |
      |**Remarks** |Optional. Describe the import task. |
      

5. Click **OK**.


<span id="whKwMhAR"></span>
## Related actions

After a successful import, the **Task status** for this task will display as **Executed successfully** on the **Import/Export** tab.
