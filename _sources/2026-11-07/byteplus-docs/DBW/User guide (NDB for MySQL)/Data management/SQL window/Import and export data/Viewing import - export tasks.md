---
title: "Viewing import/export tasks"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/viewing-import-export-task"
---

This topic explains how to view the details of data import and export tasks on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An import or export task has been created. For detailed steps, refer to [Creating a data import task](https://docs.byteplus.com/en/docs/DBW/Creating_a_data_import_task) and [Creating a data export task](https://docs.byteplus.com/en/docs/DBW/Creating_a_full_database_export_task).

<span id=".5Lu75Yqh54q25oCB6K-05piO"></span>
## Task status description


|**Status** |**Description** |
|---|---|
|**Task pre\-check** |The status a task enters when DBW checks the uploaded data during data upload. |
|**Pre\-check failed** |The state the task enters when the pre\-check fails during data upload. |
|**Task initializing** |The state the task enters after the pre\-check is successful in an import task. |
|**Task in progress** |The status of an import/export task in progress. |
|**Task execution completed** |The status a task enters after the import/export task is completed. |
|**Task execution failed** |The status a task enters when an issue or failure occurs during the execution of an import/export task, causing it to be interrupted or abnormal. |


<span id=".5p-l55yL5a-85YWl5Lu75Yqh"></span>
## View import tasks


1. Log on to the [veDB MySQL Data Interaction Platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. In the upper right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export** tab, you can view the following task details.

   On the **Import/Export** tab, view task information, including **Task ID**, **Task list**, **Database**, **Table**, **Task status**, **Task progress**, and **Execution time**.

4. On the **Import/Export** tab, select the target task, and click **View details** under the **Actions** column to view detailed information of the specific task.

5. In the **Import task details** dialog box, view detailed information of the task, including the following:

   * **Exception handling**: Displays whether to report errors when exceptions occur during data import.

   * **Remarks**: Displays the remarks of the data import task.

   * **Execution log**: Displays the execution result, execution time, and specific execution details of the data import task.


<span id=".5p-l55yL5a-85Ye65Lu75Yqh"></span>
## View export tasks


1. Log on to the [veDB MySQL Cloud Database Data Interaction Console](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. In the upper right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export** tab, you can view the following task details.

   On the **Import/Export** tab, view task information, including **Task ID**, **Task list**, **Database**, **Table**, **Task status**, **Task progress**, and **Execution time**.

4. On the **Import/Export ** tab, select the target export task, click **View details** under the **Actions** column to view detailed information of the specific task.

5. In the **Export task details** dialog box, view detailed information of the task. Specifically includes the following information:

   * **Remarks**: Display the remarks of the task.

   * **Download file**: Display the link address for downloading the file, which is valid for 1 day.

   * **Execution log**: Display the execution results, execution time, and specific execution details of the data import task.
