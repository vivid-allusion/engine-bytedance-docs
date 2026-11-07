---
title: "Creating event policy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_event_policy"
---

Subscribe to events and tasks executed by MySQL instances via Cloud Monitor, helping you keep track of instance status in real time. This topic describes how to create an event policy.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Create a notification policy in Cloud Monitor. For more information, refer to [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

You can save a maximum of 1,000 event policies for a single account.

<span id=".5Yib5bu65LqL5Lu26KeE5YiZ"></span>
## Creating event policy


1. Log on to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview).

2. In the left\-side navigation pane, choose **Event center \> Event policy**.

3. On the **Event policy** page, click **create event policy** and configure the event policy.

   
   |**Configuration item** |**Is it required?**  |**Description** |
   |---|---|---|
   |Parameter name<br><br> |Yes |Specify a name as a unique identifier for the cloud service event rule. Duplicate names are not allowed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using certain characters in the name may cause warning SMS delivery to fail. For more information, see <a href="https://docs.byteplus.com/en/docs/6361/170340">Template review specifications</a>.</div><br> |
   |Description |No |The description of the event policy, which you can customize. |
   |Resource type |Yes |Select **RDS for MySQL** from the drop\-down list. |
   |Event name |Yes |Select an event name from the drop\-down list. You can select one or more events. |
   |Severity |Yes |Indicates the severity of the event. You can set the level to **Critical**, **Warning**, or **Notice**. |
   |Project selection |Yes |After you select one or more resource types, you can select **All projects** or **Part of the project**. You can manage resources in batches by project. For more information, refer to [Project Resource Management](https://docs.byteplus.com/en/docs/6649/94337). |
   |Match by event details |No |Click ** Add** to enable more granular event matching based on the fields in the data item of the cloud product event details. For example, you can implement event matching based on the instance status or instance ID of a cloud product. For example, if you set data.WithGPUDevice to false, events with the field "WithGPUDevice": false will be matched. |
   |Notification policy |Yes |Select an appropriate notification policy based on actual circumstances. A notification policy defines the recipients, delivery channels, and content display format for alert notifications when alerts of different levels are triggered or recovered. |
   


&nbsp;

<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

A successfully created event policy is **Enabled** by default. You can manage its state later based on your actual needs. For more information, refer to [Managing event policies](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).

<span id=".55u45YWz6ZO-5o6l"></span>
## Related links


* [Creating event policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule)

* [Managing event policies](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule)
