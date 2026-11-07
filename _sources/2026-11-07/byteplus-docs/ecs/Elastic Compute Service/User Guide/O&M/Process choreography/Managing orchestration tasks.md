---
title: "Managing orchestration tasks"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks"
---

This topic describes how to create and manage orchestration tasks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed the [preparations](https://docs.byteplus.com/en/docs/ecs/Preparation).

<span id=".5Yib5bu65rWB56iL57yW5o6S5Lu75Yqh"></span>
## Create an O&M orchestration task


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. Click the "Orchestrate tasks" tab.

5. Click "Create orchestration task" and configure the parameters described in the following table.

   
   |The parameters​. |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Specify the name of the orchestration task. |Creating custom images |
   |Role<br><br> |Select a role with permission to perform operations on the service for which the orchestration task is created. The default role is "CustomRoleForOOS", which has full read and write access to ECS.<br><br>You can also click the "Role" drop\-down list to select a different role. The selected role must have permissions to perform operations on the corresponding resource.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can add task steps and then click the "View required task permissions" button to view the permissions needed for the role executing this orchestration task.</div><br> |Retain the default value.<br><br> |
   |Project |You can add orchestration tasks to a project and manage them by project, which helps maintain resource independence and data security. For more information about project management, refer to [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to easily search and aggregate your resources. For more information about tags, refer to [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   |**Execution mode** |||
   |Execution mode<br><br> |For the job execution modes, the following options are available:<br><br><br>* **Execute immediately**: After the job is created, it is executed for one time immediately.<br><br>* **Timed execution**: The task is executed automatically once at the time you specify.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The execution time must be accurate to the minute and must not be earlier than the current time.   </div><br>   <br><br>* **Periodic execution**: The task is executed automatically on a cycle starting from the specified start time, at intervals you specify (in minutes, hours, or days), and stops automatically at the specified end time. You need to configure the following information:<br><br>   * **Repeat cycle**: Specify the interval at which the job is executed repeatedly. The repeat interval must be longer than the timeout period. Value:<br><br>      * by minute: The minimum interval is 5 minutes.<br><br>      * by hour: The minimum interval is 1 hour.<br><br>      * by day: The minimum interval is 1 day.<br><br>   * **Start time**: Specify the time when the periodic job is first executed. This time must be later than the current time.<br><br>   * **Stop time**: Specify the time when the periodic task stops. The task automatically stops at this time.<br><br>      * If the task is not being executed at the stop time, it automatically stops and will never be executed again.<br><br>      * If the job is being executed at the stop time, it automatically stops after the execution is complete and will never be executed again.<br><br>      * If the interval between the stop time and the start time is less than one repeat cycle, the task is executed only once.<br><br>   * **Time zone**: Fixed to `GMT +08:00` (China Standard Time).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The execution interval is independent of the actual execution duration of the task and is calculated based on the "Start time" you specify. For example, if the start time for a job is <code>2022-12-20 11:00:00</code>, the repeat cycle is 1 hour, and the duration of the first execution is 3 minutes, the second execution starts at <code>2022-12-20 12:00:00</code>.   </div><br>    |Execute immediately<br><br> |
   |**Task step** |||
   |Add step<br><br> |Add the steps you want to execute one by one in your desired order.<br><br><br>1. Click the "Add step" button, and select the required step in the pop\-up window.<br><br>   > After you add a step, the system automatically assigns an ID to the step, making it easier to distinguish steps with the same feature. For example, the ID for a step that creates an ECS instance is id:437a.   <br>   <br><br>2. Click the "Add" button to complete the addition.<br><br>3. Configure parameters for each step.<br><br>   You can configure input and output parameters for each step. Once a step is executed, the relevant information is displayed. For parameters supported by each step, see [Summary of orchestration steps](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps).<br><br>   1. Select the "Input" tab and configure the input parameters required for step execution. Parameter sources:<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The first step only allows you to manually enter parameter values.      </div><br>      <br><br>      * **Custom input**: Select or enter parameter values.<br><br>      * **From the preceding task**: You can select the output parameter values of the preceding steps in the O&M orchestration as parameter values.<br><br>   2. Select the "Output" tab to view information about the parameters returned after the current step is executed.<br><br>4. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_778d25c3b299f8ab8b2f07913a3ffff4.png) </span> icon to add more steps based on your business requirements.<br><br>   > You can reorder the added steps by dragging them. |Create ECS instances<br><br> |
   

6. Click the "Create" button. After the creation, the system will automatically redirect you to the orchestration list page and start executing the orchestration task based on the execution method you configured.

7. You can click the target task name to view task execution information. For more information, see [View task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF).


<span id=".5p-l55yL5Lu75Yqh6K-m5oOF"></span>
## View task details

On the task details page, you can view task information, the execution status of each task step, and historical logs, including logs of each step and global logs of the orchestration task.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. Click the target task name to view the information described in the following table.

   
   |Parameter |Description |
   |---|---|
   |Overview |Click the "Overview" tab to view the basic information, mode, and task template of the orchestration task.<br><br><br>* Basic information: includes information such as the task name, role, task ID, and associated project.<br><br>* Mode: includes execution mode and execution time.<br><br>* Task template: All task templates used in this orchestration task and the names of the task templates. |
   |execute |* Click the "execute" tab to view execution records of the orchestration task.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only one execution record exists if you set "Mode" to "Execute immediately" or "Timed execution".   </div><br>   <br><br>* Click the "View details" button to view task execution details, including the execution status of all steps in the current task. Click any step to view the basic information, input/output arguments, loop task list, and log details for that step.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only tasks created in the orchestration console support viewing input/output arguments.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only tasks that include loop tasks (executed in batches) enable you to view the loop task list, including the execution objects and status of the loop tasks. Examples include "batch instance operations" and "batch key pair association." Click the "View subtask" button to view the details of the subtasks.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the task status is <strong>Success,</strong> all subtasks succeed.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the task status is <strong>Fail</strong>, all subtasks fail.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the task status is <strong>Partial Failure</strong>, at least one subtask succeeds and at least one subtask fails.   </div><br>    |
   |Log |Click the "Log" tab to view the global execution log for the orchestration task. |
   

5. After the task is successfully executed, you can go to the relevant cloud product page to view the execution results.

   For example, you can go to the "Instances" page and check whether the instance is running as expected after the operating system is changed.


<span id=".5YWL6ZqG5rWB56iL57yW5o6S5Lu75Yqh"></span>
## Clone an orchestration task

You can use the cloning feature to replicate an existing task, including its execution method, steps, and parameters. You can also adjust the configuration based on the original task, facilitating efficient task management and execution.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. Click the "Clone" button in the "Actions" column of the target operations orchestration task to access the "Clone task" page.

5.  **(Optional)**  Adjust the task information based on your needs, refer to [Create an orchestration task](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5Yib5bu65rWB56iL57yW5o6S5Lu75Yqh) for parameter descriptions.

6. Click the "Clone" button to complete the cloning operation.

7. After the task is successfully cloned, the system will automatically redirect you to the orchestration list page and immediately start executing the orchestration task.

8. You can click the target task name to view task execution information. For more information, see [View task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF).


<span id=".5Y-W5raI5rWB56iL57yW5o6S5Lu75Yqh"></span>
## Cancel an orchestration task

You can manually cancel orchestration tasks, canceling all current and subsequent executions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can cancel only orchestration tasks in the <strong>Waiting for execution</strong> or <strong>in progress</strong> status.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, select "Maintenance & Monitoring \> Orchestration" to go to the orchestration list page.

4. Click the "Cancel" button in the "Actions" column of the target orchestration task.

5. After you confirm the target orchestration information in the pop\-up window, click the "Cancel" button to complete the operation.


<span id=".5Yig6Zmk5rWB56iL57yW5o6S5Lu75Yqh"></span>
## Delete an orchestration task

You can delete orchestration tasks that are no longer needed to reduce redundant information.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You cannot delete orchestration tasks in the <strong>Waiting for execution</strong> or <strong>in progress</strong> status.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. Click the "Delete" button in the "Actions" column of the target orchestration task.

5. After you confirm information of the orchestration task you want to delete, click the "Delete" button to complete the operation.
