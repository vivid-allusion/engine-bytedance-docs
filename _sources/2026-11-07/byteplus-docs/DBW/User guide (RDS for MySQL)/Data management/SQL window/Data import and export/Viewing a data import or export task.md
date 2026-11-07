---
title: "Viewing a data import or export task"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/viewing-a-data-import-or-export-task-for-mysql"
---

This topic explains how to view details of data import and export tasks on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* An import or export task has been created. For detailed steps, refer to [Creating a data import task](https://docs.byteplus.com/en/docs/DBW/creating-a-data-import-task-for-mysql) and [Creating a data export task](https://docs.byteplus.com/en/docs/DBW/creating-a-full-database-export-task-for-mysql).


<span id=".5Lu75Yqh54q25oCB6K-05piO"></span>
## Task state description


|**State** |**Description** |
|---|---|
|**Task pre\-check** |The data import task enters this state when the DBW checks the uploaded data. |
|**Pre\-check failed** |The data import task enters this state when the uploaded data fails to pass the pre\-check. |
|**Task initializing** |The data import task enters this state when the uploaded data passes the pre\-check. |
|**Task in progress** |The data import or export task is being executed. |
|**Task completed** |The data import or export task has been executed. |
|**Task failed** |The data import or export task is interrupted or becomes abnormal due to an error or a failure that occurs during execution. |


<span id=".5p-l55yL5a-85YWl5Lu75Yqh"></span>
## View a data import task


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. In the upper right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export ** tab, you can view the details about tasks.

   On the **Import/Export ** tab, you can view the task information, including **Task ID**, **Task list**, **Database**, **Table**, **Task status**, **Task progress**, and **Execution time**.

4. On the ** Import/Export** tab, find the target task and click **View details** in the **Actions** column.

5. In the **Import task details** dialog box, you can view more information on the task, including:

   * **Exception handling**: Specifies whether to report an error that occurs during data importing.

   * **Remarks**: Displays the description of the data import task.

   * **Execution log**: Displays the execution results, execution time, and specific execution details of the data import task.


<span id=".5p-l55yL5a-85Ye65Lu75Yqh"></span>
## View a data export task


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. In the upper right corner of the **Data interaction platform** page, click **Import/Export**.

3. On the **Import/Export ** tab, you can view the details about tasks.

   On the **Import/Export ** tab, you can view the task information, including **Task ID**, **Task list**, **Database**, **Table**, **Task status**, **Task progress**, and **Execution time**.

4. On the **Import/Export** tab, find the target export task and click **View details** in the **Actions** column.

5. In the **Export task details** dialog box, you can view more information on the task, including:

   * **Remarks**: Displays the description of the task.

   * **Download file**: Displays the link to download the file. This link is valid for 1 day.

   * **Execution log**: Displays the execution results, execution time, and specific execution details of the data import task.
