---
title: "Building an automated O&M system for ECS instances through event-triggered orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Trigger_orchestration_plans_through_events_to_build_an_automated_O_and_M_system_for_ECS"
---

<span id="TVrQuo4g"></span>
## Applicable scenario

As business continues to grow, the traditional O&M mode, "initiating and executing O&M manually based on event notifications", gradually exposes problems such as delayed response and long handling time. As a result, the requirement for troubleshooting efficiency can no longer be met.

To handle this issue, BytePlus provides you with an automated event\-triggered O&M solution. Specifically, the platform performs standard O&M operations (such as batch associating EIP addresses, starting or stopping instances) after preset orchestration plans are automatically triggered. This helps build an O&M process of "automatic fault discovery \- automatic handling". Besides, the solution upgrades O&M operations targeted at ECS instances from "passive response" to "proactive automated response". Therefore, faults are handled much more efficiently, which ensures that your business runs continuously and stably.

<span id="oWqmZH4i"></span>
## Planning information

When the "GPURiskDetected.Succeeded" event occurs for a GPU instance, the running instance may be faulty. You can try restarting the instance to resolve the issue. To minimize business impact, this topic describes a plan to preset an automated O&M process of batch restarting instances.

<span id="MuejkCMA"></span>
## Usage note

Once an orchestration plan is created and associated with an event rule, new events are under continuous monitoring, with specified O&M operations performed. Processes continue until you [cancel the orchestration plan](https://docs.byteplus.com/en/docs/ecs/Cancel_the_orchestration_plan) or stop using this orchestration plan as the delivery channel for the event rule.

<span id="g9s5oGi9"></span>
## Procedure

<span id="bjDGEOZ9"></span>
### Step 1: Create an orchestration plan

Based on a default step, preset an O&M orchestration process for the "GPURiskDetected.Succeeded" event. This ensures that when this event occurs, the associated orchestration plan is automatically triggered to achieve automated O&M.

<span id="mSrz04B9"></span>
#### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located. In this topic, China (Beijing) is used as an example.

4. On the "CloudOps Orchestration" page, click the "orchestration plan" tab.

5. Click the "Create orchestration plan" button. Configure the parameters described in the following table.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Specify the name of the orchestration plan to identify this plan. |Orchestration plan for GPU instance risk |
   |Role<br><br> |Select a role with read and write permissions on your ECS resources. The default role is "CustomRoleForOOS," which integrates all permissions supported by Orchestration by default. This prevents permission issues during usage. |Default configuration<br><br> |
   |**Execution mode** |||
   |Execution mode |Indicates the mode of executing the orchestration plan. Default option: "trigger execution". |Default configuration |
   |Trigger method |Select the method for automatically triggering the orchestration plan. |Event trigger |
   |**Task step** |||
   |Add step<br><br> |Indicates the operation performed (for O&M) after the event specified in an event rule is generated, when the event rule is associated with an orchestration plan.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple steps can be added, with the upper limit of ten and the lower limit of one. Here, we take an example of adding one step for illustration.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Task steps are preset by default. <a href="https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps">Learn more</a>.</div><br><br><br>1. Click the "Add step" button, and in the right pane, select "BulkyRebootInstances".<br><br>   > Before the task for batch restarting instances is executed, we recommend that you first learn the prerequisites, precautions, and other information for restarting instances. For details, refer to [Restarting instances](https://docs.byteplus.com/en/docs/ecs/Restarting-instances).   <br>   <br><br>2. Click the "Add" button to complete the addition.<br><br>3. Configure parameters for each step.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To learn more about supported parameters in each step, see <a href="https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps">Summary of orchestration steps</a>.   </div><br>   <br><br>   1. Select the "Input" tab, and enter or select the parameter values required for step execution as guided by the console.<br><br>      Select "Get from event object" for the instance ID source. Then, enter the ID of the instance as the event object, as shown below:<br><br>      ```Plain Text```<br>```      {{[.Metric.Resources[].ID]}}```<br>```      ```<br>      <br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">"Get from event object" can be configured only when the trigger method is <strong>Event trigger</strong>.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After "Get from event object" is enabled, event\-triggered parameters are delivered in "Event" format. You can select a corresponding value from the JSON of the event object. <a href="https://docs.byteplus.com/en/docs/ecs/Content_of_the_event_alert_callback_request">Learn more</a>.      </div><br>      <br><br>   2. (**Optional**) Select the "Output" tab to view information about the parameter returned after the current step is executed. The returned parameter is preset by default. No manual configuration is needed. |BulkyRebootInstances<br><br> |
   

6. Click "Create" to complete the operation.

   Then, you can view the orchestration plan "Orchestration plan for GPU instance risk" on the orchestration plan list page. The plan status is **Running**.


<span id="FQcU2MY4"></span>
### Step 2: Create an event rule

Configure an event rule (event trigger) for "Orchestration plan for GPU instance risk" created in step 1 and associate them. This ensures that when a "GPURiskDetected.Succeeded" event is triggered, the preset orchestration process (orchestration plan) is automatically triggered to achieve automated O&M.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">An orchestration plan can be associated with multiple event triggers. This allows multiple event triggers to use one orchestration plan for automated O&M operations. Here, we take an example of adding one event rule for illustration.</div>


<span id="ak8CGsUl"></span>
#### Limits

Only instances of GPU Accelerated and HPC\-optimized instance type families can trigger "GPURiskDetected.Succeeded" events. For details, refer to the [instance type list](https://docs.byteplus.com/en/docs/gpu/Instances).

<span id="D0aoVq5J"></span>
#### Procedure


1. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Monitor".

2. In the left navigation pane, select "Event Center \> Event Rule".

3. Click the "Create event rule" button and configure the parameters described in the following table.

   This section only describes parameters related to a "GPURiskDetected.Succeeded" event. For more information, see [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Enter the name to identify the event rule. |Orchestration due to GPU operation risk |
   |**Event Rule** |||
   |Resource scope |Select the cloud product to be monitored. |ecs |
   |Event name |Specify the event description as "GPURiskDetected.Succeeded". This enables the event to trigger the orchestration plan for restarting instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Event descriptions vary based on selected resource type. The event descriptions displayed in the console prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple preset events can be selected, with the upper limit of all and the lower limit of one.</div><br> |GPURiskDetected.Succeeded |
   |Level |Click the dropdown list and select an event severity level. This helps O&M personnel to quickly learn whether an event is important, severe, or urgent. |Severe |
   |**Delivery method** |||
   |Delivery channel |Select the delivery channel for event notification. When the monitored resource meets a trigger condition, Cloud Monitor automatically sends an event notification and triggers the [Orchestration plan for GPU instance risk](https://docs.byteplus.com/en/docs/ecs/Trigger_orchestration_plans_through_events_to_build_an_automated_O_and_M_system_for_ECS?lang=zh&TagIDs=2,288,70,69,87#bjDGEOZ9).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Alert channels are important for sending alert notifications. This parameter is required only when you select "Manual selection".</div><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple channels can be selected based on your needs, with the lower limit of one. Here, we take an example of selecting one channel for illustration.</div><br> |operation and maintenance orchestration |
   |orchestration plan |Select the region of the [orchestration plan](https://docs.byteplus.com/en/docs/ecs/Trigger_orchestration_plans_through_events_to_build_an_automated_O_and_M_system_for_ECS#bjDGEOZ9) and its name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Specify the same region as the orchestration plan.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required only when you set the delivery channel to "operation and maintenance orchestration".</div><br> |* Region: China (Beijing)<br><br>* Orchestration plan: Orchestration plan for GPU instance risk |
   |Effective time |Specify the effective duration of the event rule. Only during this period can alerts be triggered and events be generated. |Default configuration |
   

4. Click "Create" to complete the operation.

   Then, you can view the event rule "Orchestration due to GPU operation risk" on the event rule list page. The rule status is **Enabled**.


<span id="G27aFhjD"></span>
#### Expected result

When a "GPURiskDetected.Succeeded" event is triggered on an instance, O&M operations preset in the "BulkyRebootInstances" O&M process are performed based on the associated orchestration plan.

<span id="zTDHbd2u"></span>
### Step 3: View execution results

View details of "Orchestration plan for GPU instance risk" to verify whether the O&M operation of restarting instances is performed.

<span id="BtQzzGaZ"></span>
#### Procedure


1. On the orchestration plan list page, click the orchestration plan "Orchestration plan for GPU instance risk".

2. Click the "execute" tab. Then, you can view all execution records of the orchestration plan, such as execution ID and status. For more information, refer to [Viewing orchestration plans](https://docs.byteplus.com/en/docs/ecs/View_orchestration_plans).


<span id="XTocCXAK"></span>
#### Expected results


* If "No data" is displayed, the orchestration plan is not executed. This may be because no trigger event has actually been generated. For more event details, [learn more](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events).

* If a successfully executed task is displayed, observe whether the "GPURiskDetected.Succeeded" event continues to be generated. If so, we recommend [submitting a ticket ](https://console.byteplus.com/ticket/createTicketV2/)for further troubleshooting.
