---
title: "Subscribe to dashboard messages"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Subscribing_to_a_dashboard"
---

Log Service supports the dashboard subscription feature, which periodically sends the dashboard as an image to designated WeChat Work groups, DingTalk groups, or Lark groups. This document describes the steps to subscribe to a dashboard.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Log Service provides a dashboard subscription feature. After successfully subscribing to a dashboard, Log Service renders the dashboard as an image according to the specified message sending schedule and sends it to the designated channel. The message sending channels support Lark groups, WeChat Work groups, and DingTalk groups. Dashboard push messages are sent via custom bots.

The dashboard subscription feature periodically pushes data dashboards to designated groups, suitable for scenarios such as operation reports, daily reports, leaderboards, and regular data exposure.

<span id=".6ZmQ5Yi26K-05piO"></span>
## Description


* Each project can create up to 100 subscription tasks.

* In WeChat Work and DingTalk groups, dashboard subscription notifications keep dashboard image snapshots for up to 1 day. Save them locally in time, as the images become unavailable after 1 day.

* China and world maps do not support subscriptions. If a dashboard subscription contains either map, the corresponding charts in the push notification will appear empty.

* The total number of charts sent simultaneously in dashboard subscription messages cannot exceed 15; otherwise, some charts will display **current search results are empty** in the notification. It is recommended to schedule dashboard subscription messages sequentially during different time periods under each BytePlus account, with no more than 15 charts per dashboard.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A dashboard has been created. For detailed steps, refer to [creating a dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard).

* Before using the dashboard subscription feature for the first time, you must authorize cloud resource access by granting Log Service permissions to query logs and view dashboards. After authorization and adding a dashboard subscription, Log Service periodically uses the role ServiceRoleForTLS to retrieve data for the specified dashboard. Log Service guides you through the authorization process when you first create a dashboard subscription in the console. It is recommended to use the BytePlus account for authorization. For details, see [cross-service access authorization](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the dashboard involves a large amount of data or more complex query and analysis statements, it may cause subscription message sending failures.</div>



1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls/).

2. On the top navigation bar, select the region where the log service is located.

3. On the left navigation bar, select **Common Features** \> **dashboard**.

4. In the dashboard list, click the dashboard under the target project.

5. Click the subscription icon at the top right of the dashboard.

6. Set the subscription rules.

   
   |Configuration |Description |
   |---|---|
   |subscription task name |Name of the dashboard subscription task. |
   |Subscription time period |The dashboard time indicates the time range of the data being viewed. Supports setting to:<br><br><br>* **Dashboard time period**: matches the time range set on the dashboard.<br><br>* **Custom time period**: specify a time range. Supports relative time ranges such as the last 1 minute, or absolute time ranges such as September 1, 2023, 00:00:00 to September 2, 2023, 00:00:00. |
   |Filters and variables |Set filters and variables for dashboard subscriptions. Only filters and variables already added to the current dashboard will appear. For details, refer to [dashboard filters and variables introduction](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard).<br><br><br>* Default option: Use default settings for filters and variables.<br><br>* Custom option: Select relevant variables already set in the current dashboard as needed. |
   |Message sending method |Set channels and corresponding request addresses; up to 5 different request addresses can be configured. Note:<br><br><br>* **Channel**: Supports setting to **Lark**, **WeCom**, and **DingTalk**, representing Lark groups, WeCom groups, and DingTalk groups respectively.<br><br>* **Request address**: Custom webhook URL of the group bot. |
   |Message sending cycle |Set the message sending schedule. Supports setting specific times hourly, daily, weekly, or monthly. Multiple time periods can be set, precise to the minute.<br><br><br>* Hourly.<br><br>* Daily: for example, set **9:00** and **11:00** at the **30th** minute.<br><br>* Weekly: for example, set **Monday**, **Friday**, and **Sunday** at **09:30**.<br><br>* Monthly: for example, set the day of the month as**1, 9**, **24**, the **last day of the month** at **14:00**. |
   |send message test |After setting up, click **Send Test Message**. The log service will send a subscription message within 5 minutes. You can preview the dashboard subscription message effect in the corresponding channel group.<br><br>The sending frequency limit for test messages is one message per minute. Only one test message can be sent per minute. |
   

7. Click **Create Subscription Task**.


<span id=".55u45YWz5pON5L2c"></span>
## Related actions


|Related actions |Description |
|---|---|
|Edit subscription task |Click the subscription dropdown icon at the top right of the specified dashboard's detail page, and find the specified subscription task. Select ... \> **Edit** at the top right of the subscription task to modify the subscription task. |
|Delete subscription task |Click the subscription dropdown icon in the upper right corner of the specified dashboard detail page, then find the specified subscription task. Select ... \> **Delete** at the top right of the subscription task to delete it. |
|Turn subscription task off/on |Click the subscription dropdown icon at the top right of the specified dashboard's detail page, and find the specified subscription task. You can toggle the switch at the top right of the subscription task to enable or disable the subscription task.<br><br>The switch is turned on by default after creating a subscription task. After manually disabling the subscription task, the system will stop sending notifications. |
