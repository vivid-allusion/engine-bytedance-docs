---
title: "Creating orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan"
---

You can create orchestration plans to predefine O&M orchestration workflows for specific alert policies or event rules. When an alert or event occurs, the associated orchestration plan is automatically triggered, enabling automated O&M.

<span id="q0FkHCKi"></span>
## Prerequisite

If you want to use a custom template to create an orchestration plan, create the [custom template](https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates) first.

<span id="pQR27Xtx"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "orchestration plan" tab.

5. Click the "Create orchestration plan" button. Configure the parameters described in the following table.

   
   |Parameter​ ||Description |Sample value |
   |---|---|---|---|
   |**Basic information** ||||
   |Name ||Specify the name of the orchestration plan. |AutoInstanceRestartUponGPURisk |
   |Role ||Select a role with read and write permissions on your ECS resources. The default role is "CustomRoleForOOS," which integrates all permissions supported by Orchestration by default. This prevents permission issues during usage.<br><br>You can also click the "Role" drop\-down list to select a different role. The selected role must have permissions to perform operations on the corresponding resource.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click "View permissions required for the task" to view the permissions that are required by the role to execute orchestration plan.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the existing roles do not meet your business requirements, you can also click "Navigate to role management" to create a role.</div><br> |Retain the default value.<br><br> |
   |**Execution mode** ||||
   |Execution mode ||The execution mode of tasks in the orchestration plan. Valid values:<br><br><br>* **Execute immediately**: After the tasks in the orchestration plan are created, they are executed immediately.<br><br>* **Trigger execution**: The orchestration plan is executed each time the orchestration plan is triggered by the specified event or alert. |Trigger execution |
   |Trigger method ||Select the trigger method. Valid values:<br><br><br>* Event trigger: When a specific event is generated for the target resource, the orchestration plan is automatically triggered, enabling automated O&M.<br><br>* Alert trigger: When the target resource generates an alert notification, the orchestration plan is automatically triggered, enabling automated O&M.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when you set "Mode" to "trigger execution".</div><br> |Event trigger |
   |**Task step** ||||
   |Step creation type |Create from scratch |Add the steps you want to execute one by one in your desired order, using the [preset task steps](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps) as a foundation. When the orchestration plan is executed, it performs automated O&M according to the sequence of these task steps.<br><br><br>1. Click the "Create from scratch" button.<br><br>2. Click the "Add step" button, and select the required step in the pop\-up window.<br><br>   > After you add a step, the system automatically assigns an ID to the step, making it easier to distinguish steps with the same feature. For example, the ID for a step that creates an ECS instance is id:437a.   <br>   <br><br>2. Click the "Add" button to complete the addition.<br><br>3. Configure parameters for each step.<br><br>   You can configure input and output parameters for each step. Once a step is executed, the relevant information is displayed. For parameters supported by each step, see [Summary of orchestration steps](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps).<br><br>   1. Select the "Input" tab and configure the input parameters required for step execution. Parameter sources:<br><br>      * **Custom input**: Select or enter parameter values.<br><br>         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div><br>         <br><br>         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Certain steps only allow you to manually enter parameter values. The requirements specified for the steps in the console prevail.         </div><br>         <br><br>      * **Select from previous tasks**: Select the output parameter values of the previous steps in O&M orchestration as the input parameter values.<br><br>      * **Get from event object**: The parameters triggered by the event are passed in the form of an Event. You can select a specific value from the JSON data of the event object. For example, you can use `{{.Event.Details.data.InstanceId}}` to obtain the instance ID from the event object. For the description of the event object structure, see [Content of event alert callback requests](https://docs.byteplus.com/en/docs/ecs/Content_of_the_event_alert_callback_request).<br><br>         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div><br>         <br><br>         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">When you set "trigger method" to <strong>"Event trigger"</strong>, you can select "Get from event object".         </div><br>         <br><br>      * **Get from alert object**: The parameters triggered by the alert are passed in the form of a Metric. You can select a specific value from the JSON data of the alert object. For example, you can use `{{.Metric.Resources[0].id}}` to obtain the instance ID from the alert object. For the description of the alert object structure, see [Content of metric alert callback requests](https://docs.byteplus.com/en/docs/ecs/Metric_alert_callback_request_content).<br><br>         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div><br>         <br><br>         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">When you set "trigger method" to <strong>"Alert trigger"</strong>, you can select "Get from alert object".         </div><br>         <br><br>   2. Select the "Output" tab to view information about the parameters returned after the current step is executed.<br><br>4. (**Optional**) After you click the target step, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_778d25c3b299f8ab8b2f07913a3ffff4.png) </span> icon to add more steps based on your business requirements.<br><br>   > You can reorder the added steps by dragging them. |Create ECS instances<br><br> |
   ||Select an existing template |You can create an orchestration plan based on an existing template ([custom template](https://docs.byteplus.com/en/docs/ecs/Viewing_custom_templates)). This enables the orchestration plan to automatically execute O&M tasks using your preset standardized O&M workflows.<br><br><br>1. Click the "Select an existing template" button.<br><br>2. Click the template drop\-down list, select the target template, and view its basic information to verify whether the selected template meets your requirements.<br><br>3. Configure the parameters based on the template you select. [Learn more](https://docs.byteplus.com/en/docs/ecs/Viewing_custom_templates).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The parameters vary depending on the selected template. The parameters displayed in the console prevail.   </div><br>    |\- |
   

6. Click "Create" to complete the operation.

7. (**Optional**) You can click the plan name to view plan execution information. For more information, see [Viewing orchestration plans](https://docs.byteplus.com/en/docs/ecs/View_orchestration_plans).


<span id="WupobkTs"></span>
## Subsequent steps

After the orchestration plan is created, go to the CloudMonitor console to specify an event or alert trigger based on the trigger method you selected. [Learn more](https://docs.byteplus.com/en/docs/ecs/Set_up_event_or_alert_triggers).
