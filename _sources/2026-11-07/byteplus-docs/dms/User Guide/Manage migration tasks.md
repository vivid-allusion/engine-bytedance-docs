---
title: "Manage migration tasks"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Manage-migration-tasks"
---

After creating a migration task, you can manage it through the Storage Migration Service console. This includes viewing task details, downloading reports, and deleting migration tasks. This article explains how to manage migration tasks.

<span id="前提条件"></span>
## **Prerequisites**

Migration task has been created. For specific steps, please refer to [Create a migration task](https://docs.byteplus.com/docs/dms/Create-a-migration-task).

<span id="查看任务详情"></span>
## View task details


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click the name of the target task,view the detailed information of this task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the <strong>Migrated storage capacity</strong>, <strong>Number of migrated files</strong>, <strong>Estimated remaining migration time</strong>,<strong>Basic information</strong>,<strong>Network information</strong>, <strong>Parameter information</strong>, <strong>Source information</strong>, and <strong>Destination information</strong> of the migration task.   </div>
   

<span id="查看迁移进程"></span>
## View migration progress


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click  **...**  \> **View migration progress** in the **Actions** column of the target task.

3. View migration process details in the pop\-up dialog box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your migration task is an incremental task, you can view the time and detailed information of each incremental task execution during the process.   </div>
   

<span id="暂停迁移任务"></span>
## Pause migration task


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click  **...**  \> **Pause** in the **Actions** column of the target task.

3. Click **OK** in the pop\-up dialog box to pause the migration task.


<span id="删除迁移任务"></span>
## Delete migration task

After the migration task is completed, you can delete the task.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting the task, it is recommended that you revoke the corresponding permissions or delete the used keys during the migration process.</div>



1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click  **...**  \> **Delete** in the **Actions** column of the target task.

3. In the pop\-up dialog box, click delete.


<span id="74ec405e"></span>
## Filter migration tasks


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task** list page, click on the filter icon in the **Task status** column, select the target status, and click on **OK**.

   After completing the settings, the migration task list page will only display tasks in the target state.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the <strong>Migration task</strong> list page, click on the filter icon in the <strong>Task status</strong> column，Click on <strong>Reset</strong>, the migration task list page will display all tasks.   </div>
   

<span id="修改流控"></span>
## Modify flow control

Tasks in the states of Initializing, Migrating, Waiting for migration, Suspending, Suspended, and Failed can be modified for flow control time periods and rates.


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click the name of the target task.

3. On the task details page, click on the right side of **modify** next to the **Flow control period/rate** in the **Parameter information** area.

4. In the **Flow control period/ratedialog** box, modify the flow control period and rate, and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the Flow control period/rate dialog box, click <strong>Add Field</strong> to add <strong>Flow control period</strong> and <strong>rate</strong>.   </div>
