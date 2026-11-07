---
title: "Building an automated O&M system for ECS instances through alert-triggered orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Use_alert_to_trigger_orchestration_plans_and_build_an_automated_O_and_M_system_for_ECS"
---

<span id="oUR3Ocx9"></span>
## Applicable scenario

As business continues to grow, the traditional O&M mode, "initiating and executing O&M manually based on alert notifications", gradually exposes problems such as delayed response and long handling time. As a result, the requirement for troubleshooting efficiency​ can no longer be met.

To handle this issue, BytePlus provides you with an automated, alert\-triggered O&M solution. Specifically, the platform performs standard O&M operations (such as batch changing instance types, starting or stopping instances) after preset orchestration plans are automatically triggered. This helps build an O&M process of "automatic fault discovery \- automatic handling". Besides, the solution upgrades O&M operations targeted at ECS instances from "passive response" to "proactive automated response". Therefore, faults are handled much more efficiently, which ensures that your business runs continuously and stably.

<span id="uTfaLmiq"></span>
## Planning information

Suppose your instances (Instances A, B, and C) are memory overloaded (average memory usage ≥ 80%) due to growing business, and the available memory can no longer meet business requirements. To resolve this issue, you need a larger memory capacity based on the feature of automatically batch changing instance types. The plan is as follows:


|Instance |Original instance types |Original memory |Availability zone of instance |Billing method |Instance type after change |Memory after change |
|---|---|---|---|---|---|---|
|Instance A |ecs.g3il.large |8GiB |cn\-beijing\-a |Pay\-as\-you\-go |ecs.r4i.xlarge |32GiB |
|Instance B |ecs.c3il.xlarge |8GiB |||||
|Instance C |ecs.g4i.xlarge |16GiB |||||


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Instance types can be changed in a batch only when the availability zone and billing method of target instances are the same.</div>


* <div data-tips="true" data-tips-type="warning">Specifications and memory capacities of each instance may vary before batch changes. Afterward, the configurations of the two parameters are the same among all target instances.</div>



<span id="ydHBnawX"></span>
## Usage note

Once an orchestration plan is created and associated with an alert policy, new alerts are under continuous monitoring, with specified O&M operations performed. Processes continue until you [cancel the orchestration plan](https://docs.byteplus.com/en/docs/ecs/Cancel_the_orchestration_plan) or stop using this orchestration plan as the channel for the alert policy.

<span id="A28lsiOi"></span>
## Procedure

<span id="bScEeLWl"></span>
### Step 1: Create an orchestration plan

Based on a default step, preset an O&M orchestration process for the alert where the average memory usage reaches or exceeds 80%. This ensures that when this alert is generated, the associated orchestration plan is automatically triggered to achieve automated O&M.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "orchestration plan" tab.

5. Click the "Create orchestration plan" button. Configure the parameters described in the following table.

   The following only describes related parameters for the alert where the average memory usage reaches or exceeds 80%. For more parameter descriptions, see [Creating orchestration plans](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan).

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Specify the name of the orchestration plan to identify this plan. |O&M plan for average memory load​ ≥ 80% |
   |Role<br><br> |Select a role with read and write permissions on your ECS resources. Default option: "CustomRoleForOOS". |Default configuration |
   |**Execution mode** |||
   |Execution mode |Indicates the mode of executing the orchestration plan. Default option: "trigger execution". |Default configuration |
   |Trigger method |Select the method for automatically triggering the orchestration plan. |Alert trigger |
   |**Task steps** |||
   |Add step<br><br> |Add operations to be performed (O&M) after an alert is triggered by the associated alert policy. This enables O&M operations to be performed in the specified sequence based on alert.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple steps can be added, with the upper limit of ten and the lower limit of one. Here, we take an example of adding one step for illustration.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Task steps are preset by default. <a href="https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps">Learn more</a>.</div><br><br><br>1. Click the "Add step" button, and in the right pane, select "BulkyModifyInstanceSpec".<br><br>   > Before the task for batch changing instance types is executed, we recommend that you learn related information first, such as limits and operation descriptions. For details, refer to [Changing instance types](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).   <br>   <br><br>2. Click the "Add" button to complete the addition.<br><br>3. Configure parameters for each step.<br><br>   You can configure input and output parameters for each step. Once a step is executed, the relevant information is displayed. To learn more about supported parameters in each step, see [Summary of orchestration steps](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps).<br><br>   1. Select the "Input" tab, and enter the parameter values required for step execution as guided by the console.<br><br>      1. Select "Custom input" for the instance ID source. Then, select instances whose specifications need to be changed.<br><br>         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div><br>         <br><br>         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">To change instance types successfully, you are required to select instances that have the same configuration for both the "Availability zone" and "Billing method" parameters.         </div><br>         <br><br>      2. Then, configure related parameters based on your needs. For parameter descriptions, see [Changing instance types](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).<br><br>   2. (**Optional**) Select the "Output" tab to view information about the parameters returned after the current step is executed.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Returned parameters are preset by default. No manual configuration is needed.      </div><br>       |BulkyModifyInstanceSpec<br><br> |
   

6. Click "Create" to complete the operation.

   Then, you can view the orchestration plan, named "O&M plan for average memory load​ ≥ 80%" on the orchestration plan list page.


<span id="EC4Ioy8o"></span>
### Step 2: Configure an alert policy

Configure an alert policy (alert trigger) for "O&M plan for average memory load​ ≥ 80%" created in step 1 and associate them. This ensures that when an alert is triggered, the preset orchestration process (orchestration plan) is automatically triggered to achieve automated O&M.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can specify multiple triggers for an orchestration plan. This way, multiple alert policies can use the same orchestration plan to execute automated O&M tasks. Here, we take an example of adding one alert policy for illustration.</div>


<span id="nLdKv9Y8"></span>
#### Procedure


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, click "Alarm Center \> Alarm strategy".

3. On the Alarm strategy page, click the "Create alarm strategy" button and configure the parameters described in the following table.

   The following only describes parameters related to this practice. For more parameter descriptions, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Specify the name for the alert policy to identify this policy. |Monitoring for memory load exception |
   |**Alarm object** |||
   |Resource type |Select the type of cloud product to be monitored. |ECS |
   |Subnamespace |Specify the resource dimension of ECS instances to be monitored. |Instance |
   |selection method |Specify a method of selecting ECS instance resources to be monitored. Default option: "Manual selection". |Default configuration |
   |Region |Select the region where the resources to be monitored belong.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Specify the same region as the orchestration plan.</div><br> |China (Beijing) |
   |Resource |Specify the resource scope for which the alert policy takes effect. Only resources within the specified resource scope are monitored. Supported:<br><br><br>* **All**: Indicates that the alert policy takes effect on all resources under the current account that match the specified resource type, region, and dimension. After this option is selected, new resources that meet conditions also automatically match this alert policy.<br><br>* **Part**: Manual resource selection is required. Multiple selection is supported. After this option is selected, the alert policy takes effect only on selected resources. |All |
   |**Alarm rules** |||
   |Metric type |Select a monitored metric type. For target instances, one or multiple metric types can be selected. |Single metric |
   |Trigger condition |Configure metrics to be monitored and the duration cycle. This way, when a specified metric of monitored resources meets trigger conditions, an alert is triggered. |Memory Used Utilization \>= Critical 80% |
   |Mute For |Select a cycle of sending alert notifications, which means how often an alert notification is sent. |5 minutes |
   |Notify mode |Specify the notification mode of the aggregation policy. |rule |
   |**Alert setting** |||
   |Project |Associate the alert policy with a project. Default option: "default". |Default configuration |
   |**Alarm way** |||
   |Notification method |Select the method for alert notifications. |Manual selection |
   |Alarm channel |Select the channel for alert notifications. When monitored resources meet trigger conditions, the system sends alert notifications accordingly.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple channels can be selected based on your needs, with the lower limit of one.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required only when you select "Manual selection".</div><br> |operation and maintenance orchestration |
   |orchestration plan |Select the [orchestration plan created in step 1](https://docs.byteplus.com/en/docs/ecs/Use_alert_to_trigger_orchestration_plans_and_build_an_automated_O_and_M_system_for_ECS?lang=zh#bScEeLWl).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Specify the same region as the orchestration plan.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required only when you set "Alarm channel" to "operation and maintenance orchestration".</div><br> |O&M plan for average memory load​ ≥ 80% |
   |Effective time |Specify an effective duration of the alert policy. Only during this period, the alert policy takes effect and triggers alerts. |Default configuration |
   

4. Click "Create" to complete the operation.

   Then, you can view the alert, named "Monitoring for memory load exception" on the alert policy list page. The policy status is **Enabled**.


<span id="oO2tMBcQ"></span>
#### Expected result

When the average memory load of an instance reaches or exceeds 80%, an alert is automatically triggered. At the same time, the associated orchestration plan is triggered to execute O&M operations.

<span id="vIH7po34"></span>
### Step 3: View execution results

View details of "O&M plan for average memory load​ ≥ 80%" to verify whether the O&M operation of changing instance types (specifically, expanding memory capacity) is performed.

<span id="4WB0TBmu"></span>
#### Procedure


1. On the orchestration plan list page, click the orchestration plan named "O&M plan for average memory load​ ≥ 80%".

2. Click the "execute" tab. Then, you can view all execution records of the orchestration plan, such as execution ID and status. For more information, refer to [Viewing orchestration plans](https://docs.byteplus.com/en/docs/ecs/View_orchestration_plans).


<span id="HzZ8QfCl"></span>
#### Expected results


* If "No data" is displayed, the orchestration plan is not executed. This may be because no alert has been generated. For details of generated alerts, [learn more](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history).

* If a successfully executed task is displayed, you can:

   1. Go to the instance list page. Then, check whether the instance whose specification has been changed is running normally and whether its total memory capacity is expanded as expected. [Learn more](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1).

   2. Based on diagnosis of [instance performance issues](https://docs.byteplus.com/en/docs/ecs/Diagnose_instance_health_status), check whether the instance memory load drops to the safe threshold to make sure the memory expansion takes effect.
