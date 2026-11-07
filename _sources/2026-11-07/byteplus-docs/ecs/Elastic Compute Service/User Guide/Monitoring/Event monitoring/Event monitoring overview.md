---
title: "Event monitoring overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Event-monitoring-overview"
---

Event monitoring is used to record ECS instance information and send notifications. When an instance or task triggers a system event (such as a system failure that leads to instance redeployment), you can promptly view the event details and take actions.

<span id=".5LqL5Lu254q25oCB"></span>
## Event state


* Event state descriptions:

   
   |Status |Console display |Attribute |Description |
   |---|---|---|---|
   |Inquiring |Inquiring |Intermediate state |This event is in inquiry and waiting for your authorization. After your authorization is obtained, this event will change to​ "Executing" status. |
   |Scheduled |Scheduled |Intermediate state |The O&M task is scheduled for execution but has not started yet. After the task starts, it will enter the "Executing" status. |
   |Executing |Executing |Intermediate state |The O&M task is in progress. |
   |Pending |Pending |Intermediate state |The O&M task has been paused. |
   |Recovered |Recovered |Intermediate state |The O&M task has resumed. |
   |Succeeded |Succeeded |Stable state |The O&M task has been completed. |
   |Rejected |User refuses to execute |Stable state |If you manually refuse authorization, the O&M task will not be conducted. |
   |Failed |Failed |Stable state |The O&M task failed. |
   |Canceled |Cancel |Stable state |The system canceled the O&M task. |
   

* Diagram of general event state changes


<span id=".5LqL5Lu257G75Z6L5LiO5LqL5Lu25ZCN56ew5ZG95ZCN6KeE5YiZ"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5f25757d3fd1144ba0bae2ea0a4f517.png) </span>

<span id=".5LqL5Lu257G75Z6L5LiO5LqL5Lu25ZCN56ew5ZG95ZCN6KeE5YiZ"></span>
## Event types and event naming rules

Event types and event names follow fixed naming rules. After understanding the naming rules, you can quickly understand what an event means through its name. The naming formats are as follows:


* Event type: `<event cause>.<impact on the resource>`

   For example, `SystemFailure.Reboot` means that the ECS instance restarts due to a host machine failure.

* Event name: `<event cause>.<impact on the resource>:<event state>`

   For example: `SystemFailure.Reboot:Succeeded` means that the ECS instance was restarted due to a host machine failure, and the event status is "Succeeded".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information about currently supported events, such as the type, state, name, and recommended action, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Event-type-overview">Event type overview</a>.</div>


<span id="tDCO0Dps"></span>
## Query and handle events

You can query and handle events in the console and through OpenAPI. For more details, refer to [Querying and handling events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events).

<span id=".57O757uf5LqL5Lu26L-Q57u0"></span>
## System event maintenance

You can use the O&M feature to have O&M operations automatically performed based on your configurations for the instance that triggers a specified system event. This helps improve ECS instance stability and reduce O&M costs. For details, refer to [Configuring automatic O&M for system events](https://docs.byteplus.com/en/docs/ecs/Configuring-system-event-auto-maintenance).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager.</div>


<span id=".5o6l5pS25LqL5Lu26YCa55-l"></span>
## Receiving event notifications

When an ECS instance triggers a monitoring event, the event notification can be sent to you via Message Center and Cloud Monitor. [Learn more](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications?lang=zh).
