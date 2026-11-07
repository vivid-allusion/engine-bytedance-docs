---
title: "Configuring automatic O&M for system events"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-system-event-auto-maintenance"
---

You can configure automatic O&M actions for an instance in the instance maintenance settings, which means the default system response action when the instance encounters a fault risk.  For example, when an unexpected O&M event occurs, the system automatically restarts the instance or keeps the instance shut down.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Currently, this feature only supports certain instance type families. For details, refer to [Supported event types and actions](https://docs.byteplus.com/en/docs/ecs/Configuring-system-event-auto-maintenance#.5pSv5oyB5LqL5Lu257G75Z6L5LiO5Yqo5L2c).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Images". The Instances page appears.

3. In the top menu bar, select the project and region of the target instance.

4. Select "... \> Operations and troubleshooting \> Instance maintenance property" in the "Actions" column on the right side of the target instance.

5. In the pop\-up window, select the default maintenance action to be performed when the instance triggers the corresponding event.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_24a76302e3ee63879cae0bc8a1612e74.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The maintenance action differs based on whether the instance is of the Local SSD type. Please refer to the actual display.   </div>
   

6. Click "Confirm" to complete the configuration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the currently selected instance is the same as that before the change, the "Confirm" button is gray. This means that no O&M configuration is needed for this instance.   </div>
   

<span id=".5pSv5oyB5LqL5Lu257G75Z6L5LiO5Yqo5L2c"></span>
## Supported event types and actions

The following table lists the event types currently supported for O&M configuration and their processing actions.


|Event type |Description |Supported action |Supported instance types |Description |
|---|---|---|---|---|
|SystemFailure.Reboot |The instance is restarted due to system failures |* Automatically restart the instance<br><br>* Automatically redeploy the instance<br><br>* Keep the instance in a shutdown status |* [Local SSD](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based)<br><br>* [Big Data](https://docs.byteplus.com/en/docs/ecs/Big-data-based) |"Automatically restart the instance" is the default action.   |
|SystemFailure.Redeploy |The instance is redeployed due to system failures |* Redeploy the instance and keep its original status<br><br>* Redeploy the instance and shut it down |[All instance types provided by BytePlus](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) |"Redeploy the instance and keep its original status" is the default action.<br><br><br>* If an instance does not meet the requirements for automatic evacuation, it automatically restarts together with its host machine (physical machine). |
|SystemFailure.Stop |The instance is stopped due to system failures |Redeploy the instance and shut it down |* [General-purpose](https://docs.byteplus.com/en/docs/ecs/General-purpose)<br><br>* [Compute-optimized](https://docs.byteplus.com/en/docs/ecs/Computing-optimized) (excluding RDMA instances)<br><br>* [Memory-optimized](https://docs.byteplus.com/en/docs/ecs/Memory-optimized) |"Redeploy the instance and shut it down" is the default action. |
