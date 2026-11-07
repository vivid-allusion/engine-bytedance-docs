---
title: "Creating an event rule"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule"
---

You can configure event alert rules for specified cloud products. When an event that matches a rule occurs, you will promptly receive alert notifications. This helps you quickly locate affected cloud product resources.

<span id="f471eca4"></span>
## Prerequisites

You have selected an appropriate notification method and created a matching notification policy. For more details, see[ Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Up to 1,000 event rules can be created within a root user.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview). 

2. In the left navigation bar, click **Event Center \> Event Rule**.

3. On the **Event rule** page, click **Create event rule** to configure the event rule.

   
   |Parameter |Description |
   |---|---|
   |Name |Specify a name as a unique identifier for the cloud service event rule. Duplicate names are not allowed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using certain characters in the name may cause alert SMS delivery failures. .</div><br> |
   |Resource type |Specify the cloud service to be monitored. |
   |Event name |After you select **Resource type**, names of events supported by the cloud product are displayed on the page. You can select one or more events from the drop\-down list. |
   |Level |Specify the severity level of the event. Valid values: **Critical**, **Warning**, **Notice**. |
   |Project selection |After you select one or more resource types, you can select **All projects** or **Part of the project**. You can manage resources in batches by project. . |
   |Match by event details |Click **Add** to enable more granular event matching based on the fields in the `data` item of the cloud product event details. For example, you can implement event matching based on the instance status or instance ID of a cloud product. For example, if you set `data.WithGPUDevice` to `false`, events with the field `"WithGPUDevice": false` will be matched.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Event details vary by cloud product. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events">Querying events</a>.</div><br> |
   |Notification policy |Select an appropriate notification policy based on actual circumstances. A notification policy defines the recipients, delivery channels, and content display format for alert notifications when alerts of different levels are triggered or recovered. |
   


<span id="xWSMRmZL"></span>
## What to do next

The created event rule is **enabled** by default. You can manage the status of the event rule based on your business requirements. For specific operations, refer to [Managing event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).
