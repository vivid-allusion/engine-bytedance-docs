---
title: "Querying and responding to \"SystemFailure.Redeploy\" events"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Responding-to-the-SystemMaintenance_Redeploy-event"
---

This topic describes how to query and respond to "SystemFailure.Redeploy" events in the console. This helps you quickly troubleshoot issues and run your cloud products stably.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

When the host machine (host) of an ECS instance crashes due to a failure, it may be necessary to redeploy the instance to a new host machine to restore normal operations of the instance. To help you quickly resolve the failure, the platform sends you event\-based notifications and also offers you comprehensive automatic O&M methods.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After <a href="https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications">enabling event monitoring notifications</a>, you can receive event notifications via the message center and Cloud Monitor.</div>


<span id=".5Zy65pmv5LiA77ya5L-d5oyB5a6e5L6L5YGc5q2i54q25oCB"></span>
## Scenario 1: Keep instance stopped

This scenario applies when you do not want the instance to be redeployed to another host machine when an event is triggered.

<span id=".5pON5L2c5rWB56iL"></span>
### Operation processes

After an ECS instance triggers this event, it will not be redeployed. Meanwhile, an event indicating the instance is successfully stopped due to a system failure is generated to notify you.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For instances in the <strong>Stopped</strong> status, billing continues.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Images". The Instances page appears.

3. In the top menu bar, select the project and region of the target instance.

4. Select "... \> Operations and troubleshooting \> Instance maintenance property" in the "Actions" column on the right side of the target instance.

5. In the pop\-up window, check "Redeploy instances and shut down". For detailed automatic O&M configurations, see [Configuring automatic O&M for system events](https://docs.byteplus.com/en/docs/ecs/Configuring-system-event-auto-maintenance).


<span id=".5Zy65pmv5LqM77ya6Ieq5Yqo6YeN5paw6YOo572y5a6e5L6L"></span>
## Scenario 2: Automatically redeploy instance

This scenario applies when you want your instance to be automatically redeployed to another host machine to restore its normal operation when an event is triggered.

<span id=".5pON5L2c5rWB56iL"></span>
### Operation processes

When an ECS instance triggers this event, an event indicating the instance is being redeployed due to a system failure is generated. After receiving this notification, the O&M personnel redeploys your instance to a new host machine, which is expected to take 5 minutes.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Images". The Instances page appears.

3. In the top menu bar, select the project and region of the target instance.

4. Select "... \> Operations and troubleshooting \> Instance maintenance property" in the "Actions" column on the right side of the target instance.

5. In the pop\-up window, check "Automatically Redeploy (Default)". For detailed automatic O&M configurations, see [Configuring automatic O&M for system events](https://docs.byteplus.com/en/docs/ecs/Configuring-system-event-auto-maintenance).

6. When the ECS instance is redeployed successfully after triggering this event, an event indicating the instance is successfully redeployed due to a system failure is generated to synchronize the O&M result with you.
