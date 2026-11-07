---
title: "Configuring an alarm policy"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/alarm-rules"
---

Cloud Search service has been integrated with Cloud Monitor, which allows you to configure alarm policies in the Cloud Monitor console. Once a resource exception is detected, the system sends alarm notifications to inform you, thus improving the efficiency of operations and maintenance (O&M).

This topic describes how to configure alarm policies in the Cloud Monitor console.

<span id="e894527e"></span>
## Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Observability \> Monitoring overview**.

5. On the upper\-right corner of **Running state** pane, click **Create alarm policy**, and then the [Create alarm strategy](https://console.byteplus.com/cloud-monitor/alert/strategy/create) page in Cloud Monitor console pops up.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5657d975675340b6909b96f6bd7295cc~tplv-goo7wpa0wc-image.image) </span>

6. In the **Basic information** pane, set the name and description of the alarm policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/663f99fb8cf448e7a168cd8ec102866e~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify a customized name for the alarm policy as an identifier.<br><br><br>* The length must be within 0\-128 characters.<br><br>* It cannot start with a digit or a hyphen. |
   |Description |Specify an explanation for the alarm policy.<br><br><br>* English letters, Chinese characters, digits, underscores (_) and hyphens (\-) are supported.<br><br>* The length must be within 0\-255 characters.<br><br>* It cannot start with a digit or a hyphen. |
   

7. In the **Alarm object** pane, set the resource type to **Middleware \> Cloud Search**, and then select the Region, dimension, and effective range based on your business needs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d73d39dbf59418292fcca852989997e~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Resource type |Select **Middleware \> Cloud Search**. |
   |Region |Select the Region where your resource resides. |
   |Dimension |Select a dimension for the alarm policy.<br><br><br>* **Instance**: If you select this dimension, the alarm policy is configured based on the following metrics: **Instance Health State**, **Instance Data Node Number**, **Active Shard Number**, **Unsigned Shard Number**, **Total Document Number**, **Instance Capacity Usage**, **Red Index Number**, **Yellow Index Number**, **MaxDiskUsagerPercent**, and **AvgDiskUsagePercent**.<br><br>* **Node**: If you select this dimension, the alarm policy is configured based on the following metrics: **JVM Usage**, **Young GC Count Per Min**, **Old GC Count Per Min**, **Node FS IOPS**, **Node CPU Usage**, **DiskUsagePercent**, **es_fs_io_total_write_bytes**, and **es_fs_io_total_read_bytes**. |
   |Resources |Select the range of resources to which you want to apply the alarm policy.<br><br><br>* **All**: The policy applies to all instances or nodes within the current account. The policy also applies to all new instances and nodes that match specific conditions.<br><br>* **Part**: The policy applies only to instances or nodes that you manually selected. |
   

8. In the **Alarm rules** pane, configure the following parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adfb387c00694d6f9420f57da0ebb967~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Use preset trigger conditions |The trigger conditions that are preset based on the dimension of the alarm policy. This parameter helps you quickly configure the alarm policy. However, no preset trigger conditions are available for any dimensions of Cloud Search. You can ignore this parameter. |
   |Metric type |Select **Single metric** or **Multiple metrics**.<br><br>Select **Multiple metrics** if you want to monitor multiple metrics of resources. |
   |Trigger condition |Specify a metric, interval, statistics type, relationship operator, and threshold. If the metric of a monitored resource meets the trigger condition, the system sends an alarm notification.<br><br><br>* If the metric type is set to **Single metric**, only one trigger condition can be set.<br><br>* If the metric type is set to **Multiple metrics**, one or more trigger conditions can be set. |
   |Alarm level |Specify an alarm severity level. Alarm severity levels include **Critical**, **Warning**, and **Notice**. |
   |Effective time |Specify the effective period of the alarm policy. The alarm policy only monitors whether the resources meet the trigger conditions within the effective period. |
   |Mute For |Specify the alarm notification interval to determine how frequently the system sends notifications when a monitored resource constantly meets the trigger conditions. |
   |Alarm recovery notification |Specify whether the system sends a notification after an alarm is cleared. By default, this switch is turned on.<br><br>The notification is sent by email, phone, text message, or webhook (Lark, DingTalk, or WeCom). Other API webhooks cannot be used to send alarm clearance notifications. |
   

9. In the **Alarm way** pane, select alarm notification methods and contact groups that receive notifications.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/916e0f8864554b71a466e52fd8a77545~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Alarm channel |Select one or more alarm channels. Options are **Email** and **Webhook**. |
   |Alarm contact group |When you select **Email** as the alarm channels, you must set one or more contact groups to receive notifications. |
   |Webhook |Specify an available URL. This parameter appears and is required only when you select **Webhook** as the alarm channel.<br><br>When an alarm is triggered, the system sends alarm details to the specified URL using a POST request. This allows you to conduct in\-depth data analysis. |
   

10. After all the settings are complete, click **OK** on the lower\-right corner of the page.

   The alarm policy takes effect immediately after it is created.
