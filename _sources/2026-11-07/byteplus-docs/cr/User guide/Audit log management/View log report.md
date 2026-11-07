---
title: "View log report"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/View_the_image_instance_log_report"
---

CR supports image push and pull logs and other logs via log audit, helping you understand the status of image push and pull operations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The log audit service has been enabled. For details, see [Enabling log audit](https://docs.byteplus.com/en/docs/cr/Turn_On_Audit_log).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the[ CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **Instance list**. Then, in the **Instance list** area, find the Standard Edition instance where you need to create an artifact repository and click **Enter instance**.

2. On the Standard Edition instance details page, click **Audit log** in the left navigation bar.

3. On the **Audit log** \> **Log report** page, view the instance logs.


<span id=".5a6e5L6L5pel5b-X5Luq6KGo55uY"></span>
## Instance log dashboard

Currently, the image instance information dashboard includes the following dashboards.

<span id=".5o6o6YCB57uf6K6hL-aLieWPlue7n-iuoQ=="></span>
### Push statistics / Pull statistics

Displays the number of image push and pull operations in the instance within the specified time period.

<span id=".5YWs56eB572RLeaLieWPlumVnOWDj-avlOS-iy_lhaznp4HnvZEt5o6o6YCB6ZWc5YOP5q-U5L6L"></span>
### Private/public network image pull ratio / Private/public network image push ratio 

Displays the ratio and count of image push and pull operations over different network types in the instance within the specified time period.


* Private: VPC.

* Public: public network.


<span id=".5ouJ5Y-W6aKR5qyh5pyA6auYIFRhZy1Ub3AxMC_mjqjpgIHpopHmrKHmnIDpq5ggUmVwby1Ub3AxMA=="></span>
### Top 10 tags by pull frequency / Top 10 OCI artifact repositories by push frequency 

Displays the top 10 image tags (Tag) by pull count and the top 10 OCI artifact repositories (Repo) by push count in the instance within the specified time period.

<span id=".55So5oi35L2_55So6aKR5qyh"></span>
### User usage frequency

Displays the total number of image push and pull operations on the instance by user within the specified time period.

<span id=".5Luq6KGo55uY6YCa55So5Yqf6IO9"></span>
## General dashboard features

<span id=".6K6-572u5p-l6K-i5pe26Ze06IyD5Zu077yI5YWo5bGA5pe26Ze077yJ"></span>
### Specify the query time range (global time)

The dashboard query time is used to specify the time range for all statistical charts in the dashboard. In the time selection box at the top right corner of the dashboard, specify a time range. You can select a relative time range or specify a custom time.


* When you re\-enter the dashboard, the dashboard time range is automatically cleared.

* When you refresh the dashboard using the refresh button in the upper right corner, the dashboard time range remains unchanged.


<span id=".5raI5oGv6K6i6ZiF"></span>
### Message subscription

After you subscribe to a dashboard, the system will render the dashboard as an image and send it to the specified channel based on the specified message sending cycle. The message can be sent to Feishu groups, WeCom groups, and DingTalk groups. Dashboard push messages are sent using custom bots. For details, see [Subscribing to dashboards](https://docs.byteplus.com/en/docs/tls/Subscribing_to_a_dashboard).

<span id=".5re75Yqg5ZGK6K2m"></span>
### Add an alarm

Charts added to a dashboard can be used as monitoring tasks for alarm policies. This allows you to quickly create an alarm policy.

In the upper\-right corner of the target chart, open the drop\-down menu and click **Add alarm**. Then complete the alarm configuration as needed. For a detailed description, see [Creating alarm strategies](https://docs.byteplus.com/en/docs/tls/create_alarm_policies).

In the alarm policy, the **Execute statement** field under **Monitoring task ** is automatically populated with the monitoring object, search and analysis statement, and time range from the corresponding chart. You can modify these settings or use them directly.
