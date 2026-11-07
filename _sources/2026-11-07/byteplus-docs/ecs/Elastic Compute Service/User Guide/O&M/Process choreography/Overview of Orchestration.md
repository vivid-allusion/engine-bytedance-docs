---
title: "Overview of Orchestration"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration"
---

Orchestration is a process\-based automated O&M service for cloud products. It allows you to orchestrate task workflows based on your business requirements for auto\-execution. You can also centrally manage these tasks and view their execution progress and results.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

Orchestration is often used in relatively complex cloud product O&M scenarios. It can orchestrate multiple operations into a single process for unified execution, addressing the inefficiency and fragmentation issues of manual execution.

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Concept |Description |
|---|---|
|Step |The basic actions that can be executed with the orchestration feature, which are generally operations and O&M on cloud products, such as ECS instance creation, starting, and stop actions, and calling cloud assistant. You can orchestrate multiple steps into a complete workflow. You can view details of currently supported steps in [Summary of orchestration steps](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps). |
|Role |A role is a type of identity in the IAM system. Its permissions are defined by the attached policy. For more information about roles, see Role management. The orchestration service will assume the role you select to obtain permissions to access the resources under your account. You can create roles with permissions to execute orchestration tasks. For detailed operations, refer to [Preparations](https://docs.byteplus.com/en/docs/ecs/Preparation). |
|Alert trigger |An alert trigger is an automated response mechanism designed for metric anomalies or risks. When the metrics or status of a monitored object reaches a predefined exception threshold or meets risk conditions, an alert is generated, which then triggers predefined follow\-up operations to enable automated O&M. |
|Event triggers |An event trigger is an automated response mechanism designed for specific events. When a specific event occurs, the system automatically initiates predefined operations to enable automated O&M. Specific events can be detected risks in GPU operation or pending responses for instance redeployment triggered by disk anomalies. |


<span id=".5L2_55So5rWB56iL"></span>
## Procedure

<span id="jBfpmAWf"></span>
### **Use preset steps to create an orchestration task**

By combining various preset steps, you can achieve process\-based automated O&M. The following table describes the procedure.


|Method for initiating O&M orchestration |Procedure and description |
|---|---|
|Proactive O&M orchestration |O&M orchestration is proactively initiated and executed based on preset rules or detection results, independent of triggers from external events or alerts. Its core lies in "proactive prevention and proactive O&M."<br><br><br>1. [Preparations](https://docs.byteplus.com/en/docs/ecs/Preparation)<br><br>   Grant read and write permissions on ECS instances to your account.<br><br>2. Create a custom template or view steps to orchestrate an O&M task (**optional**)<br><br>   * [Create a custom template](https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates)<br><br>      If the current preset public templates do not meet your business requirements, you can create a custom template.<br><br>   * [View steps to orchestrate an O&M task](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps)<br><br>      Understand the purpose, input and output parameters, and other relevant aspects of each step of your task. This helps you accurately and appropriately plan the steps when you create an orchestration task.<br><br>3. [Create an orchestration task](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5Yib5bu65rWB56iL57yW5o6S5Lu75Yqh)<br><br>   Add preset steps to create a task. This enables process\-based automated O&M.<br><br>4. [View task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF)<br><br>   Learn about task information and the execution status of each step of the task. |
|Passive O&M orchestration |O&M orchestration is passively triggered and executed when external (CloudMonitor) events or alerts meet specific conditions. Its core lies in "on\-demand responsive and automated O&M".<br><br><br>1. [Preparations](https://docs.byteplus.com/en/docs/ecs/Preparation)<br><br>   Grant read and write permissions on ECS instances to your account.<br><br>2. [Summary of orchestration steps](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps) (**optional**)<br><br>   Understand the purpose, input and output parameters, and other relevant aspects of each step in your plan. This helps you accurately and appropriately plan the steps when you create an orchestration plan.<br><br>3. [Create an orchestration plan](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan)<br><br>   Add preset steps to predefine the O&M orchestration workflow for a specific alert policy or event rule.<br><br>4. [Specify event or alert triggers](https://docs.byteplus.com/en/docs/ecs/Set_up_event_or_alert_triggers)<br><br>   Associate event or alert triggers with your orchestration plan. This allows preset operations in the plan to start under specific conditions, thereby enabling automated O&M. |


<span id="rjQfQXK3"></span>
### **Create orchestration tasks for common batch operations**

You can perform the following steps to create orchestration tasks for common batch operations on instances, volumes, and images.


|Procedure |Description |
|---|---|
|1. [Preparations](https://docs.byteplus.com/en/docs/ecs/Preparation) (optional) |When using O&M Orchestration for the first time, you need to prepare read and write permissions for Elastic Compute Service (ECS) resources for your Account. |
|2. Create tasks |* [Create tasks for batch instance operations](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task): By entering commands, independently create tasks for batch instance operations to enable process\-based automated O&M.<br><br>* [Create tasks for batch volume operations](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_EBS_Volume_tasks): Perform batch O&M operations on multiple volumes, including volume scaling, snapshot creation, and volume specification modifications, to enhance O&M efficiency.<br><br>* [Create tasks for batch image operations](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_image_tasks): Batch\-create custom images for multiple existing instances to enhance O&M efficiency.<br><br>* [Create temporary bandwidth upgrade tasks](https://docs.byteplus.com/en/docs/ecs/Creating_a_temporary_bandwidth_upgrade_task): Batch\-create temporary bandwidth upgrade tasks for multiple subscription instances to handle traffic peaks, ensure business stability, and lower bandwidth costs. |
|3. View tasks |View the execution results and status of batch tasks, as well as the overview, log, and workflow for each task.<br><br><br>* [Viewing tasks for batch instance operations](https://docs.byteplus.com/en/docs/ecs/View_batch_actions_instance_task)<br><br>* [Viewing tasks for batch volume operations](https://docs.byteplus.com/en/docs/ecs/View_batch_actions_EBS_Volume_tasks)<br><br>* [Viewing tasks for batch image operations](https://docs.byteplus.com/en/docs/ecs/View_batch_actions_image_tasks)<br><br>* [Viewing temporary bandwidth upgrade tasks](https://docs.byteplus.com/en/docs/ecs/View_temporary_bandwidth_upgrade_tasks) |
