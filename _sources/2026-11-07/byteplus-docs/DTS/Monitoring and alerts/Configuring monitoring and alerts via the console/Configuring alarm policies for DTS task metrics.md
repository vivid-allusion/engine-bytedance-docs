---
title: "Configuring alarm policies for DTS task metrics"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/setting_alerts"
---

You can set alarm rules for important metrics in data migration and synchronization tasks through the cloud monitor console. When an abnormality occurs in the metric, cloud monitoring will promptly notify you to take measures. This topic describes how to set the notification policy of metric alarms on the cloud monitor console, such as metric alarm triggering conditions, alarm level, and effective time.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cloud monitor has already been activated. For more details, refer to [Enabling pay-as-you-go for cloud monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling_pay-as-you-go).

* You have created alarm contacts and contact groups. For details, refer to [Creating alarm contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Monitoring metric items of the Redis type is not supported.

* Alert policies are only supported for started transport tasks.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Go to the alarm policy page of cloud monitor.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If it is a data subscription task, choose method 2 to create it in the cloud monitoring console.   </div>
   

   * Method 1

      1. Log on to the [DTS console](https://console.byteplus.com/dts).

      2. In the left navigation bar, click **Data migration** or **Data synchronization**.

      3. On the **Data migration list** or **Data synchronization list** page, click the task name.

      4. On the task details page, click **Monitor**.

      5. On the **Monitor** tab, click **Create alarm policy**.

   * Method 2

      1. Log on to the [Cloud monitor console](https://console.byteplus.com/cloud-monitor/overview).

      2. In the left navigation pane, choose **Alarm center** \> **Alarm policy**.

      3. On the **Alarm policy** page, click **Create alarm policy**.

2. On the **Create alarm policy** page, configure the following information.

   
   |**Type** |**Name** |**Description** |
   |---|---|---|
   |**Basic information** |**Name** |Customize the alarm policy name to identify the alarm policy. Naming rules are as follows: <br><br><br>* Cannot start with a number or a hyphen (~).<br><br>* The length must be between 1 and 128 characters. |
   ||**Description** |Descriptive information for custom alarm policies. The rule is described as follows:<br><br><br>* Cannot start with digits or hyphen.<br><br>* It can only contain Chinese, letters, digits, underscores, and hyphens.<br><br>* The length must be within 0~255 keys. |
   |**Alarm object** |**Resource type** |Select **Database Transmission Service (DTS)**  from the drop\-down list of resource types. |
   ||**Region** |Select the target region from the drop\-down list. |
   ||**Dimension** |The default value is **Task** and it cannot be selected. |
   ||**Select resources** |Set the resource scope of the alarm policy, that is, monitor only within this resource scope. The following settings are supported:<br><br><br>* **All**: Indicates that the alarm policy is set for all resources that meet the specified resource type, region, and dimension under the current account. At the same time, the newly created resources that meet the conditions will automatically match the alarm policy.<br><br>* **Part**: You need to manually select one or more resources. When selected, it indicates that the alarm policy is only set for that part of the resource. |
   |**Alarm rule** |**Use preset trigger condition** |The trigger conditions pre\-configured by the console according to the alarm dimension make it easy for you to quickly fill in the alarm policy. Contains indicator types and trigger conditions.<br><br><br>* Preset trigger conditions are supported when the indicator type is a multi\-indicator.<br><br>* Check **Use preset trigger conditions** to automatically fill in the indicator type and trigger conditions, which can be modified, deleted, and added.<br><br>* If no preset trigger condition is set for the dimension, you cannot select **Use preset trigger condition**. |
   ||**Type of indicators** |You can select **single indicator** or **multiple indicators**. If you need to monitor multiple indicators of resources, you can directly configure the multi\-indicator Type. |
   ||**Trigger condition** |Set the monitor indicators, duration, statistic types, comparison relationships, and thresholds for the alarm. The system pushes alarm notifications when the monitored resource indicator meets the trigger condition.<br><br><br>* If the indicator type is set to **single indicator**, only one trigger condition can be set.<br><br>* If the indicator type is set to **Multi\-indicator**, one or more trigger conditions are supported.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Trigger condition for multi\-indicator:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It supports triggering after all conditions are met or after any condition is met.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set at least one trigger condition and at most 10 trigger conditions.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Repeated setting of the same trigger condition is not supported.   </div><br>   <br><br><br>Example: The trigger condition is` average CPU usage > 80%, lasting 3 cycles (1 cycle = 1 minute)`, indicating that the system detects resource indicators in 1 minute as a cycle, and if the average CPU usage of a resource in three consecutive cycles is greater than 80%, an alarm is triggered. |
   ||**Alarm level** |Used to identify the severity of an alarm. You can set the level to **Critical**, **Warning**, or **Notice**. |
   ||**Effective time** |The effective time of the alarm policy. The alarm policy only monitors whether the resource data reaches the triggering condition within the effective time. |
   ||**Alarm sending cycle** |After the alarm policy is triggered, if the monitored resource continues to trigger alarms, the system periodically sends alarm notifications. |
   ||**Alarm recovery notification** |A recovery notification is sent to the user after the alarm is recovered. Enabled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Email, phone, SMS, alarm callbacks (Feishu, DingTalk, WeCom) have alarm recovery notifications, and other API alarm callbacks have no alarm recovery notifications.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The alarm recovery notification is a recovery notification for the alarm rule dimension. Cloud monitor (VCM) determines that the alarm is recovered when the alarm rule state is <strong>Normal</strong><strong></strong><strong></strong><strong></strong><strong></strong>.</div><br> |
   |**Alarm mode** |**Alarm channel** |Select one or more channels. Supports **email**, **phone**, **SMS**, and **alarm callback**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For phone and SMS notification receiving limits, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Limits">Limits</a>.</div><br> |
   ||**Alarm contact group** |When you select one or more **Alarm channels** from **Email**, **Phone**, or **SMS**, the page displays the **Alarm** contact group, and you must set one or more contact groups to receive **Alarm** notifications. Set a maximum of 5 contact groups as recipients. |
   ||**Alarm callback** |When the **alarm channel** selects **alarm callback**, the **alarm callback** text box is displayed on the page, and you must specify an available URL. If a resource triggers the Alarm policy, the System sends the Details of the Alarm to this URL via a POST request for in\-depth data analysis.<br><br><br>* Prepare a server with an opened HTTP service and network intercommunication with the cloud monitor console, and then set the server's HTTP URL as the alarm callback URL.<br><br>* For more information about warning callbacks, refer to [Warning callback usage instructions](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions).<br><br>* The alarm callback supports associating with group robots in Feishu, DingTalk, and Enterprise WeChat to automatically push alarm notifications. For specific operations, refer to [Receiving Alarm Notifications Through Feishu Groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups), [Receiving Alarm Notifications Through DingTalk Groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups), and [Receiving alarm notifications through WeChat groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups). |
   

3. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

You can view and manage the created alarm policies. For specific operations, refer to [Viewing alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy).
