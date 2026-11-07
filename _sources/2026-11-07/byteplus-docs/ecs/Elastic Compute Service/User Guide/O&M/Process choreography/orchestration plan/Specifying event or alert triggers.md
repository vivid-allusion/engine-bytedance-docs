---
title: "Specifying event or alert triggers"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Set_up_event_or_alert_triggers"
---

You can specify alert or event triggers for your orchestration plan, and associate them with alert policies or event rules. This way, predefined operations in the orchestration plan are initiated under specific conditions to execute automated tasks.

> You can specify multiple triggers for an orchestration plan. This way, multiple event rules and alert policies can use the same orchestration plan to execute automated O&M tasks.


<span id="wqrTeHsI"></span>
## Specify an alert trigger

<span id="u4I6yA4F"></span>
### Prerequisites

You have [created an orchestration plan](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan) for which the trigger method is set to **alert trigger**.

<span id="BgIJs70k"></span>
### Procedure


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, click "Alarm Center \> Alarm strategy".

3. On the "Alarm strategy" page, click the "Create alarm strategy" button.

4. Configure the parameters in the "Basic information", "Alarm object", "Alarm rules", "Advanced Settings", and "Alarm way" sections. For more information, see [Creating alarm strategies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you configure the alert method, select "operation and maintenance orchestration" as the alert channel, and select the orchestration plan you want to associate.   </div>
   

<span id="kpK53Z6e"></span>
### Operation results

After you create an alert trigger, when an alert is generated for the resource, Orchestration automatically executes O&M operations based on the orchestration plan associated with the alert policy (alert trigger).

<span id="sZbLz7bu"></span>
## Specify an event trigger

<span id="CHTQdXkv"></span>
### Prerequisites

You have [created an orchestration plan](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan) for which the trigger method is set to **event trigger**.

<span id="jZVt38DH"></span>
### Procedure


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, click "Event Center \> Event Rule".

3. On the "Event Rule" page, click the "Create event rule" button.

4. Configure the parameters in the "Basic information", "Event Rule", and "Delivery method" sections. For more information, see [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you configure the delivery method, select "operation and maintenance orchestration" as the delivery channel, and select the orchestration plan you want to associate.   </div>
   

<span id="n0Zr6907"></span>
### Operation result

After you create an event trigger, when the specified event occurs for the resource, Orchestration automatically executes O&M operations based on the orchestration plan associated with the event rule (event trigger).
