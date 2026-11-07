---
title: "Task Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Task_Management____"
---

<span id="_1-概述"></span>
# 1. Overview

Task management refers to the actions of viewing, operating, and configuring visual modeling tasks by the user. In the visual modeling task overview section, users can view an overview of all visual modeling tasks within the project, which includes task status statistics and a task list. In the details section of a visual modeling task, users can view detailed configuration information for the visual modeling task, including basic information, processing flow, preview of input and output table data, and run records.

<span id="_2-任务概览"></span>
# 2. Task overview

On the task overview page, users can view all visual modeling tasks within the project and search by task name, input, output, or creator. Click the name of a visual modeling task to go to its details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2029669687d41b58b50241997fba49f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-任务状态统计"></span>
## 2.1 Task status statistics

The status of the most recent run record for each task's business date is displayed; clicking a card filters by that status. Definitions of each status:


* Run successful: Success—all outputs are successful

* Run failed: Failure, terminated—there is at least one failed or terminated output

* Running: Waiting for scheduling, waiting for upstream dependencies to complete, synchronizing—there is at least one output in progress and no failed outputs

* Other: Not yet run, or tasks without a clear run status


<span id="_2-2-任务列表"></span>
## 2.2 Task list


* Search: Search by task name, input, output, or creator.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/815370fdda9e4977844461e1bbfdd96e~tplv-goo7wpa0wc-image.image) </span>


* Filters

   * Run type: All, manual run, periodic run

   * Creator: Everyone, only my tasks


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ea1bc911f1c46fa8b13bcc81387e775~tplv-goo7wpa0wc-image.image) </span>


* Sort: Supports sorting by most recent run time in ascending or descending order.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec948de3262544678347db38d8dc48a4~tplv-goo7wpa0wc-image.image) </span>


* Actions

   * Run: Select the outputs and business date for the task, and run in batch.

   * Run records: Navigate to the run records tab on the task details page

   * Edit: Enter the edit page for the task

   * Delete: Move to the recycle bin; permanently deleted after 15 days.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8825acdced76466eac21d2b138c0efa9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-任务操作-运行"></span>
## 2.3 Task operations \- run

Supports manually triggering or backtracking the execution of tasks within a specific interval. Select the objects to run and choose the business time for execution, then click Confirm.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa8ceae49c704880a2b247862b249094~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-任务操作-运行记录"></span>
## 2.4 Task operations \- run records

Click Run Records to navigate to the task details page and view the run records for the task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05c2e93943ce4ed49a025e043ef8dd94~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-任务操作-编辑"></span>
## 2.5 Task operations \- edit

Click the Edit button to navigate to the task editing page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6e9edca8f124d1581f9fb52c207cc33~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-任务操作-删除"></span>
## 2.6 Task operations \- delete

Users can quickly delete tasks with one click on the overview page. Deleted tasks will be moved to the recycle bin and will be permanently deleted after 15 days.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6ad05a001b741e2992bf1734260cc16~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-任务详情"></span>
# 3. Task details

Click the task list on the left to view the details of a specific task.

<span id="_3-1-基本信息"></span>
## 3.1 Basic information

Task basic information: creator, creation time, run frequency, most recent run time, most recent modification time

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d5daf8416f6473c92871f71b8a99dd4~tplv-goo7wpa0wc-image.image) </span>

The following operations are supported at the top:


* Permission assignment: assign permissions for visual modeling tasks;

* Edit: edit dataset configuration;


<span id="_3-2-处理流程"></span>
## 3.2 Processing flow

**Processing flow preview** supports zooming and dragging for viewing; other operations are not currently supported

**Output list** displays the table names corresponding to output nodes and the most recent run information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3216115995b490399cb79a5357b1594~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-数据预览"></span>
## 3.3 Data preview


* Supports selecting input/output tables

* Supports two preview modes: table structure and detailed data


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/154768a6b8724179bca61d4ae020b85a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-运行记录"></span>
## 3.4 Run records

Allows viewing and quickly modifying run configuration.

Run records list


* Search: supports searching output tables

* Filter: supports filtering by run status

* List operations: all statuses support "rerun"; running status supports "terminate"

* Batch run: select output data and business date, then submit for batch run


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abf557c29e6a47a28e2c85c55d343645~tplv-goo7wpa0wc-image.image) </span>

<span id="d567a6b0"></span>
# 4. More operations

<span id="357cd769"></span>
## 4.1 Templates

The system provides modeling task templates for user reference. Users can click the lower left corner of the page to view and apply templates.

For more information about templates, see [Commercial Bank Customer Churn Prediction](https://docs.byteplus.com/docs/dataagent/Commercial_Bank_Customer_Churn_Prediction_)[⁣Statistical Analysis of Key Behaviors of Automotive Users](https://docs.byteplus.com/docs/dataagent/Statistical_Analysis_of_Key_Behaviors_of_Automotive_Users) [Prediction of Automotive User Intent Tags](https://docs.byteplus.com/docs/dataagent/Prediction_of_Automotive_User_Intent_Tags_).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d991b5bd174f4e52918d662a87eedd38~tplv-goo7wpa0wc-image.image) </span>

The template page supports searching by industry, operator used, and keywords.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/763d3590a4e24deb850f02f169911305~tplv-goo7wpa0wc-image.image) </span>

Click to enter the template details page, where users can view the scenario description for the template and apply the current template.

The data source used for template tasks is a demonstration table. Users need to modify and adjust the input table according to their actual analysis scenarios.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f4bf154ca1045ab8a1f1d38a3bf9403~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-回收站"></span>
## 4.2 Recycle bin

Click Recycle bin to view visual modeling tasks that have been deleted but are still within the 15\-day validity period.

To permanently delete or restore a task, click the operation button on the right side of the middle section of the page. Batch delete and restore operations are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11ca1503e62e4e7693541c015b9c00d1~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-任务再次编辑"></span>
## 4.3 Editing tasks again

For tasks that have already been created, users with visual modeling task editing permissions can edit again or perform further editing and other operations. On the task details page, users can quickly view model and output information, preview data, view run records, synchronize data, and click the Edit button to make changes.

First, click the corresponding task, then click Edit in the upper right corner to enter the visual modeling editor. You can edit tasks that are temporarily stored and have not been run, as well as tasks that have already been run.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cb1d53f7f5848b099d1f44cbaad8625~tplv-goo7wpa0wc-image.image) </span>

Next, in the visual modeling editor, you can edit the model, output, run frequency, and more. For specific configuration methods, refer to [Task Creation](https://docs.byteplus.com/docs/dataagent/Task_Creation___).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4e1b4fcab52485eae4f7819de4e31a9~tplv-goo7wpa0wc-image.image) </span>
