---
title: "Configure Flink Alert Policies"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Configure_Flink_Alert_Policies"
---

BytePlus Flink has been integrated with the cloud monitoring service. You can configure alert policies on the cloud monitoring platform to promptly identify abnormal states and send alert notifications.

This document takes configuring alert policies for **job failure or recovery duration** as an example to introduce the alert policy configuration process. After configuring the alert policy, it will monitor the task status, and when it fails or is not in a running state, it will trigger an alert.

<span id="c747d730"></span>
## Create Alert Policies


1. Log in to the [Cloud Monitoring Console](https://console.byteplus.com/cloud-monitor/).

2. In the left sidebar, select **Alarm Center \> Alert Strategy**, then click **Create alarm strategy**.

3. In the **Basic Information** area, set the name and description of the alert policy.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f71f844b732b4e51bf6c383cb0d45646~tplv-goo7wpa0wc-image.image" width="594px" /></div>



4. In the **Alarm Object** area, select the resource type as **Data Hub \> Serverless Flink**, then choose the region, dimension, and resources based on actual conditions.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aeb9da65dad64aff9e8872fb363293e9~tplv-goo7wpa0wc-image.image" width="596px" /></div>



|**Configuration** |**Description** |
|---|---|
|Resource type |Select **Data Hub \> Serverless Flink**. |
|Region |Select based on the region where your resource object is located. |
|Subnamespace |Create dimensions for alert policies, currently supporting **job operational status**, **checkpoint**, and **Kafka**.<br><br>This article configures alarm strategies for the duration of **failed or recovered tasks**, therefore it selects the **task running status** dimension. |
|Resources |Determine the scope of resources (tasks) for setting alarm strategies.<br><br>This article selects **certain parts**, then searches for the target tasks by name or ID, and selects the tasks found.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5086e7bbbdc436b9d0d3a88229de3d4~tplv-goo7wpa0wc-image.image) </span> |



5. In the **Alarm Rules** area, choose the metric type, set the alert rule trigger conditions, alert level, policy effectiveness time, alert sending cycle, etc.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76e73a5f16104d059f2f962c606feb43~tplv-goo7wpa0wc-image.image" width="600px" /></div>



|**Configuration** |**Description** |
|---|---|
|Use preset trigger conditions |No need to focus on this parameter, as BytePlus Flink does not have preset trigger conditions. |
|Metric types |Supports the selection of **single metric** or **multiple metrics**. If you need to monitor multiple metrics of a resource, you can configure multiple metric types directly.<br><br>This article only sets alarm strategies for the duration of metrics **job failed or recovered**, hence selecting **single metric**. |
|Trigger Conditions |Set the monitoring metrics, duration, statistical type, comparison relation, and threshold for alarms. When the monitored resource metrics reach the trigger conditions, the system will send alarm notifications.<br><br>This article sets alarm strategies for the duration of metrics **job failed or recovered**. |
|Alarm Level |Used to indicate the severity of the alarm. Supports setting **critical**, **warning**, **notice** levels. |
|Mute For |Activation time for the alert policy. The alert policy only monitors if the data of the resources reach the triggering conditions during the active time. |
|Notify mode |After the alert policy is triggered, if the monitored resources continue to trigger alerts, the system will periodically send alert notifications. |



6. On the **Create Alert Policy** page, in the **Alert Method** area, select the alert notification method and the alert notification group.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eb4efc96c0646b0b9e8e49dbda7713d~tplv-goo7wpa0wc-image.image" width="606px" /></div>



|**Configuration** |**Description** |
|---|---|
|Alert channels |Select one or more channels. Supports **email**, **phone**, **sms**, and **alert callback**. |
|Alert contact group |When selecting one or more channels such as **alert channels**, **email**, **phone**, or **SMS**, you must set up one or more contact groups to receive alert notifications. For how to set up contact groups, see [creating alert contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).<br><br>First, select the contact groups that need to receive alert notifications, then click the  **\>**  button to confirm. |



7. After configuring the alert policy, click **OK** at the bottom right of the page.

   Return to the Alert Policy page to view policy trigger conditions and status. After the alert policy is successfully created, it will be enabled automatically.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db7648436c5b4c8e8bd045a8cc721110~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="0b9784d7"></span>
## View alert notifications

When the alert policy detects a task failure or a non\-running state, it will trigger an alert and send a notification.

<span id="5c8526b8"></span>
## View alert history

When members of the alert contact group receive the notification, they can go to Cloud Monitor to view the alert history.


1. Log in to the Cloud Monitor Console.

2. Select **Alarm Center \> Alarm History** in the left navigation bar.

3. On the **alert history** page, search for alert history by setting filters such as time period and resource type.

4. Click **Details** behind the alert history to view the alert details, including the time the alert was triggered, the current value of monitoring metrics, and results of alert notifications.
