---
title: "Copying an alert template"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Replicating-an-alarm-template"
---

You can create an alert template by copying an existing alert template, which helps you quickly create a similar template without the need to repeatedly specify parameters.

<span id=".5pON5L2c5q2l6aqk"></span>
## Copy an alert template


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Template**.

3. Find the target alert template in the alert template list, and click **Copy** in the **Actions** column.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5885454ee65ff88024571472a0103a6.png) </span>

4. On the **Create alert template** page, modify the configuration and then click **Confirm**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify a custom name for the alert template to identify the alert template.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>* The name can contain special characters. |
   |Description |Specify a custom description for the alert template. |
   |Resource type |Specify the type of monitored cloud service. |
   |Subnamespace |Specify a resource dimension of the monitored cloud service. |
   |Rule name |Specify a custom name for the alert rule.<br><br><br>* The name must be 1 to 64 characters in length.<br><br>* The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>* The name can contain special characters. |
   |Metric type |Specify the metric type for the alert. Valid values: **Single metric** and **Multiple metrics**. |
   |Trigger condition |Configure the metrics, duration, statistic type, comparison operator, and threshold for the alert. If the monitored resource metric meets the trigger condition, the system will send an alert notification.<br><br><br>* If the Metric type parameter is set to **Single metric**, only one trigger condition can be set.<br><br>* If the Metric type parameter is set to **Multiple metrics**, one or more trigger conditions can be set. |
   |Alert level |Specify the severity level of the alert. Valid values: **Critical**, **Warning**, **Notification**. |
   |Effective time |The effective period of the alert policy. The alert policy only monitors whether the resource data meets the trigger condition during the effective period. |
   |Mute For |After an alert policy is triggered, if the monitored resource continues to trigger alerts, the system will periodically send alert notifications. |
   |Alert recovery notification |A recovery notification is sent to users after the alert is cleared. The feature is enabled by default. |
