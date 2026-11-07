---
title: "Viewing events"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events"
---

Event Center enables you to monitor the faults of cloud services. After an event of a cloud service occurs, information about the event, such as the occurrence time, source, name, and details, will be saved in Event Center. You can view cloud service events to promptly identify and resolve issues.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

Occurred events are saved for 30 days by default.

<span id=".5pON5L2c5q2l6aqk"></span>
## View cloud service events


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Event Center \> Cloud product event**.

3. On the **Cloud Service Event** page, view the information about cloud service events within the specified time period.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b58f291e37b9032d69bbe8e86481fdcc.png) </span>

   You can filter events by specifying the time period, cloud service, and event type. The following table describes the specific operations.

   
   |Section |Descriptions |
   |---|---|
   |① |You can select a time period or specify a custom time period to filter events that occurred during the specified time period.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can query event information within the last hour by default. You can query data within the last 30 days at most.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The specified time period can be accurate to minutes, with seconds set to 00 by default.</div><br> |
   |② |You can filter events by selecting a cloud service and selecting one or more event types. |
   |③ |View the list of events that meet the filter criteria. The string displayed in the **Event** column consists of three parts, which is in the format of `service name:event type:event content`.<br><br>For example, the event `ecs:Instance:RunInstance.Executing` indicates that the service name is ECS, the event type is the instance resource, and the event content is that the instance is being started. |
   

4. Click **Details** in the **Actions** column that corresponds to an event to view the event details in JSON format.
