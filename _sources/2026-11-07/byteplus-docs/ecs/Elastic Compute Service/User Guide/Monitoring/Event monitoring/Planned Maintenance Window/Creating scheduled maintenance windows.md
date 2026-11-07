---
title: "Creating scheduled maintenance windows"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_scheduled_maintenance_windows"
---

If you create a maintenance window for a target instance, BytePlus will automatically be authorized to redeploy your instance to a new host machine when a [scheduled O&M event ](https://docs.byteplus.com/en/docs/ecs/Event-type-overview?lang=zh#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2)is triggered. This helps mitigate the risk of severe downtime caused by abnormally running hosts and ensures the continuity and stability of your business.

> If the associated resources have already triggered a scheduled maintenance event in the ** Inquiring ** status when you create the scheduled maintenance window, you need to manually select a maintenance time and complete the authorization. 


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For instances mounted with local volumes: Redeploying instances will affect data stored on all local volumes (including both faulty and healthy volumes) associated with the instances. Please back up data in advance to prevent data loss. You can back up data using <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh">volumes</a>, <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh">TOS</a>, or other methods.</div>


* <div data-tips="true" data-tips-type="warning">During the O&M period, operations such as <strong>shutdown</strong> and <strong>restart</strong> are performed on instances, which may impact your business. Please select an appropriate O&M time, such as during off\-peak hours.</div>



<span id="UA46ByZb"></span>
## Prerequisites

To use tags to select target ECS instances for scheduled maintenance window operations, first [associate the corresponding tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview?lang=zh#.5Yib5bu65bm257uR5a6a5qCH562-) with the instances.

<span id="EOR3ryl5"></span>
## Limits


|Associated object |Association relationship |Description |
|---|---|---|
|Scheduled maintenance window and resource object (instances selected by project) |One\-to\-one |* Each scheduled maintenance window can be associated with only one resource object (project) and cannot be associated with multiple resource objects (projects) simultaneously.<br><br>* Each resource object (project) can be associated with only one scheduled maintenance window and cannot be associated with multiple scheduled maintenance windows. |
|Scheduled maintenance window and resource object (instances selected by tag) |One\-to\-ten |* A single scheduled maintenance window can be associated with up to ten resource objects (tags).<br><br>* A single resource object (tag) can be associated with only one scheduled maintenance window. |


<span id="9CMddqO3"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. Select the region where your business is located.

4. Click the "Scheduled maintenance window" tab.

5. Click the "Create maintenance window" button and configure the parameters described in the following table.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Window name |The name of the scheduled maintenance window. |Scheduled maintenance window for project A |
   |Resource object |Target resource objects (instances) can be precisely selected by specifying a project or tag.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After a scheduled maintenance window is configured to select resources by specifying a project or tag and is in the <strong>Enabled</strong> status, newly created instances that match the criteria will also be automatically included in the window's management scope.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If configurations for both the "Specify project" and "Specify tag" parameters are present, the configuration selected at submission time takes precedence as the final effective rule.</div><br><br><br>* **Specify project**<br><br>   Resources covered by the scheduled maintenance window can be flexibly selected based on projects associated with instances. This is applicable to batch O&M scenarios.<br><br>* **Specify tag**<br><br>   Resources covered by the scheduled maintenance window can be flexibly selected based on custom tag key\-value pairs (Key\-Value) of instances. This is applicable to batch O&M scenarios. |Specify project/default |
   |Window cycle |The preset time period for executing O&M operations. Supported options include "Daily" and "Weekly".<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend configuring multiple time periods for a scheduled maintenance window to reduce the probability of mismatches between the actual required maintenance time and the scheduled window time, thereby improving the success rate of event execution.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The window cycle uses UTC time by default, with <code>Sunday 00:00</code> as the minimum starting point for configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The duration of a single time period within a single scheduled maintenance window must be at least 30 minutes.</div><br><br><br>* **Daily**<br><br>   * Repeats the time window configuration on a daily basis, suitable for setting short, fixed maintenance periods each day with relatively minor impact and short duration.<br><br>   * Click the "Add time range" button to set more maintenance time periods. Up to 10 time ranges can be added, and at least 1 time range is required.<br><br>* **Weekly**<br><br>   * Repeats the time window configuration on a weekly basis, suitable for setting longer, fixed maintenance periods each week, which may have a greater impact and longer duration.<br><br>   * Click the "Add time range" button to set more maintenance time periods. Up to 10 time ranges can be added, and at least 1 time range is required.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The window cycle supports cross\-week configuration, but the total duration cannot exceed one week (7 days).   </div><br>    |Daily<br><br>Start time: 00:00<br><br>End time: 02:00 |
   |Maintenance action |The default maintenance action of a scheduled maintenance window is "Redeploy", and cannot be modified. |Retain the default value |
   |Enable maintenance window |Specifies whether to enable the scheduled maintenance window immediately upon creation.<br><br><br>* Enable (default): The scheduled maintenance window is enabled immediately upon creation.<br><br>* Disable: The scheduled maintenance window does not need to be enabled immediately upon creation.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you choose not to enable the window, you are required to manually enable it later for it to take effect.   </div><br>    |Enable |
   

6. Click the "Confirm" button to complete the operation.


<span id="7sbSmwMa"></span>
## Expected results

When a [scheduled O&M event](https://docs.byteplus.com/en/docs/ecs/Event-type-overview?lang=zh#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2) is triggered for resources associated with this maintenance window,  is automatically authorized to deploy your instances to a new host. Upon successful authorization, the event status updates to **Executing**. And  will perform the redeployment operation based on the configured window cycle. Once the deployment succeeds, the event status updates to **Succeeded**.
