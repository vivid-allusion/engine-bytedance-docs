---
title: "Exporting an SQL result set"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Exporting_an_SQL_result_set"
---

DBW supports exporting SQL result sets via the SQL window. This topic explains how to export SQL result sets using the data interaction platform.

## Prerequisite

An instance, an account, a database and a table have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account), [Creating a database](https://docs.byteplus.com/en/docs/DBW/database-management-for-PG) and [Creating a table](https://docs.byteplus.com/en/docs/DBW/schema-management-for-PG).

> **tip**

> The account you create must have the corresponding permissions for querying and modifying the corresponding database.

## Precautions

* A maximum of 3,000 data entries can be exported per file due to SQL execution result constraints.

* Due to login account permission limits, daily query frequency and maximum row limits apply. For more information, refer to [Viewing my permissions](https://docs.byteplus.com/en/docs/DBW/Viewing_my_permissions).

## Create a table

1. [Log on to the data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg)icon after the database, select the target database.

3. On the **Data interaction platform** page, execute the relevant SQL statements in the execution pane.

4. In the Execution result pane, perform the following operations to export the SQL result sets as needed.

   |**Supported function** |**Description** |
   |---|---|
   |Export current page |Click **Export result set**, select **Export current page**, and choose the export format as needed.<br><br>> **tip**<br><br><br><br>* > DBW currently supports exporting current page data to `excel`, `csv`, `text`, `JSON`, and `insert` SQL formats.<br><br><br>* > By default, 100 entries per page are displayed. You can modify the number of entries per page.<br> |
   |Export all pages |Click **Export result set**, select **Export all pages**, and choose the export format as needed.<br><br>> **tip**<br><br><br><br>* > DBW currently supports exporting data from all pages to `excel`, `csv`, `text`, `JSON`, and `insert` SQL text.<br><br><br>* > A maximum of 3,000 data entries can be exported.<br> |
   |Export selected data |1. In the execution result pane, select the target data.<br><br>2. Click **Export result set**, and choose the export format from the right\-click menu as needed.<br><br><br>> **tip**<br><br><br>> DBW currently supports exporting selected data to `excel`, `csv`, `text`, `JSON`, and `insert` SQL text.<br> |
   |Export selected area |1. In the execution result pane, select the target data.<br><br>2. Right\-click and choose **Export selected data**, then select the export format as needed.<br><br><br>> **tip**<br><br><br>> DBW currently supports exporting data from the selected area to `Excel`, `CSV`, `Text`, `JSON`, and `Insert` SQL text.<br> |
   |Export all |In the upper\-right corner of the execution results area, click **Export All** to package all current execution results into a ZIP archive. After extraction, each result set will be exported as a separate Excel file. |
