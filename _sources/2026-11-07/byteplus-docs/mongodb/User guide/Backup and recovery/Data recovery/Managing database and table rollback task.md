---
title: "Managing database and table rollback task"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/manage-rollback-task"
---

After initiating a database and table data rollback task, you can manage rollback tasks on the MongoDB console. This topic describes how to manage database and table rollback tasks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

A table rollback task has been created. For specific procedures, refer to [Rolling back database and table data](https://docs.byteplus.com/en/docs/mongodb/roll-back-data).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database\> MongoDB \> Batch rollback**.

4. Under the **Rollback task** tab on the **Batch rollback** page, you can perform the following management operations on rollback tasks.

   
   |Supported operations |Description |
   |---|---|
   |Viewing rollback task details |In the rollback task list, you can view the details of rollback tasks that have been executed or are being executed, including the task ID, instance ID, start and end time of the rollback task, execution progress, task status, and rollback time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also specify the start and end time at the top left of the list to filter tasks, or filter tasks by their status.</div><br> |
   |Managing successful rollback tasks |1. In the rollback task list, filter rollback tasks in the status of **Succeeded**, and then click **View details** in the **Actions** column.<br><br>2. On the **Batch modify table names** panel, you can perform the following operations:<br><br>   * Viewing details of database and table rolled back<br><br>      View database table details in the current rollback task, including database name, data table name, rollback table name, and so on.<br><br>   * Modifying table names in batches<br><br>      1. In the upper\-right corner of the **Batch modify table names** panel, click **Batch modify table names**.<br><br>      2. In the pop\-up dialog box, click **OK**.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This operation modifies the names of all tables under a single instance in a single rollback task. If you select multiple instances for batch task rollback, you need to access the <strong>Batch modify table names</strong> panel of each instance to modify the table names.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After batch modification, the table names change to <strong>original table name\-new table name</strong>, while the name of the rolled\-back table changes to <strong>rolled\-back table name\-new table name</strong>.      </div><br>      <br><br>   * Exporting rollback database and table list<br><br>      1. In the upper\-right corner of the **Batch modify table names** panel, click  <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) </span>  icon.<br><br>      2. In the pop\-up dialog box, select the database and table information to be exported according to your business needs, then click **OK**.<br><br>         After clicking **OK**, the rollback database and table list will be exported as a CSV file and automatically downloaded to your local device via the browser. You can view the file using a text editor. |
