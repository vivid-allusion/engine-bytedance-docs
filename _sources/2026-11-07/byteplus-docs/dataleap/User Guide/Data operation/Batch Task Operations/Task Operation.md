---
title: "Task Operation"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/task_operation"
---

Displays offline tasks that are already online under the project. You can view task dependencies and changes in runtime duration as needed, perform maintenance operations such as data backtracking, monitoring configuration, and other related actions, and manage task status by enabling, disabling, and other status operations.

<span id="_1-进入任务运维"></span>
## 1 Go to Task Operations and Maintenance


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Under the corresponding project, go to the **Operations Center \> Batch Task Operations \> Tasks** page.


<span id="_2-任务筛选搜索"></span>
## 2 Task filtering and search

You can quickly find the specified task by filtering and searching. The available filter and search options are:


* Filter options: owner, storage directory, task status, scheduling type, task type, runtime monitoring, task mode (distinguishing between single\-node task mode and workflow task mode), task tags, scheduling cycle, priority level, engine type, and baseline monitoring

* Search items: task ID/name, Code, configuration parameters, project parameters, and ID lists.

   * You can select Code, configuration parameters, project parameters, and ID list search from the dropdown menu.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b12e4bff12f640b194c631e901281802~tplv-goo7wpa0wc-image.image) </span>

* Reset: The reset button clears all filter options, and the list displays all tasks under the project.

* Quick filter: Select **My tasks** to filter tasks for which the current account is the responsible person.


<span id="_3-查看任务列表"></span>
## 3 View task lists

<span id="_3-1-任务列表自定义展示"></span>
### 3.1 Custom display of task lists

Click the **List item settings** button to access the configuration for customizing the display columns in the task list.


* List items: Click **All** to display all list parameters on the interface. You can also customize your selection.

* Frozen columns: By default, the two columns, **task name and operation column**, are frozen.

* Activity column: You can customize the order of selected list items by dragging, or delete this activity column.


<span id="_3-2-单任务操作列"></span>
### 3.2 The single task operation column


|Functionality |Note |
|---|---|
|Task DAG |On the task dependency display page, you can view the upstream and downstream dependencies of tasks. The lineage display supports two viewing modes: DAG and list.<br><br>For details, see **View the task DAG diagram**. |
|View instances |Navigate to the instance maintenance list to view the running instance for the task. For details, see [Instance Operation](https://docs.byteplus.com/docs/dataleap/69652). |
|Data retrospective |When a task is started, you can backtrack data. As needed, you can rerun the current task or supplement missing data. For details, see [Data backfill](https://docs.byteplus.com/docs/undefined/689b0e2d1393e804f3ca3043). |
|Edit |Enter the **Task Development** interface and edit and modify the task again. |
|Copy |According to the selected task configuration, copy the corresponding task to the specific directory within this project. |
|Move |Move the selected tasks to the specified directory under the specified project. |
|Exchange |Go to the task swap configuration page. By performing this operation, you can swap two deployment tasks with the same frequency within the same project. The specific exchange effect is as shown in the following figure:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42910769d37f427082bd80644ac4d7f4~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>1. <div data-tips="true" data-tips-type="tip">Within the same project, two tasks that are both online and enabled can be exchanged.</div><br><br><br>2. <div data-tips="true" data-tips-type="tip">For task exchange, only the task ID and dependency settings are exchanged; other configurations remain unchanged.</div><br><br><br>3. <div data-tips="true" data-tips-type="tip">Swap operations are not supported for workflow tasks.</div><br> |
|Edit tags |You can define custom tags to identify categories of tasks, enabling quick search and filtering. Changes take effect immediately, and there is no need to redeploy tasks.<br><br><br>* Select the tag group to which the project belongs and the corresponding tag information from the dropdown. Multiple tag groups can be added.<br><br>* If there are no available tag groups, you can go to **Project Console** \-\-\-\> **Tag Management** to create or add a tag group.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The current DataLeap version does not support this feature.</div><br> |
|Edit the responsible person |Change the assignee of the current task, and in the popup window, select another user from the current project. For details about adding project users, see [Manage Member Information](https://docs.byteplus.com/docs/dataleap/manage_project_member). |
|Modify queues |Currently, only LAS engine type jobs support modifying the queue. In the popup window, select the queue information required for running the task from the dropdown list. |
|Modify priority |Modify the priority of the current task. Only tasks with **D3~D5** priority can be modified here. For higher\-priority tasks, namely "**Core (D2)** " and "**Super Core (D1)** ", you must go to the Data Governance Platform to adjust their priority.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The current DataLeap version does not support this feature.</div><br> |
|Operations monitoring |View the runtime monitoring already configured for this task. At the same time, you can use this entry point to add new runtime monitoring to the current task. For detailed instructions, see [Monitoring rules](https://docs.byteplus.com/docs/dataleap/monitor_rules). |
|Quality monitoring |Go to data quality and configure quality monitoring for the current task. For details, see [Configure Hive Template Rules](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules). |
|Add to baseline |Add the current task to the existing baseline monitoring. For details on baseline creation, see [Baseline management](https://docs.byteplus.com/docs/undefined/689b106ca5abd9051f272182).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Monthly scheduling task, weekly scheduling task, and minute\-level scheduling task cannot be added to the baseline for baseline monitoring.</div><br> |
|Use/do not use default monitoring |If the project sets the system\-provided default monitoring as the project default, this operation allows you to quickly assign or remove the default monitoring for specified tasks. |
|Alarm ACK settings |Go to the alarm ACK settings page for the current task, and configure alarm suppression for the specified monitoring item as needed. During the alarm suppression period, if the task triggers an alarm for the specified monitoring item, the system will automatically suppress the alarm and will not send it to the alarm recipients. |
|Historical run times |View the historical changes in the runtime duration of this task. The historical data viewing range varies depending on the task frequency.<br><br><br>* Monthly, weekly, or daily tasks: Changes in runtime duration over the past 30 days.<br><br>* Hourly tasks: Changes in runtime duration over the past 7 days.<br><br>* Minutes: Changes in runtime duration over the past 3 days. |
|Message notifications |When a task is changed or you need to send a message to the person responsible for the task, you can use the **Message Notification** feature to send the required information to the corresponding person in charge. For detailed configuration instructions, see [Message notifications](https://docs.byteplus.com/docs/dataleap/task_operation#jump). |
|Export downstream |View the downstream tasks of this task, including tasks that are directly or indirectly dependent on it. You can export them to an Excel file as needed. |
|Turn off/turn on |The task has been enabled. When routine execution is no longer required, you can click **More \- Close** to close it. For closed tasks, when you need to schedule them for routine execution again, you can click **More \> Enable**. |
|Delete |For tasks that are no longer needed, you can click **More\-Delete** to delete them. |


<span id="_3-3-批量操作列"></span>
### 3.3 The batch operation column

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b087dabb284cf598781d9103f0a01e~tplv-goo7wpa0wc-image.image) </span>

In the task list, you can select multiple tasks and use the action bar below to perform batch operations, such as **enabling, disabling, deleting, copying, moving, exporting to downstream, editing (changing assignee, updating tags), running monitoring (using or not using default monitoring, adding monitoring rules, adding baseline monitoring, changing priority), and data backtracking**.

<span id="jump"></span>
### 3.4 Message notifications

Click the **Message Notification** button in the **Operation** column. This will take you to the message notification configuration page. Configure the following parameters:


|Parameters |Note |
|---|---|
|Notification content |Enter the message content you need to inform the task owner or project administrator. |
|Notification formats |You can choose two notification methods: **email**.<br><br><br>* Email: The notification content will be sent to the notification recipient by email;<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The relevant task information will be displayed in the body of the email. Due to underlying service limitations, a maximum of 1,000 rows can be displayed at present.   </div><br>    |
|Notification recipients |Send message notifications to the person responsible for the task or the project administrator of the project to which the task belongs. |
|Message recipient |Select which task owners or administrators will receive the message. Batch selection is supported. |


<span id="_3-5-查看任务dag"></span>
### 3.5 View task DAGs

In the task list, click the **task name**, or click the **task DAG** button in the **operations** column to enter the DAG display interface.

<span id="_3-5-1-血缘展示支持以下两种模式："></span>
#### 3.5.1 Lineage display supports the following two modes:


1. DAG：

   * The display of percentage operations in DAG diagrams can be customized.

   * Right\-click the task DAG diagram to view instances, enable or disable tasks, edit tasks, perform data backtracking, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c22ae4e425a44b62aa9c9879db90e240~tplv-goo7wpa0wc-image.image) </span>

   * Click the “ **+** ” icon on the upper or lower boundary of the DAG graph to manually expand the upstream and downstream dependencies of the task.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e643cb88f0df41228035bdbdbd19caab~tplv-goo7wpa0wc-image.image) </span>

2. List mode:

   * Lineage type: Select to display upstream or downstream lineage, and enter the number of lineage levels to display. By default, 1 level is displayed. The list below will then show the corresponding upstream and downstream lineage list.

   * Lineage list search: You can filter the displayed hierarchy, task owner, or task type, or enter a task name, ID, or project name to search for tasks related to lineage.

   * Enable or disable multiple tasks: You can select multiple tasks and click the **Enable, Disable** button in the upper right corner to enable or disable them in batch.

   * Export to Excel: You can export the displayed lineage list to a local Excel file.


<span id="_3-4-2-任务详情"></span>
#### 3.5.2 Task details

You can view the properties and operation logs of periodic tasks in the production environment, and check whether the code meets expectations.


* Properties: Displays basic information for the current task, including name, person responsible, scheduling status, execution time, and task type.

* Operation logs: Actions you perform on tasks, such as enabling, disabling, or rolling back tasks, are all recorded in the operation log to facilitate subsequent review of task operation records.

* Code: For offline tasks, except for data integration synchronization tasks, the task's logic code can be displayed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/797360a3b51a4cd8891189b8c7a846dd~tplv-goo7wpa0wc-image.image) </span>
