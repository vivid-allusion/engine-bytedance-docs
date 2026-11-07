---
title: "Managing migration evaluation tasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Managing_migration_evaluation_tasks"
---

This topic describes how to view and manage migration evaluation tasks on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data migration evaluation task has been created. For more information, refer to [Create migration evaluation task](https://docs.byteplus.com/en/docs/DTS/Creating_a_migration_evaluation_task).

<span id=".5p-l55yL6L-B56e76K-E5Lyw5Lu75Yqh"></span>
## Viewing a migration evaluation task


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation pane, click **Migration evaluation**.

* Viewing a migration evaluation task list

   On the **Migration evaluation list** page, you can view the Task name/ID, Task status, Source database, Target database, Start time, and End time of the migration evaluation tasks.

   * **Task status** includes **To be started**, **In progress**, **Suspended**, **Evaluate completed**, and **Evaluate failed**.

      When the task status is displayed as **Evaluate completed**, reevaluation of the task is supported.

   * Source database and target database: Hover the cursor over the source and target databases to view the relevant information of the source and target instances.

* View a migration evaluation report

   You can view the evaluation report in the following two methods:

   * Method 1: On the **Migration evaluation list** page, click the migration task name and view the evaluation report on the **Migration evaluation report** page.

   * Method 2;

      1. Click **...**  in the **Action** column of the target task. \> **View report**.

      2. On the **Migration evaluation report** page, **view** the evaluate report.

         * The evaluate report includes basic information of the migration task, evaluate conclusions (including evaluated item, passed item, prompt item, and failed term) and evaluate item details. For more information about evaluation items, refer to [Migration evaluation](https://docs.byteplus.com/en/docs/DTS/Migration_evaluation_overview#.6L-B56e76K-E5Lyw5Yqf6IO9).

         * If the migration evaluation failed or an evaluation item fails, you can click **View optimization suggestions** of the evaluation item, correct related problems according to the optimization suggestions, and then reevaluate. For detailed operations, refer to [Reevaluate migration task](https://docs.byteplus.com/en/docs/DTS/Managing_migration_evaluation_tasks#.6YeN5paw6K-E5Lyw6L-B56e75Lu75Yqh).


<span id=".5LiL6L296L-B56e76K-E5Lyw57uT5p6c"></span>
## Downloading migration evaluation results


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left\-side navigation pane, click **Migration evaluation**. You can download the migration evaluation report in the following two ways:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Do not close the download preview interface during the report download, otherwise the download will fail.   </div>
   

   * Method 1: On the **Migration evaluation list** page, click the migration task name, and on the **Migration evaluation report** page, click **Download the report**.

   * Method 2;

      1. Click **...**  in the **Action** column of the target task. \> **View report**.

      2. On the **Migration evaluation report** page, click **Download the report**.


<span id=".6YeN5paw6K-E5Lyw6L-B56e75Lu75Yqh"></span>
## Reevaluate the migration task

You can reevaluate tasks whose **Task status** is **Evaluate completed**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The completed evaluation task can be reevaluated within 6 hours. If it exceeds 6 hours, the task status will change to evaluate completed. If you need to reevaluate, create a new evaluation task. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/Creating_a_migration_evaluation_task">Create migration evaluation task</a>.</div>



1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation pane, click **Migration evaluation**.

4. On the **Migration evaluation list** page, filter tasks with **Task status** of **Evaluate completed**.

5. Select one of the following methods to reevaluate as needed:

   * Method 1:

      1. Click **...**  in the **Action** column of the target task. \> **Reevaluate**.

      2. In the **Whether to reevaluate** dialog box, click **Reevaluate**.

   * Method 2: 

      1. Click the target task name. On the **Migration evaluation report** page, click **Reevaluate**.

      2. In the **Reevaluate** dialog box, click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation pane, click **Migration evaluation**.

4. On the **Migration evaluation list** page, manage the evaluate task.

   
   |**Actions** |**Limits** |**Description** |
   |---|---|---|
   |Starting the evaluation task |You can start **Suspended** and **To be started** evaluation tasks. |1. Click **Start** in the **Action** column of the target task.<br><br>2. In the **Whether to start selected Migration evaluation task** dialog box, click **Start**. |
   |Configuring the evaluation task |You can configure **To be started** tasks. |1. Click **Configuration** in the **Action** column of the target task.<br><br>2. On the **Configuring source and target database** configuration wizard page, configure the relevant information of the source and target database.<br><br>3. Click **Next: Configure migration evaluation object**.<br><br>4. After configuring the migration evaluation object, click **Next: View evaluate results**.<br><br><br>For more configuration information, refer to [Create Migration evaluation task](https://docs.byteplus.com/en/docs/DTS/Creating_a_migration_evaluation_task). |
   |Retry the evaluate task |Only **valuate failed** tasks can be retried. |1. Click **...**  in the **Action** column of the target task. \> **Retry**.<br><br>2. In the **Whether to reevaluate selected migration evaluation task** dialog box, click **Retry**. |
   |Pause the evaluate task |You can pause **in progress** and **Evaluate completed** evaluation tasks. |1. Click **...**  in the **Action** column of the target task. \> **Suspend**.<br><br>2. In the **Whether to pause selected Migration evaluation task** dialog box, click **Pause**. |
   |Terminating evaluation task |You can terminate evaluate **In progress**, **Evaluate completed**, and **Suspended** tasks. |1. Click **...**  in the **Action** column of the target task. \> **Terminate**.<br><br>2. In the **Whether to terminate the selected migration evaluation task** dialog box, click **Terminate**. |
   |Deleting migration evaluation task |It cannot be restored after deletion, proceed with caution. |1. Click **...**  in the **Action** column of the target task. \> **Delete**.<br><br>2. In the **Whether to reevaluate selected migration evaluation task** dialog box, click **Delete**. |
