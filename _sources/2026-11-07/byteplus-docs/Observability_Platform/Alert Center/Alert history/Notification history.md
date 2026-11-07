---
title: "Notification history"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Notification_history"
---

After an alert is successfully triggered, the system records notification history, including the notification message content, notification time, and notification result. These records facilitate historical review and troubleshooting. This topic describes how to view notification history.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Notification history includes both alert notification records and records of silenced notification messages.</div>


<span id="bIX5LszL"></span>
## Prerequisites

Required alert configurations, including the notification method, notification recipient, notification template, notification policy, and alert rule, have been completed, and an alert has been successfully triggered. For detailed usage steps, see [Alert Center usage steps](https://docs.byteplus.com/en/docs/Observability_Platform/Alert_Center_overview#0RBoBRkb).

<span id="zpKE9BID"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select  **"Alert Center \> Notification history"**  to open the "Notification history" page.

3. Select a product to view its notification history and key information. Products that support notification history include Cloud Monitor, cloud product events, VMP, and Server\-side Monitoring.

   
   |Key information |Description |
   |---|---|
   |Notification batch ID |The unique identifier for a notification history entry. Click the notification batch ID to view the details of the current notification. |
   |Alert policy ID |The alert policy associated with the notification batch. Click the alert policy ID to go to the associated alert rule details page for more information. |
   |Sent at |The time at which the notification was sent. |
   |Alert type |The type of alert notification. Options: "Threshold alert triggered" and "No\-data alert triggered".<br><br><br>* **Threshold alert triggered**: The collected data has reached the threshold condition configured in the alert rule, triggering an alert and sending a notification. This is expected behavior.<br><br>* **No\-data alert triggered**: No data has been collected for an extended period, triggering a no\-data alert notification. This indicates an abnormal condition that may be caused by issues such as a faulty collection probe, a service or monitoring resource crash, or a network interruption. Troubleshoot and resolve the issue promptly. |
   |Notification result |The result of the notification delivery.<br><br><br>* Red indicates a delivery failure; green indicates a successful delivery.<br><br>* Hover over a channel icon to view more details, including the notification recipient, channel, target, delivery result, and response result. |
   

4. Click the notification batch ID of the target notification to view the batch details. The details include basic information such as the batch ID, alert type, monitoring type, and notification policy, as well as alert\-related information such as the notification channel, alert policy, and alert event.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Click <strong>Show message content</strong> in the "Actions" column next to the notification recipient to view the notification message content.   </div>
