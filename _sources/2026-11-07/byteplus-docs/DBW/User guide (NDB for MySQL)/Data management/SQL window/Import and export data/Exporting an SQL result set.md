---
title: "Exporting an SQL result set"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_a_SQL_result_set_export_task"
---

DBW supports exporting SQL result sets via the SQL window. This topic explains how to export SQL result sets using the data interaction platform.

## Prerequisite

* A  NDB for MySQL instance and account have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* Make sure that the account you use to export data has read\-only permission on the target database.

## Limitations

DBW currently supports three methods for exporting SQL result sets.

|**Export method** |**Limitations** |
|---|---|
|Create an SQL result set export task<br><br> |* The instance has not enabled security control.<br><br>* After an export task is created, the file available for downloading is retained for 1 day by default and will become unavailable after expiration. Download the data immediately after obtaining the download link.<br><br>* Only one export task can be created at a time. Concurrent exports are not supported.<br><br>* For export tasks, the maximum size for a single table is 10 GiB, and the maximum total size for a single task is 50 GiB.<br><br>* For instance with security control enabled, a ticket must be submitted to export SQL result sets. |
|Creating an SQL result set export ticket |The instance has enabled security control. For more information, see [Creating an SQL result set export ticket](https://docs.byteplus.com/en/docs/DBW/Creating_an_SQL_result_set_export_ticket). |
|Export SQL result sets via SQL window |* A maximum of 3,000 data entries can be exported per file due to SQL execution result constraints.<br><br>* Due to login account permission limits, daily query frequency and maximum row limits apply. For more information, refer to [Viewing my permissions](https://docs.byteplus.com/en/docs/DBW/Viewing_my_permissions). |

## Create an SQL result set export task

1. Log in to the [Data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql) of [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql) [for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. In the upper\-right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export** tab, select **Data export** \> **SQL result set export**.

4. In the **SQL result set export** dialog box, configure the parameters as required.

   |**Parameter** |**Description** |
   |---|---|
   |**Target database** |From the drop\-down list, select the target database. |
   |**File type** |**CSV** is selected by default and can not be modified. |
   |**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   |**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`. |
   |**Export SQL** |Enter `select` statements to query data from multiple tables. When entering multiple SQL statements, the total text size is limited to a maximum of 4 GiB. |
   |**Remarks** |Optional. Describe the export task. |

5. Click **OK**.

6. On the **Import/Export** tab, find the target export task and click **Download file** in the **Actions** column.

## Export SQL result sets via SQL window

1. Log in to the [Data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql) of [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql) [for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the **Data interaction platform** page, execute the relevant SQL statements in the execution pane.

3. In the Execution result pane, perform the following operations to export the SQL result sets as needed.

   |**No.**  |**Supported function** |**Description** |
   |---|---|---|
   |1 |Export current page |Click **Export result set**, select **Export current page**, and choose the export format as needed.<br><br>> **tip**<br><br><br><br>* > DBW currently supports exporting data from the current page to `excel`, `csv`, `text`, `json`, and `insert` SQL text.<br><br><br>* > By default, 100 entries per page are displayed. You can modify the number of entries per page.<br> |
   ||Export all pages |Click **Export result set**, select **Export all pages**, and choose the export format as needed.<br><br>> **tip**<br><br><br><br>* > DBW currently supports exporting data from all pages to `excel`, `csv`, `text`, `json`, and `insert` SQL text.<br><br><br>* > A maximum of 3,000 data entries can be exported.<br> |
   ||Export selected data |1. In the execution result pane, select the target data.<br><br>2. Click **Export result set**, and choose the export format from the right\-click menu as needed.<br><br><br>> **tip**<br><br><br>> DBW currently supports exporting selected data to `excel`, `csv`, `text`, `json`, and `insert` SQL text.<br> |
   |2 |Export selected area |1. In the execution result pane, select the target data.<br><br>2. Right\-click and choose **Export selected data**, then select the export format as needed.<br><br><br>> **tip**<br><br><br>> DBW currently supports exporting selected data to `excel`, `csv`, `text`, `json`, and `insert` SQL text.<br> |
   |3 |Export all |Click **Export All** to package all current execution results into a ZIP archive. After decompression, each result set will be exported as a separate Excel file. |

> **tip**

> The number of rows displayed in SQL query results is incomplete. If you need to export more query results after security control is enabled for the instance, we recommend that you create an [SQL result set export ticket for the instance](https://docs.byteplus.com/en/docs/DBW/Creating_an_SQL_result_set_export_ticket?lang=en).
