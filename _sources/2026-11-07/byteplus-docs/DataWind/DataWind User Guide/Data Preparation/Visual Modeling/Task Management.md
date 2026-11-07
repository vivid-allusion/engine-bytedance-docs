---
title: "Task Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Task_Management"
---

<span id="_1-概述"></span>
# 1. Overview

Task management refers to viewing, operating, and configuring visual modeling tasks. In the visual modeling task overview section, users can view an overview of all visual modeling tasks within the project, including task status statistics and the task list. In the details section of a visual modeling task, users can view detailed configuration information for the visual modeling task, including basic information, processing flow, preview of input and output table data, and run records.

<span id="_2-任务概览"></span>
# 2. Task overview

On the task overview page, users can view all visual modeling tasks within the project and search for tasks by task name, input, output, or creator. Clicking the visual modeling task name takes you to the details page for that task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a9cdc9fb02f4e96b00b94dfa5a276ce~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-任务状态统计"></span>
## 2.1 Task status statistics

Displays the status of the most recent run record for each task's business date. Clicking a card filters tasks by that status. Status definitions:


* Run successful: Success—all outputs are successful.

* Run failure: Failure, terminated—there is at least one failed or terminated output.

* Running: Waiting for scheduling, waiting for upstream dependencies to complete, in synchronization—there is at least one output in progress and no failed outputs.

* Other: Not yet run, or tasks without a clear run status.


<span id="_2-2-任务列表"></span>
## 2.2 Task list


* Search: Supports searching for tasks by task name, input, output, or creator.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3535fa7d03204b009ad1fa5d9d03827b~tplv-goo7wpa0wc-image.image) </span>


* Filter

   * Run type: All, manual run, periodic run

   * Creator: All users, only mine


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c56084cb27b41fc9ee4301e7fdce221~tplv-goo7wpa0wc-image.image) </span>


* Sort: Supports sorting by most recent run time in ascending or descending order.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18db3bd4ebae4815977e55d5e8e0f96b~tplv-goo7wpa0wc-image.image) </span>


* Actions

   * Run: Select the outputs and business date for the task and run them in batch.

   * Run records: Navigate to the run records tab on the task details page.

   * Edit: Enter the edit page for the task.

   * Delete: Move to the recycle bin. Permanently deleted after 15 days.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f4b0490383b47788d04359d01f7e765~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-任务操作-运行"></span>
## 2.3 Task operations \- run

Supports manually triggering or backtracking task runs for a specific period. Select the objects to run and specify the business time, then click Confirm.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5940d04329b0478db53e8e082dba9756~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-任务操作-运行记录"></span>
## 2.4 Task operations – run records

Click Run records to navigate to the task details page and view its run records.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b383a7560abb4316a1bde47797b328c7~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-任务操作-编辑"></span>
## 2.5 Task operations – edit

Click the Edit button to navigate to the task edit page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b67510f0e5445ee92cf03b3b79273a2~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-任务操作-删除"></span>
## 2.6 Task operations – delete

A task can be quickly deleted with one click on the overview page. The deleted task is moved to the recycle bin and will be permanently deleted after 15 days.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eeba56d05759471d9ee046d02fc043be~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-任务详情"></span>
# 3. Task details

Click the task list on the left to view details for a specific task.

<span id="_3-1-基本信息"></span>
## 3.1 Basic information

Basic task information: creator, creation time, run frequency, most recent run time, most recent modification time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a256abe62d744fc800a4d0a4c0773a3~tplv-goo7wpa0wc-image.image) </span>

The top section supports the following operations:


* Permission assignment: Assign permissions for visual modeling tasks.

* Edit: Edit and modify dataset configurations.


<span id="_3-2-处理流程"></span>
## 3.2 Processing flow

**Processing flow preview** supports zooming and dragging for viewing; other operations are not currently supported.

**Output list** displays the table names corresponding to output nodes and the most recent run information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37bcab02df8d4f02a465d2fff2679599~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-数据预览"></span>
## 3.3 Data preview


* Supports selecting input or output tables.

* Supports two preview modes: table structure and detailed data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b3cde754b6e432da0787c08f78c6c11~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-运行记录"></span>
## 3.4 Run records

Allows viewing and quickly modifying run configurations.

Run records list


* Search: Supports searching output tables.

* Filter: Supports filtering by run status.

* List operations: All statuses support "Rerun"; the running status supports "Terminate".

* Batch run: Select output data and business date, then submit for batch run.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c4dbfc2099d4e1486b65265c39fd3d4~tplv-goo7wpa0wc-image.image) </span>

<span id="d567a6b0"></span>
## 3.5 Lineage view

The visual modeling lineage can be viewed, with visual modeling as the main subject, to quickly check how it is referenced and used for analysis, facilitating upstream and downstream management.


* Click upstream or downstream resources to view details.

* Supports two viewing modes: graph and table.


<span id="_4-更多操作"></span>
# 4. More operations

<span id="357cd769"></span>
## 4.1 Task maintenance

Users can click "Task Operations and Maintenance" to view the instance overview dashboard, understand the status of task execution, gain a comprehensive view of all tasks, and quickly locate tasks that require troubleshooting.

By clicking on sections such as "Run Successful" or "Run Failed," users can jump to Instance Management to view specific records.

Clicking Instance Management allows users to locate execution records via the search bar and perform operations such as rerunning single or multiple tasks, viewing logs, and viewing execution diagrams.

<span id="_4-1-模版"></span>
## 4.2 Templates

The system provides modeling task templates for user reference. Users can click the lower left corner of the page to view and apply templates.

For more information about templates, see [Commercial Bank customer churn prediction](https://docs.byteplus.com/docs/DataWind/110009), [⁣Statistical Analysis of Key Automotive User Behaviors](https://docs.byteplus.com/docs/DataWind/109978), and [Prediction of Automotive User Intent Tags](https://docs.byteplus.com/docs/DataWind/110016).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cd774b07e5f4c36949e1f6371d7a6c3~tplv-goo7wpa0wc-image.image) </span>

The template page supports searching by industry, operators used, and keywords.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c796d91b2b884df0a282b96f64b2208a~tplv-goo7wpa0wc-image.image) </span>

Click to enter the template details page, where users can view the template scenario description and apply the current template.

The data source used by template tasks is a demonstration table. Users need to modify and adjust the input table according to the actual analysis scenario.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/506562ec75fd4ef4906338806dcb71dd~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-回收站"></span>
## 4.3 Recycle bin

Clicking Recycle Bin allows users to view visual modeling tasks that have been deleted but are still within the 15\-day validity period.

To permanently delete or restore, click the operation button located on the right side of the middle section of the page. Batch delete and restore operations are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2ae4a5c41e64b57a5a0840e4d865d67~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-任务再次编辑"></span>
## 4.4 Task re\-editing

For tasks that have already been created, users with visual modeling task editing permissions can perform re\-editing and other operations. On the task details page, users can quickly view model and output information, preview data, view execution records, synchronize data, or click the Edit button to edit.

First, click the corresponding task and then click Edit in the upper right corner to enter the visual modeling editing interface. You can edit both tasks that are temporarily saved and not yet executed, as well as tasks that have already been executed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1270fe6b6e6b433cae7b3d01be539114~tplv-goo7wpa0wc-image.image) </span>

Next, in the visual modeling interface, users can edit the model, output, execution frequency, and more. For specific configuration methods, refer to [Create Offline Tasks](https://docs.byteplus.com/docs/DataWind/109984).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26b9361934a14aa294357d951ac1ed63~tplv-goo7wpa0wc-image.image) </span>
