---
title: "Data backfill"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data_backfill"
---

You can use data backtracking to perform **backfill/rerun** operations for tasks within a specified historical time range. Supports backtracking for a single task, a single task and its downstream tasks, multiple tasks, and multiple tasks and their downstream tasks. After initiating backtracking, you can view the backtracked instances in instance maintenance.

This article will introduce how to perform data backtracking.

<span id="_1-使用场景"></span>
## 1 Use cases

Supplement data: After a new task is submitted and goes live, data for the past 30 days needs to be supplemented. This can be accomplished through data backfill.

Rerun: When there are existing tasks and the data processing logic has changed, it is necessary to correct the previously generated data. This can be accomplished through data reprocessing.

<span id="_2-进入数据回溯"></span>
## 2 Access the data backtracking feature


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Under the corresponding project, click the **Maintenance \> Batch Task Operations \> Data backfill** interface.


The data traceability module is divided into three sections: initiated, received, and pending review. The functions of each module are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f176ab776c9d4033bd48b1c1267307bc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-发起的回溯列表"></span>
## 3. List of initiated tracebacks

You can view all data trace\-back records initiated by this project here, create new data trace\-back records, and quickly filter records by initiation time, task status, trace\-back scope, task level, and other parameters.

<span id="_3-1-新建数据回溯"></span>
### 3.1 Create a data trace\-back

Enter the **Data backfill** interface. In the upper\-right corner, click the **New Data Backfill** button to access the new trace\-back interface:

<span id="_3-1-1-回溯任务选择"></span>
#### 3.1.1 Traceback configuration


|Parameters |Note |
|---|---|
|Scope of review ||
|Traceback scope |Select the scope of backtracking tasks:<br><br><br>* Single task: Only a single task can be specified for data backtracking.<br><br>* Single task and its downstream tasks: Select a task for rollback from the rollback\-initiating task and its downstream tasks.<br><br>* Multiple tasks: Select multiple tasks simultaneously to perform rollback operations. It supports selecting tasks across projects; you only need editing permissions for cross\-project tasks. When specifying the scope for multi\-task backtracking, you can also choose **manual input and URL import** as two ways to import tasks.<br><br>   For the URL import method, you must specify a URL link. You must enter an accessible link, and it must return the task ID in JSON array format. After entering the URL, click the **Start Import** button to view the corresponding import task results.<br><br>* Multiple tasks and their downstream tasks: Select multiple tasks simultaneously as rollback initiators. Then, from among the rollback initiators and their downstream tasks, select multiple tasks to roll back.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Downstream tasks: According to the upstream traced instances and dependency settings, obtain the corresponding downstream instances that depend on the upstream, and use these as the downstream traced instances.</div><br> |
|Retrospective tasks |Search\-backtracking tasks:<br><br><br>* You can enter information such as the task name, task ID, data table, HDFS path, and more to search for backtracking tasks.<br><br>* You can also click the **Rollback tasks by upstream** button, select key information such as the upstream task name, task ID, or data table to search, and after specifying the project scope, the system will automatically select the required rollback tasks and their downstream tasks based on dependencies.<br><br>* After selecting a backtracking task, click the **Use Table Lifecycle View** button to view information about the backtracking task, its upstream dependencies, data output, TTL details for the involved tables, dependency settings, and other information. |
|Business business time |Select the start and end business time for backtracking. |
|Backfill pruning |When you select **single task and its downstream, multiple tasks and their downstream** as the backtracking scope, you can configure backtracking pruning as needed. When there are many tasks to be traced back, you can specify trace\-back conditions to filter the scope, so that only tasks meeting the conditions are traced back, thereby improving trace\-back efficiency.<br><br>After selecting **some tasks** using backtracking pruning, you must configure at least one backtracking filter condition. Available filter criteria include **hierarchy, priority, project name, person in charge, dependency type, backtracking suggestion, scheduling type, scheduling frequency**, and more. You may also configure multiple filter conditions as needed, and the relationship between conditions can be either "and" or "or".<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To ensure the connectivity of the backtracking chain, except for the <strong>hierarchy</strong> pruning condition, which supports fixed retrieval of tasks from the first N layers, all other pruning items filter eligible tasks in a top\-down manner based on <strong>hierarchy</strong>. If none of the tasks in the current layer meet the pruning condition, tasks from the next layer will not be retrieved.</div><br> |
|Backtracking rules ||
|Specify schedulable time periods |1. All instances generated by this round of backtracking or rerunning are only allowed to be submitted for scheduling within the specified runtime window.<br><br>2. If the relevant configuration is enabled, the system will only submit the corresponding backtracking or re\-run instances to the engine during the specified time period.<br><br>3. "Scheduling" is not equivalent to "execution"; the system is only responsible for submitting the corresponding instance for scheduling to the engine, and whether it is executed is determined by the engine.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you need to specify the runtime period, the DataLeap product requires the purchase of the service solution for <strong>DataOps Agile Development</strong>, <strong>Lakehouse Integration</strong>, or <strong>Distributed Data Autonomy</strong>.</div><br> |
|Generate instance status (single\-task and multi\-task) |**Single\-task and multi\-task** For instances generated within the backtracking scope, you can select the following statuses:<br><br><br>* Obtain the actual execution result after running.<br><br>* Directly set as successful.<br><br>* Mark as failed immediately. |
|Dependency check (single\-task, multi\-task) |**Single\-task, multi\-task** backtracking scope instances: You can choose at runtime whether to follow upstream dependency settings.<br><br><br>* Follow the dependency settings and start execution only after upstream tasks are completed.<br><br>* If upstream dependencies are ignored and tasks are executed immediately, there may be cases where, during task backtracking, the upstream data is not yet ready, which can result in abnormal output data. |
|Downstream self\-dependent tasks (single\-task, multi\-task, and downstream tasks) |1. Obtain a traceback instance using the complete dependency setup:<br><br>   1. According to the dependency settings, use the instances that depend on upstream backtracking instances as the backtracking instances for this task.<br><br>   2. Due to task self\-dependency, backtracking instances will always retrieve the instance corresponding to the latest business date.<br><br>2. Retrieve backtrace instances after removing self\-dependency:<br><br>   1. After removing self\-dependencies, according to the dependency settings, use the instances that depend on the upstream backtracking instances as the backtracking instances for this task.<br><br>   2. This applies only to downstream self\-dependent tasks with rollback permissions. For downstream tasks that require approval, to ensure data quality, rollback instances are still retrieved according to dependency settings. Each downstream task decides whether to participate in this rollback. |
|Specify a backtracking queue |You can select backtracking\-generated instances based on your actual business situation and decide whether to execute them using other specific queues or compute groups, so that they are distinguished from routine scheduling instances at the queue level and do not affect the execution of normal queue tasks.<br><br><br>* Yes: You need to specify the particular queue and compute group for backtracking in the **Designated Queue** section below.<br><br>* No: No queue or compute group is specified; by default, the same queue and compute group as those used for routine scheduling instances will be used.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Task types such as Shell, Python, Notebook, EMR Doris, EMR StarRocks, EMR Serverless StarRocks SQL, ByteHouse CE SQL, and other similar task types do not support specifying a queue, so there is no need to specify a fallback queue.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When the <strong>backtracking scope</strong> is set to the <strong>multi\-task</strong> type and the tasks include Shell, Python, EMR Doris, or EMR StarRocks task types, the <strong>Specify Backtracking Queue</strong> entry is not displayed. In this scenario, specifying the backtracking queue is not supported.</div><br> |
|Specify a queue |**Designate rollback queue** When "Yes" is selected, you must specify the information for the specific rollback queue. You can select the queue and compute group information that has already been bound in the project console from the dropdown menu at the end. For details about project binding operations, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Scope of specified queue or compute group: The task must support queue or compute group configuration, and the task owner must have the specified queue or compute group permissions; otherwise, traceback will not take effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple tasks under the same engine instance can initiate backtracking. For these tasks, only the same queue or compute group information can be specified.</div><br> |
|Increase backtracking priority |Choose whether to enable raising the priority of backtracking instances:<br><br><br>1. By default, backtracking instances use the lowest priority, that is, D5.<br><br>2. After increasing the backtracking priority, the priority of the backtracking instance is aligned with that of the routine instance of the task, that is, the priority level configured in the scheduling settings. For details, see [Basic Task Attributes](https://docs.byteplus.com/docs/dataleap/basic_attribute_of_task). |
|Maximum parallelism |During this rollback, all included instances are subject to a concurrency limit. If multiple instances under a task that uses dynamic partitioning are rerun, the concurrency must be set to 1. |
|Input parameters |During data backtracking, you can determine whether to enable task input parameter settings as appropriate:<br><br><br>1. If you initiate a task retroactively and use input parameters, you can specify the values of the input parameters here.<br><br>2. The system currently supports input parameters of the **Custom** and **Project** types. After specifying the actual values, the scope in which they take effect is as follows:<br><br>   1. "Custom" type input parameters: Only applies to the "Initiate Retrospective Task".<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This type of parameter can only be set when the backtracking initiating task has custom parameters set during task development.      </div><br>      <br><br>   2. "Project"\-type input parameter: Applies to all tasks under this project that use this project parameter and participate in this trace\-back. |
|Retrospective subscription ||
|Second reviewer |If the project has a requirement for retrospective review, you need to select a reviewer. For details on configuring the review, see [Configuration Review Strategy](https://docs.byteplus.com/docs/undefined/682ad07683179e04f69f189d).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The current DataLeap version does not support this feature.</div><br> |
|Root causes |You can enter the reason for initiating this task rollback here to facilitate future review of the rollback history explanation. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to further narrow the scope of the traceback task or view specific traceback tasks, you can click the <strong>Next (View Task List)</strong> button to preview the traceback tasks. If you do not need to view the task list, you can select <strong>Initiate Directly</strong>, and the system will asynchronously initiate the traceback. Before the instance is fully generated, you can also click <strong>Cancel Approval</strong> in the traceback list as needed to cancel the generation of the traceback instance. For details, see <a href="https://docs.byteplus.com/docs/dataleap/69691#_3-3-%E5%9B%9E%E6%BA%AF%E4%BB%BB%E5%8A%A1%E5%88%97%E8%A1%A8">3.3 Operations on the traceback task list</a>.</div>


<span id="a87ac078"></span>
#### 3.1.2 Preview of retrospective tasksx

On the backtracking task preview page, you can view the list of tasks that meet the above backtracking configuration criteria.


1. Retrospective task filter

   When there are many eligible backtracking tasks, you can filter them by the following types: **backtracking permissions, task type, backtracking suggestions, scheduling type, dependency type, frequency, task hierarchy, task name, owner, associated project**, and more.

2. Select number of tasks to backtrack

   The list of eligible backtracking tasks is displayed here. Simply select the specific tasks you want to backtrack.

3. After checking off the tasks, click the "**Next**" button to enter the final backtracking plan confirmation screen.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the task data rollback recommendation is to select <strong>cautious rollback</strong>, a second confirmation for the rollback is required, and the corresponding rollback reason must be provided. When a rollback is initiated by someone other than the task owner, the task owner must also perform an approval operation.</div>


<span id="_3-1-2-回溯实例确认"></span>
#### 3.1.3 Retrospective plan confirmation

When the retrospective plan is confirmed, you can count the specific number of instances generated by the selected retrospective task.


1. For each task, you can click the **View** button in the list of generated rollback instances to continue selecting the business time range that needs to be rolled back.

2. Alternatively, go to **Backfill instance advanced settings** to filter instances. You can select from the following two methods:

   1. Retain only backtracking instances that meet the criteria

   2. Remove eligible backtracking instances

      Continue selecting parameters such as backtracking permissions and business time range to filter instances.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69aba9520ed44700aa405aa828b70c4b~tplv-goo7wpa0wc-image.image) </span>


After all backtracking instances have been confirmed, click the **Confirm Backtracking** button to complete the data backtracking task creation.

<span id="_3-2-回溯任务筛选"></span>
### 3.2 Backtracking task filtering

You can quickly locate the specified traceback task by filtering and searching. The specific filter and search items are:


* Filter options: initiation time, lookback period, user filter.

* Search items: traceback ID, initiating task ID/name, downstream task ID/name, initiator, traceback approver.

* Reset: The reset button can clear all filter options, and the list will display all retrospective tasks under the project.

* Quick filter: Select **My retrospectives** to filter retrospectives for which the current account is the responsible person.


<span id="_3-3-回溯任务列表"></span>
### 3.3 Operations on the traceback task list

Here, you can view a list of backtracking tasks under the project that meet the specified criteria. For each initiation, you can see the backtracking ID, initiation time, initiating task ID, the business time associated with the backtracking, initiator, backtracking configuration, reason for the backtracking, and backtracking status.

In the Traceback status bar, you can perform the following actions:


* View traceback details:

   You can click the **Traceback ID** button to view in depth the **traceback details** of this traceback task, where you can view the specific task list and instance run details.

* Cancel approval:

   1. If the data backtracking initiation method is selected as **Direct initiation**, a backtracking instance will be generated asynchronously.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/624fb9ae0d7f41a9b13f78e067282617~tplv-goo7wpa0wc-image.image) </span>

   2. In the backtracking list, when the status of a backtracking instance is **Generating**, you can click the **Cancel approval** button. After confirming in the second **Confirmation** dialog, any instances that have not been generated will be canceled, and only the generated part of the instances will be executed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdc5d85999744092a9640a5f980cdc68~tplv-goo7wpa0wc-image.image) </span>

* Terminate downstream approvals:

   In the list of **initiated** retrospectives, when a retrospective task is pending approval from the task owner, the initiator can select **terminate downstream approval** to cancel the retrospective.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a23cfb13e33f437eb81bc45fc3d709d5~tplv-goo7wpa0wc-image.image) </span>

* Terminate backtracking:

   After backtracking instances are generated and running, you can, based on your actual business scenario, click the **Terminate Backtracking** button as needed to terminate instances that are running or have not yet started. You can view the actual running status of each instance in **Backtracking Details**. The following:

   * For **running** instances, after the rollback is terminated, the instance status is displayed as **Terminated (System Terminated)** .

   * For instances in **Waiting to Run**, after a rollback that results in termination, the instance status will be displayed as **Terminated (Expired Termination)** .

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23c3dc228209431ea4e595570e9a05ce~tplv-goo7wpa0wc-image.image) </span>

* Reuse: Click the reuse button under the **Operation** column to create another data backtracking task based on the previous task backtracking configuration.

* Revoke: In the **pending review** rollback list, when a rollback task requires **review**, the rollback initiator can click the **revoke** button under the **action** column to cancel this rollback operation.


<span id="_4-收到的回溯列表"></span>
## 4 The list of received tracebacks

Here, you can view the tasks under the project, all received traceback records, and the system supports careful review and approval operations for tracebacks.

You can quickly filter by initiation time and task status, and also search by trace ID, initiation task ID or name, ID or name of downstream tasks included in the trace, trace initiator, or approver.

<span id="_4-1-回溯任务审批场景："></span>
### 4.1 Retrospective task approval scenarios:


1. For backtracking tasks, select the **Cautious backtracking—task owner approval** method in **scheduling settings**. For detailed operation instructions, see [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).

2. If the retrospective initiator is not the task owner, only the task owner can perform retrospective approval.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">In the task scheduling settings, it is recommended to select the <strong>cautious rollback\-\-\-task owner approval</strong> mode. However, if the rollback initiator is the same as the task owner, no additional approval is required, and the rollback is approved by default.</div>


2. <div data-tips="true" data-tips-type="tip">When the task owner agrees to a rollback, if it is necessary to <strong>specify the runtime period</strong>, the DataLeap product must purchase service solutions for <strong>DataOps Agile Development</strong>, <strong>Lakehouse Integration</strong>, or <strong>Distributed Data Governance</strong>.</div>



<span id="04862470"></span>
### 4.2 Cautious rollback of approval operations

Cautious retrospective approvers can perform retrospective approval in the list of received **retrospective items** by following these steps:


1. Search for sensitive retrospective tasks requiring approval based on the **retrospective task ID** provided by the initiator.

2. Click **traceback task ID** to go to the traceback details page.

3. Under the **Action** column in the backtracking task list, click the **Approve** or **Reject** button to perform the approval operation:

   * Approval: Provides two approval options, "**Approve and generate a backtracking instance**" and "**Approve but do not generate a backtracking instance**" In the backtracking confirmation window, you can also configure settings for the backtracking instance, such as the **maximum number of concurrent instances, designated scheduling periods, backtracking priority, and required task parameters**, as needed.

   * Reject: Click the **Reject** button to end the current rollback operation.


<span id="_5-待复查的回溯列表"></span>
## 5 List of tracebacks pending review

You can view all data trace records requiring review for this project here. Reviewers can perform review and approval actions upon logging in.

Supports quick filtering by initiation time and review status. You can also search by trace ID, initiating task ID or name, downstream task ID or name that is included in the trace, and the initiator or reviewer of the trace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current DataLeap version does not support this feature.</div>


<span id="_5-1-复查前提条件"></span>
### 5.1 Review prerequisites

The project requires setting a **data rollback review policy**. Any data rollback that is initiated will only be executed after it has been approved by review personnel. For details about configuring the retrospective review policy, see [Configuration Review Strategy](https://docs.byteplus.com/docs/undefined/682ad07683179e04f69f189d).

<span id="_5-2-复查操作"></span>
### 5.2 Review operations


* Approve: In the pending review interface, the reviewer clicks the **Approve** button in the operation column to complete the approval.

* Reject: The reviewer enters the pending review interface and clicks the **Reject** button in the Actions column to reject this review.

* Revoke: The rollback initiator enters the pending review interface, selects the pending review tasks, and clicks **Revoke** to cancel this rollback review.


<span id="_5-3-查看回溯实例"></span>
### 5.3 View traceback instances

After the review is approved:


* Go to the **Instance O&M** interface, and search for backtracked instances using [4 Instance filtering search](https://docs.byteplus.com/docs/dataleap/69652#_2-%E5%AE%9E%E4%BE%8B%E7%AD%9B%E9%80%89%E6%90%9C%E7%B4%A2) method.

* Alternatively, on the **Data Backtracking Initiation** interface, click **View Details** in the **Status Bar** of the backtracking list to enter the backtracking multi\-task list. Then, click **View Details** in the **Status Bar** of the specific task to open the run details window. Next, click **Instance operation entry point** to access the instance O&M interface, where you can locate and view the progress of the specific backtracking task.
