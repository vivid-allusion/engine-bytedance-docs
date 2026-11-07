---
title: "Enabling scheduled maintenance windows"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enabling_scheduled_maintenance_windows"
---

You can enable a scheduled maintenance window in the **Disabled** status as needed. After it is enabled, when a [scheduled O&M event](https://docs.byteplus.com/en/docs/ecs/Event-type-overview?lang=zh#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2) is triggered by resources associated with this window, BytePlus will be automatically authorized to perform relevant O&M operations. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating_scheduled_maintenance_windows).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before enabling, confirm that the window cycle falls within off\-peak hours to avoid impacting your business.</div>


* <div data-tips="true" data-tips-type="warning">Redeploying instances will affect data stored on all local volumes (including both faulty and healthy volumes) associated with the instances. Please back up data in advance to prevent data loss. You can back up data using <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh">volumes</a>, <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh">TOS</a>, or other methods.</div>



<span id="i4u6sjK8"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. Select the region where your business is located.

4. Click the "Scheduled maintenance window" tab.

5. In the "Actions" column of the target scheduled maintenance window, click the "Enable" button to complete the operation.
