---
title: "Alert event"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Alert_event"
---

When an alert is triggered, the system records alert event information such as alert status, trigger conditions, and alert time to facilitate traceability and troubleshooting. This topic describes how to view alert events.

<span id="wmGbZQ0x"></span>
## Prerequisites

Required alert configurations, including the notification method, notification recipient, notification template, notification policy, and alert rule, have been completed, and an alert has been successfully triggered. For detailed usage steps, see [Alert Center usage steps](https://docs.byteplus.com/en/docs/Observability_Platform/Alert_Center_overview#0RBoBRkb).

<span id="iprli6Zp"></span>
## Limits


* Alert events are retained for up to 14 days.

* Up to 5,000 alert events can be displayed.

* An alert event spans from when the alert first triggers on a resource to when it recovers. If the alert triggers again after recovery, a new alert event is created.


<span id="Yp1xOX2M"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select  **"Alert Center \> Alert Event"**  to open the "Alert Event" page.

3. Select a product to view the alert event list and key information. Products that support alert events include Cloud Monitor, cloud product events, VMP, and Server\-side Monitoring.

   
   <Tabs>
   <Tab zoneid="xy1O4z7R" title="Resource alert events">
   <TabTitle>Resource alert events</TabTitle>
   
   The key information displayed for alert events in Cloud Monitor, VMP, and Server\-side Monitoring is largely the same. You can filter alert events by region, resource type, event ID, time, and more. The details are as follows:
   
   
   |Key information |Description |
   |---|---|
   |Alert event ID |The unique identifier for an alert event. Click the alert event ID to view the details of the current event. |
   |Alert resource |The resource that triggered the alert. |
   |Resource attributes |This field is included in VMP and Server\-side Monitoring alert events and records the workspace information associated with the alert event. |
   |Alert policy |The alert policy associated with the alert event. Click the alert policy ID to go to the associated alert rule details page for more information. |
   |Alert status |The status of the alert trigger. Options: "Threshold alert triggered" and "No\-data alert triggered".<br><br><br>* **Threshold alert triggered**: The collected data has reached the threshold condition configured in the alert rule, triggering an alert and sending a notification. This is expected behavior.<br><br>* **No\-data alert triggered**: No data has been collected for an extended period, triggering a no\-data alert notification. This indicates an abnormal condition that may be caused by issues such as a faulty collection probe, a service or monitoring resource crash, or a network interruption. Troubleshoot and resolve the issue promptly. |
   |Trigger condition |The condition or rule that triggered the alert. |
   |Alert time |The time at which the alert was triggered. |
   |Action |Click **Create silence policy** to quickly create a silence policy based on this alert event. For more information, see [Creating silence policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_silence_policies). |
   
   
   
   
   
   </Tab>
   <Tab zoneid="WqYOhSNs" title="Cloud product event">
   <TabTitle>Cloud product event</TabTitle>
   
   For cloud product events, you can filter alert events by event source, event name, resource ID, and time. The key information displayed is as follows:
   
   
   |Key information |Description |
   |---|---|
   |Event time |The time at which the cloud product event occurred. |
   |Event source |The resource that triggered the event. |
   |Event |The specific event that was triggered. Different cloud products may generate different events. For the complete list of cloud product events, see [Querying Cloud Monitor events](https://console.byteplus.com/cloud_monitor/docs?tabKey=event&namespace=advanced_ddos_protection). |
   |Region |The region where the event occurred. |
   |TRN |The Top Resource Name (TRN) of the event source. This can be used to control resource permission scopes. |
   |Resource name |The name of the resource that triggered the event. |
   |Project |The project to which the event belongs. |
   |Action |Click **Details** in the "Actions" column of the target event to view the detailed information of the event in JSON format. |
   
   
   
   
   
   </Tab>
   </Tabs>
   

4. Click the alert event ID of a resource to view the alert event details. The details include basic information such as the alert level, trigger condition, alert resource, alert type, and alert status, as well as the alert history and metric monitoring trend chart.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Click <strong>Show</strong> in the alert history to view detailed alert information, such as the trigger condition, current value, and alert trigger status.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Click <strong>View send result</strong> in the alert history to view notification details, such as the notification channel, address, and delivery status.   </div>
