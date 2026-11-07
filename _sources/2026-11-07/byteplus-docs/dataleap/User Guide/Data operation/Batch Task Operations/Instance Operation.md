---
title: "Instance Operation"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/instance_operation"
---

Displays Run Instance Information for the task, allowing real\-time viewing of instance state changes. Exceptions can be quickly located through Dependencies, Diagnostics, and Logs, and you can perform actions such as Rerun, Set to "Success", or Terminate on the instance.

<span id="d75ef011"></span>
## 1 Notes and limitations


* For the Instance diagnostics feature, the current DataLeap version does not support this feature.


<span id="7e4f0d41"></span>
## 2 Use prerequisites

The Data Development periodic scheduling task has been submitted and released. See details [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

<span id="_1-进入实例运维"></span>
## 3 Enter instance operations


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Under the corresponding project, click the **Maintenance \> Batch Task Operations \> Instances** interface.


<span id="_2-实例筛选搜索"></span>
## 4 Instance filtering search

The instance list is aggregated by task name and business time, displaying the related information of the latest instance for each business time. By filtering and searching, you can quickly find the specified instance. The specific filtering and searching items are:


* Filter items: Business time, Task type, State, Scheduled Time, Start time, Run type, Storage directory, Scheduling interval, Owner, Task tags, Priority, Scheduling resource group, Computing resource group, and Integrated Resource Group.

* Search items: task ID/name, Code, configuration parameters, project parameters, and ID list.

   You can choose Code, Configuration parameters, Project parameters, and ID list in the dropdown menu.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/692c0e67191940f7bea745076b71fdaf~tplv-goo7wpa0wc-image.image) </span>

* Reset: The Reset button clears all filtering options, and the List displays all Task instances under the Project.

* Quick filtering:

   * My Tasks: Show instances of tasks for which the current account is the owner.

   * My failed tasks: Tasks for which the current account is the owner and whose instance's run state is **Failed**.

   * My unfinished tasks: Tasks for which the current account is the owner, and whose state is not a **failed** or **successful** instance.


<span id="_3-查看任务实例列表"></span>
## 5 ·View the task instance list

<span id="_3-2-单实例操作列"></span>
### 5.1 The single instance action column


|Functions |Note |
|---|---|
|DAG |Go to the instance dependency page to view the upstream and downstream relationships of the instance. You can view them in either graphical or list mode.<br><br>See the [View the instance DAG](https://docs.byteplus.com/docs/dataleap/69652#_3-4-%E6%9F%A5%E7%9C%8B%E5%AE%9E%E4%BE%8Bdag)Description below. |
|Rerun |In the instance rerun window, you can perform a rerun action on selected successful or failed instances and configure configuration items such as **Specify schedulable time**, **Dependency check**, **Specify rerun queue, and Specify rerun scheduling resource group**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Specify schedulable time, this function is not supported in the current version of DataLeap.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the code for a failed instance is modified and committed for release in the Data Development interface before rerunning, both the rerun and any instances that have not yet run will use the latest code to execute the task.</div><br> |
|View Log |Go to the Instance log page to view the log overview, scheduling log, engine execution log, lag analysis, instance operation log, and other information for instance.<br><br>For data integration task types, you can also view scheduling logs, specific execution logs, task run event information, and other related information. See details [DataSail log viewing and diagnostics](https://docs.byteplus.com/docs/undefined/68c04b5ad4b05a04fd3d9fcb).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Task run events include event information from both the task startup process and the running process. These events may involve changes in task state, such as task failure, restart, and other event types.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Batch task scheduling log data is retained for 60 days. You can view the corresponding scheduling log details within 60 days.</div><br> |
|Data Integration Service Monitoring |The Batch Integration task type supports viewing cloud monitoring details for the task. Click the **Data Integration Service Monitoring** button to enter the Cloud Monitor interface, where you can view monitoring metrics such as read\-write metrics and Resource Group usage for the integration task. |
|Edit task |Enter the **Task development** interface, then make further changes to the task. |
|Set to "Success" |You can perform the Set to "Success" action on instances that have not yet finished running and on failed instances.<br><br>Instances that have not finished running: Click **More\-Set to "Success"**  to stop the instance from running. The instance state changes to **Successful.** <br><br>Failed instances: Click **More \- Set to "Success",**  and the instance state will change from Failed to **Successful.**  |
|Terminate |You can perform the Terminate action on instances that have not yet finished running.<br><br>Instances that have not yet finished running: Click **More\-Terminate** to stop the instance from running. The instance state will change to **Terminate.**  |
|Logs |Operation log for the current instance, for example, records of actions such as rerun, setting the instance to "Success", and other operation records. |


<span id="_3-3-批量操作实例"></span>
### 5.2 Batch operate instances

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a3418b2df1447dea2cd92924ef7f7cf~tplv-goo7wpa0wc-image.image) </span>

In the Instance list, you can select multiple instances and use the Action bar below to perform batch operations, such as **Terminate, Rerun, Set to "Success", Export**, and more.

<span id="_3-4-查看实例dag"></span>
### 5.3 View the instance DAG

In the instance list, click **Task name** or the **Instance DAG** button in the Action column to enter the DAG view.

<span id="_3-4-1-血缘展示支持以下两种模式："></span>
#### 5.3.1 The two modes supported by lineage display


1. DAG mode:

   1. For all DAG diagrams, you can choose to display them centered or scaled to a specified percentage.

   2. Click the **gear** icon on the right to customize the aggregation node settings. When the number of sibling nodes displayed in the interface is greater than or equal to N (where N is customizable), the DAG can be presented in aggregation node mode.

   3. Right\-click the instance DAG diagram to perform actions such as instance rerun, data backfill, terminate, set to "Success", view log, view instance, and view task.

   4. Click the  **+**  icon at the upper and lower boundaries of the DAG diagram to manually expand the upstream and downstream dependencies of the task.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55305a0c256244ecbcc9c932d574f417~tplv-goo7wpa0wc-image.image) </span>

2. List mode:

   * Lineage type: Select to display upstream or downstream lineage, and input the number of lineage levels to show. By default, 1 level is displayed. The list below will display the upstream and downstream lineage list.

   * Lineage list search: You can filter the displayed hierarchy, state, task owner, or task type, or directly enter the task name, ID, or project name to search for instances related to the lineage.

   * Batch operate tasks: You can select multiple tasks and click the **Rerun, Terminate, Set to "Success"**  button in the upper right corner to batch operate the selected tasks.

   * Operation column: In the operation column, you can rerun a single instance, terminate, set to "Success", edit a task, view historical run time, and view the operation log.

   * Export to Excel: You can export the displayed lineage list to a local Excel file.


<span id="_3-4-2-实例详情"></span>
#### 5.3.2 Instance details

You can view the run diagnostics, run log, properties, and operation log, and check whether the code matches expectations for scheduled task instances in the production environment.


* Run log: View the log overview and log details of the instance.

* Properties: Displays the name, owner, state, start/end time, scheduling interval, and other basic information of the current instance.

* Operation log: Actions you perform on an instance, such as Terminate, Rerun, or Set to 'Success', are all recorded in the operation log to facilitate subsequent tracing of operation records related to backfill tasks.

* Code: Batch tasks, except for Data Integration synchronization tasks, can display their logical code.
