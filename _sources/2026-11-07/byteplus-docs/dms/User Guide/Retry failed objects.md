---
title: "Retry failed objects"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Retry-failed-objects"
---

When there are object migration failures in a migration task, you can use the retry failed 0bjects feature to create a new task for the failed objects after the migration task is completed. This article explains how to use the "Retry Failed Objects" feature.

<span id="1806ce0c"></span>
## Background Information

You can view the task status of the target task and obtain information about task execution on the **Migration task list** page. The instructions are as follows:


* **Migration complete**: All objects have been successfully migrated.

* **Partial migration failed,tried again**: Partial object migration failed.

* **failed**: All object migrations have failed.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

11 migration task can only create 1 retry failed task.

<span id=".6buY6K6k5ZG95ZCN6KeE5YiZ6K-05piO"></span>
## Default Naming Convention Explanation

If you do not set a new task name when using the retry failed object feature, the new task will be named according to the following rules:


* If the original task name does not have the suffix \-failure, the new task will be named by adding \-failure to the original task name. For example, if the original task name is test, the new task name will be test\-failure.

* If the original task name has a suffix of \-failure, the new task will be named by adding 1 to the suffix of the original task name. For example, if the original task name is test\-failure, the new task name will be test\-failure1.

* If the suffix of the original task name is \-failure+number, the new task will be named by adding 1 to the number in the original task name. For example, if the original task name is test\-failure1, the new task name will be test\-failure2.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click **Retey** in the Target Task **Actions** column.

3. In the Retry Failed Objects dialog box, set the task name and then click **OK**.
