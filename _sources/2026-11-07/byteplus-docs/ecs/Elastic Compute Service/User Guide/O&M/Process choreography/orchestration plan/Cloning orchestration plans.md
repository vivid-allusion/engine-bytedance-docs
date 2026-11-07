---
title: "Cloning orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Clone_an_orchestration_plan"
---

You can use the cloning feature to copy an existing orchestration plan, including its basic information, execution method, steps, and parameters. You can also modify the configuration based on your business requirements. This way, you can quickly create an orchestration plan.

<span id="y7byrtRv"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. In the "Actions" column of the target orchestration plan, click the "Clone" button.

5.  **(Optional)**  Adjust plan information based on your business requirements. For information about the parameters, see [Creating orchestration plans](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan).

6. Click the "Clone" button to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The new orchestration plan is in the <strong>In effect</strong> status after the clone is complete, regardless of whether the source orchestration plan is in the <strong>In effect</strong> or <strong>Canceled</strong> status.   </div>
   

7. (**Optional**) You can click the target plan name to view task execution information. [Learn more](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF).


<span id="tBNefMxq"></span>
## Subsequent steps

If you have changed the trigger method, go to the CloudMonitor console to configure the relevant triggers for the current trigger method. [Learn more](https://docs.byteplus.com/en/docs/ecs/Set_up_event_or_alert_triggers).
