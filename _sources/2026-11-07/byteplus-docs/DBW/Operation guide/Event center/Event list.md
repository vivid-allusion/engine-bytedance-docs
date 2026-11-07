---
title: "Event list"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Event_list"
---

The event list page displays alerts and monitoring and O&M events for instances under the current account. This topic describes how to view Event Center information.

<span id="OwzrVreJ"></span>
## Background

Database Workshop provides the Event Center feature, which offers unified alarm and notification management capabilities. You can configure alarm rules, select notification objects and notification methods based on your business needs, and apply alarm capabilities to specified resources or event scopes to receive timely notifications when anomalies, risks, or critical state changes occur. DBW is responsible for defining and reporting event sources, while alarm execution, delivery, and notification capabilities are provided by Cloud Monitoring.

<span id="6T0ry5r7"></span>
## Prerequisite

You must have data sources that can generate events and the corresponding alarm or event reporting capabilities. For detailed operations, see [Notification policy management](https://docs.byteplus.com/en/docs/DBW/Notification_policy_management) and [Rule configuration management](https://docs.byteplus.com/en/docs/DBW/Rule_configuration_management).

<span id="rdEMiONb"></span>
## Precautions


* The event list only displays event records for the currently selected region. Make sure you have switched to the target region.

* Select the engine type before selecting an instance; otherwise, the instance selection box is not available.

* Event data displays the last 24 hours by default. You can adjust the query time frame using the time range selector, with support for viewing event information within the last 30 days.

* Custom events and external event sources are not supported yet.

* Event sources are defined and reported by DBW, while alarm execution, delivery, and notification capabilities are provided by Cloud Monitor.


<span id="aPCL26Q4"></span>
## Procedure


<Tabs>
<Tab zoneid="y3dIxUqdJZ" title="Viewing event list">
<TabTitle>Viewing event list</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. In the left navigation pane, choose **Event center** \> **Event list**.

4. On the **Event list** page, you can view information such as the **Event type**, **Engine type**, **Triggered instance**, and **Event time** of each event. Filter target events by engine type, event type, instance, or time frame. Select an engine type before selecting an instance.


Click **Details** in the **Actions** column of the target event to go to the **Notification details** page, where you can view the event's **Basic information** (**Event type**, **Notification content**, **Region**, **Engine type**, **Triggered instance**, **Occurrence time**) and **Payload** information.


</Tab>
<Tab zoneid="OrxuAuw6Wb" title="Downloading event information">
<TabTitle>Downloading event information</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. In the left navigation pane, choose **Event center** \> **Event list**.

4. On the **Event list** page, click Export.

5. In the **Export Data** dialog box, select the fields to export as needed. Available fields include: **Event type**, **Engine type**, **Triggered instance**, and **Event time**.

6. Click **OK**.


</Tab>
</Tabs>
