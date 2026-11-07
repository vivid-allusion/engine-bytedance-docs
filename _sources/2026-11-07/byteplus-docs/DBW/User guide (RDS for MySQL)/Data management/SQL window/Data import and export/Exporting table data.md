---
title: "Exporting table data"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-full-database-export-task-for-mysql"
---

DBW supports exporting data from tables via the SQL window. This topic explains how to export data from a table using the data interaction platform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* Make sure that the account you use to export data has read\-only permission on the target database.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After an export task is created, the file available for downloading is retained for 1 day by default and will become unavailable after expiration. Download the data immediately after obtaining the download link.

* Only one export task can be created at a time. Concurrent exports are not supported.

* For export tasks, the maximum size for a single table is 10 GiB, and the maximum total size for a single task is 50 GiB.

* For instance with security control enabled, a ticket must be submitted to export full database data. For details, refer to [Data import/export ticket management](https://docs.byteplus.com/en/docs/DBW/Data_import_and_export_ticket__).

* Files exported by the system are compressed in the .gz (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

   * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

   * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.


<span id=".5pON5L2c5q2l6aqk"></span>
## Export single table data via the menu

You can export all data from the target table using the menu function.


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Export**.

4. In the **Full database export** dialog box, configure the parameters as required. The system supports exporting CSV and SQL files with configurable parameters.

   
   <Tabs>
   <Tab zoneid="sF9muzRkw9" title="Select CSV as the file type">
   <TabTitle>Select CSV as the file type</TabTitle>
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Target database** |No selection is required for the current target database. |
   |**Export all tables?**  |The default value is **No**, and no selection is required. |
   |**Target table** |No selection is required for the current target table. |
   |**File type** |This example uses **CSV** as a demonstration. |
   |**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
   |**Remarks** |Optional. Describe the export task. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="bMH3vXVn3Q" title="Select SQL as the file type">
   <TabTitle>Select SQL as the file type</TabTitle>
   
   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Target database** ||No selection is required for the current target database. |
   |**Export all tables?**  ||The default value is **No**, and no selection is required. |
   |**Target table** ||No selection is required for the current target table. |
   |**File type** ||This example uses **SQL** as a demonstration. |
   |**Export content** ||Select the file content to export as needed. Options include **Data and structures**, **Data**, and **Structure**. |
   |**Export structure type** ||Optional. Select the structure types to download as needed. Currently supports **Stored procedures and functions**, **Trigger**, and **Event**.<br><br>Description<br><br>This parameter can be configured when selecting **Data and structures** or **Structure** for export content. |
   |**Character set** ||Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
   |**Remarks** ||Optional. Describe the export task. |
   |**Advanced options** |**Data options** |Check as needed whether to represent binary fields in hexadecimal format during transfer. |
   ||**SQL script extension** |Select whether to generate a `drop table` statement before the `create table` statement as needed. |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Click **OK**.

   After exporting the data, you can view the progress of the export task and download the export data file. For more information, refer to [Viewing a data import or export task](https://docs.byteplus.com/en/docs/DBW/viewing-a-data-import-or-export-task-for-mysql).


<span id=".5pON5L2c5q2l6aqk"></span>
## Export full database data by creating a task

You can export data from all tables or a single table in the target database by creating an export task.


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. In the upper right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export** tab, select **Data export** \> **Full database export**.

4. In the **Full database export** dialog box, configure the parameters as required.

   
   <Tabs>
   <Tab zoneid="ha1dSIGqg5" title="Select CSV as the file type">
   <TabTitle>Select CSV as the file type</TabTitle>
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Target database** |From the drop\-down list, select the target database. |
   |**Export all tables?**  |Select whether to export all tables as needed. |
   |**Target table** |Select the tables you need to download from the drop\-down list. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured when <strong>Export all tables?</strong> is set to <strong>No</strong>.</div><br> |
   |**File type** |This example uses **CSV** as a demonstration. |
   |**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
   |**Remarks** |Optional. Describe the export task. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="yq2QDbRoLs" title="Select SQL as the file type">
   <TabTitle>Select SQL as the file type</TabTitle>
   
   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Target database** ||From the drop\-down list, select the target database. |
   |**Export all tables?**  ||Select whether to export all tables as needed. |
   |**Target table** ||Select the tables you need to download from the drop\-down list. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured when <strong>Export all tables?</strong> is set to <strong>No</strong>.</div><br> |
   |**File type** ||This example uses **SQL** as a demonstration. |
   |**Export content** ||Select the file content to export as needed. Options include **Data and structures**, **Data**, and **Structure**. |
   |**Export structure type** ||Optional. Select the structure types to download as needed. Currently supports **Stored procedures and functions**, **Trigger**, and **Event**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can be configured when selecting <strong>Data and structures</strong> or <strong>Structure</strong> for export content.</div><br> |
   |**Character set** ||Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
   |**Remarks** ||Optional. Describe the export task. |
   |**Advanced options** |**Data options** |Check as needed whether to represent binary fields in hexadecimal format during transfer. |
   ||**SQL script extension** |Select whether to generate a `drop table` statement before the `create table` statement as needed. |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Click **OK**.

6. On the **Import/Export** tab, find the target export task and click **Download file** in the **Actions** column.
