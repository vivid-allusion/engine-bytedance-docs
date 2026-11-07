---
title: "Viewing orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View_orchestration_plans"
---

You can view an orchestration plan to learn about task execution progress and related information.

<span id="ctjCpcsb"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. On the "CloudOps Orchestration" page, click the "orchestration plan" tab.

5. Click the target plan name to view the information in the following table.

   
   |Parameter |Description |
   |---|---|
   |Overview |Click the "Overview" tab to view the basic information and task template of the orchestration plan.<br><br><br>* Basic information: includes the plan name, plan ID, and execution mode.<br><br>* Task template: All task templates used in this orchestration plan, including the name of each template and the input/output parameters corresponding to its task objectives. |
   |execute |* Click the "execute" tab to view all execution records of the orchestration plan.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only one execution record exists if you set "Mode" to "Execute immediately".   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each time a task is triggered for execution, an execution record is generated.   </div><br>   <br><br>* In the "Actions" column of the target execution record, click the "view details" button to view the execution details of the record, including the basic information, execution log details, and list of loop tasks.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only tasks with loop tasks (executed in batches) support viewing the loop task list. For example, "batch instance operations" and "batch associate key pair".   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the "Actions" column of "Circular task list", click the "View subtask" button to view the details of the subtasks.   </div><br>    |
   

6. After the task is successfully executed, you can go to the relevant cloud product page to view the execution results.

   For example, you can go to the "Instances" page and check whether the instance is running as expected after the operating system is changed.
