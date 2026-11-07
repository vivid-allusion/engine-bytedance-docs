---
title: "Task Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Task_Management"
---

<span id="_1-概述"></span>
# 1. Overview

Task management refers to the actions of viewing, operating, and managing configuration for visual modeling tasks by the user. In the visual modeling task overview section, users can view a summary of all visual modeling tasks within the project, including task status statistics and the task list. In the details section of a visual modeling task, users can view detailed configuration information for the task, including basic information, processing workflow, input and output table data preview, and execution records.

<span id="_2-任务概览"></span>
# 2. Task overview

On the task overview page, users can view all visual modeling tasks within the project and search for tasks by task name, input, output, or creator. Clicking the visual modeling task name will navigate to the task details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2029669687d41b58b50241997fba49f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-任务状态统计"></span>
## 2.1 Task status statistics

The status of the most recent execution record for each task's business date is displayed. Clicking a card filters by that status. Definitions of each status:


* Execution succeeded: Success—all outputs succeeded

* Execution failed: Failure, terminated—there are outputs that failed or were terminated

* Running: Waiting for scheduling, waiting for upstream dependencies to complete, synchronizing—there are outputs currently being executed, and no outputs have failed

* Other: Tasks that have not been executed yet or do not have a clear execution status


<span id="_2-2-任务列表"></span>
## 2.2 Task list


* Search: Supports searching for tasks by task name, input, output, or creator.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/815370fdda9e4977844461e1bbfdd96e~tplv-goo7wpa0wc-image.image) </span>


* Filter

   * Execution type: All, manual execution, periodic execution

   * Creator: All users, Only my tasks

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ea1bc911f1c46fa8b13bcc81387e775~tplv-goo7wpa0wc-image.image) </span>

* Sort: Supports sorting by most recent execution time in ascending or descending order.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec948de3262544678347db38d8dc48a4~tplv-goo7wpa0wc-image.image) </span>


* Actions

   * Run: Select the outputs and business date for the task, and run in batch

   * Execution records: Navigate to the execution records tab on the task details page

   * Edit: Go to the task edit page

   * Delete: Move to the recycle bin; it will be permanently deleted after 15 days


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8825acdced76466eac21d2b138c0efa9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-任务操作-运行"></span>
## 2.3 Task operations \- run

Supports manually triggering or rerunning tasks within a specific interval. Select the objects to run and choose the business time for execution, then click Confirm.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa8ceae49c704880a2b247862b249094~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-任务操作-运行记录"></span>
## 2.4 Task operations \- Run records

Click Run records to go to the details page of the task and view its run records.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05c2e93943ce4ed49a025e043ef8dd94~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-任务操作-编辑"></span>
## 2.5 Task operations \- Edit

Click the Edit button to go to the task's edit page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6e9edca8f124d1581f9fb52c207cc33~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-任务操作-删除"></span>
## 2.6 Task operations \- Delete

Users can quickly delete a task with one click on the overview page. The deleted task will be moved to the recycle bin and will be permanently deleted after 15 days.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6ad05a001b741e2992bf1734260cc16~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-任务详情"></span>
# 3. Task details

Click the task list on the left to view the details of a specific task.

<span id="_3-1-基本信息"></span>
## 3.1 Basic information

Basic task information: creator, creation time, run frequency, most recent run time, most recent modification time

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d5daf8416f6473c92871f71b8a99dd4~tplv-goo7wpa0wc-image.image) </span>

The following actions are supported at the top:


* Permission assignment: Assign permissions for visual modeling tasks.

* Edit: Edit and modify dataset configuration.


<span id="_3-2-处理流程"></span>
## 3.2 Processing flow

**Processing flow preview** supports zooming and dragging for viewing. Other operations are not supported yet.

**Output list** displays the table names corresponding to output nodes and the most recent run information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3216115995b490399cb79a5357b1594~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-数据预览"></span>
## 3.3 Data preview


* Supports selecting input/output tables.

* Supports two preview modes: table structure and detailed data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/154768a6b8724179bca61d4ae020b85a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-运行记录"></span>
## 3.4 Run records

You can view and quickly modify the run configuration.

Run records list


* Search: Supports searching output tables.

* Filter: Supports filtering by run status.

* List operations: All statuses support "Rerun"; running status supports "Terminate".

* Batch run: Select output data and business date, then submit for batch run.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abf557c29e6a47a28e2c85c55d343645~tplv-goo7wpa0wc-image.image) </span>

<span id="d567a6b0"></span>
# 4. More operations

<span id="357cd769"></span>
## 4.1 Templates

The system provides modeling task templates for users' reference. Users can click the lower left corner of the page to view and apply templates.

For more information about templates, see [Commercial Bank Customer Churn Prediction](https://docs.byteplus.com/docs/dataagent/Commercial_Bank_Customer_Churn_Prediction), [Key Behavior Statistics for Automotive Users](https://docs.byteplus.com/docs/dataagent/Key_Behavior_Statistics_for_Automotive_Users), [Predict Intent Tags for Automotive Users](https://docs.byteplus.com/docs/dataagent/Predict_Intent_Tags_for_Automotive_Users).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d991b5bd174f4e52918d662a87eedd38~tplv-goo7wpa0wc-image.image) </span>

The template page supports searching by industry, operator used, and keywords.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/763d3590a4e24deb850f02f169911305~tplv-goo7wpa0wc-image.image) </span>

Click to enter the template details page to view the template scenario description; click to apply the current template.

The data source for template tasks is a demonstration table. Users need to modify and adjust the input table based on the actual analysis scenario.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f4bf154ca1045ab8a1f1d38a3bf9403~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-回收站"></span>
## 4.2 Recycle bin

Click Recycle bin to view visual modeling tasks that have been deleted but are still within the 15\-day validity period.

To permanently delete or restore, click the action button on the right side of the middle section of the page. Batch delete and restore operations are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11ca1503e62e4e7693541c015b9c00d1~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-任务再次编辑"></span>
## 4.3 Task re\-editing

For tasks that have already been created, users with visual modeling task editing permissions can perform re\-editing and other operations. On the task details page, users can quickly view model and output information, preview data, view run records, synchronize, and perform other operations. Users can also click the Edit button to edit.

First, click the corresponding task, then click Edit in the upper right corner to enter the visual modeling editing interface. You can edit tasks that are temporarily saved and have not been run, as well as tasks that have already been run.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cb1d53f7f5848b099d1f44cbaad8625~tplv-goo7wpa0wc-image.image) </span>

Next, in the visual modeling interface, you can edit the model, output, run frequency, and more. For specific configuration methods, refer to [Task Creation](https://docs.byteplus.com/docs/dataagent/Task_Creation).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4e1b4fcab52485eae4f7819de4e31a9~tplv-goo7wpa0wc-image.image) </span>
