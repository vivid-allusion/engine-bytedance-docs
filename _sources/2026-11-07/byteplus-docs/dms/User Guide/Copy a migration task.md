---
title: "Copy a migration task"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Copy-a-migration-task"
---

The storage migration service supports copying created tasks. This article explains how to copy migration tasks.

<span id="任务名称说明"></span>
## Task Name Description

If you do not set a new task name when copying a migration task, the new task will be named according to the following rules:


* If the original task name does not have the suffix \-copy, the new task is named by adding \-copy to the original task name. For example, if the original task name is test, the new task name will be test\-copy.

* If the suffix of the original task name is \-copy, the new task will be named by adding 1 to the suffix of the original task name. For example, if the original task name is test\-copy, the new task name will be test\-copy1.

* If the suffix of the original task name is \-copy+number, the new task is named by adding 1 to the number in the original task name. For example, if the original task name is test\-copy1, the new task name will be test\-copy2.


<span id="操作步骤"></span>
## **Procedure**


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click the name of the target task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click on the name of the target task on the <strong>Migration task</strong> list page, and then click on <strong>Replication task</strong> in the top right corner of the task details page.   </div>
   

3. On the task details page, click **Replication task** in the top right corner.

4. On the **Select network** page, after confirming the information is correct, click **Next step: Set up source and destination**.

5. On the **Set the source and destination** page, after confirming the information is correct, click **Next step:Set the task parameters**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For security reasons, please re\-enter the URL list file, Access Key ID, Access Key Secret, and other parameters. Please refer to the interface for detailed parameters.   </div>
   

6. On the **Set task parameters** page, after confirming the information is correct, click **Next step:Determine task information**.

7. After confirming the information on the **Determine task information** page, carefully read it, check **I have read and agreed Storage Products and Services Terms**, and click **submit**.

8. In the \*\*\*\* **fee reminder** dialog box, click **Known,Next step**.

9. (optional)If you have selected **Cross\-service Authorization**, you will also need to click **OK** in the pop\-up **Cross\-service Authorization** dialog box.
