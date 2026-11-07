---
title: "Using Alert Center"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center"
---

Alert Center generates alerts for metrics. You can configure alert policies for key metrics of cloud products. When metric data changes or does not meet expectations, the system will immediately notify you about the exception, which enables you to handle the exception at the earliest opportunity.

<span id=".5q2l6aqk5LiA77ya5Yib5bu65ZGK6K2m6IGU57O75Lq6"></span>
## Step 1: Create a contact


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification \> Contacts**.

3. On the **Contacts ** tab, click **Create contact**.

4. In the **Create contacts** dialog box, specify the **Name**, **Email**, and **Phone** parameters of the alert contact and then click **Confirm**.

5. After you configure the email address or phone number and create the contact, Cloud Monitor will send a verification message to the specified email address or phone number.

   The following figure shows the verification message content sent to an email address. You need to click the URL to complete the verification.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65ZGK6K2m6IGU57O757uE"></span>
## Step 2: Create a contact group

When you create an alert policy, select the corresponding contact group to receive alert notifications through the contact group.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification \> Contacts**.

3. Click the **Contact group** tab.

4. On the **Contact group** tab, click **Create contact group**.

5. In the **Create contact group** dialog box, specify the **Name**, **Description**, and **Select contacts** parameters of the contact group and then click **Confirm**.


<span id="131a095e"></span>
## Step 3: Create a callback URL


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification** \> **Callback**.

3. On the **Callback address list** page, click **Create callback address**.

4. On the **Create callback address** page, specify the following parameters and then click **Confirm**.

   
   |Parameter |Descriptions |
   |---|---|
   |Webhook name |Specify a custom name for the webhook to identify the callback URL. Duplicate names are not allowed. |
   |Callback address type |Select the callback address type. Supported types include Lark, DingTalk, WeCom, and Generic Webhook. |
   |Callback address |Enter a publicly accessible URL and then click **Test** to verify the callback URL.<br><br><br>* If the callback URL returns the HTTP status code 200, it indicates that the connectivity test is successful, and the webhook can receive alerts and event notifications.<br><br>* The connectivity test enforces a one query per second (QPS) limit. |
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65ZGK6K2m562W55Wl"></span>
## Step 4: Create an alert policy

You can specify custom monitoring data thresholds, alert levels, the effective periods of alert policies, alert sending intervals, and notification methods. Flexible and diverse policies can meet your alert and monitoring requirements for different business scenarios.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification \> Alert policy**.

3. On the **Alert policy** page, click **Create alert policy**.

4. On the **Create alert policy** page, configure the details of the alert policy.

   * **Basic information**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Name |Specify a custom name for the alert policy. |
      |Description |Specify a custom description for the alert policy. |
      

   * **Alert object**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Resource type |Specify the type of monitored cloud service. Supported cloud service types displayed in the console shall prevail. |
      |Subnamespace |Specify the resource subnamespace of the monitored cloud service. |
      |Selection method |* **Manual selection**: Manually select resources.<br><br>* **Object Group**: selects resources based on object groups. For specific operations, see [Creating object groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group).<br><br>* **Resource name**: selects resources based on resource names.<br><br>* **Project**: selects resources based on projects. <br><br>* **Label**: selects resources based on labels.  |
      |Region |The region to which the monitored resource belongs. |
      |Resource |Specify a resource range to which the alert policy applies, which means only resources within the resource range can be monitored. You can perform the following operations on resources:<br><br><br>* All: The alert policy is configured for all resources matching the specified resource type, region, and subnamespace within the current account.<br><br>   After selection, newly created resources that meet these conditions will be automatically added to the alert policy.<br><br>* Part: You need to manually select one or more resources.<br><br>   After selection, the alert policy is configured only for these resources. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Available regions and subnamespaces vary based on the cloud service type. The options displayed in the console shall prevail.      </div>
      

   * **Alert rules**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Use preset trigger conditions |The console presets trigger conditions based on the resource subnamespaces to help you quickly configure alert policies.  <br><br><br>* If the Metric type parameter is set to Multi\-metric, you can use the pre\-configured trigger condition.<br><br>* Select **Use preset trigger** conditions to automatically specify the Metric type and Trigger condition parameters, which can be modified, deleted, and added.<br><br>* If no pre\-configured trigger conditions are configured for a subnamespace, you cannot select **Use preset trigger conditions**. |
      |Metric type |Select the metric type. Valid values: **Single\-metric** and **Multi\-metric**. If you need to monitor multiple metrics of a resource, you can select Multiple metrics. |
      |Trigger condition |Configure the metrics, duration, statistic type, comparison operator, and threshold for the alert. If the monitored resource metric meets the trigger condition, the system will send an alert notification.<br><br><br>* If the **Metric type** parameter is set to **Single metric**, only one trigger condition can be set.<br><br>* If the **Metric type** parameter is set to **Multiple metrics**, one or more trigger conditions can be set.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Take note of the following rules when you configure trigger conditions for multiple metrics:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An alert can be triggered if <strong>any</strong> condition or <strong>all</strong> conditions are met.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">At least one and up to 10 trigger conditions can be configured.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot configure duplicate trigger conditions.   </div><br>   <br><br>   For example, the trigger condition `average disk utilization > 80%, lasting for 10 cycles (1 cycle = 1 minute)` indicates the system checks the resource metric every 1 minute, and if the average disk utilization of a specific resource exceeds 80% for consecutive 10 cycles, an alert will be triggered. |
      |Mute For |After an alert policy is triggered, if the monitored resource continuously triggers alerts, the system will periodically send alert notifications to prevent excessive notifications.<br><br><br>* You can set the alert sending cycle to **5 minutes**, **10 minutes**, **15 minutes**, **30 minutes**, **60 minutes**, **3 hours**, **6 hours**, **12 hours**, or **24 hours**.<br><br>* The default value is 5 minutes. |
      |Notify mode |* **Rule**: If any resource in the alert rule continuously exceeds the alert threshold during the alert sending cycle, only one alert notification is sent during the cycle.<br><br>* **Rule and resource**: If different resources in the alert rule continuously exceed the alert threshold during the alert sending cycle, alert notifications will be sent for each resource. If metrics do not recover after the alert sending cycle elapses, Cloud Monitor will send alert notifications again. |
      |Alert recovery notification |A recovery notification is sent to users after the alert is cleared. The feature is enabled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">An alert recovery notification is sent when the status of an alert policy returns to <strong>Normal</strong> and Cloud Monitor determines that an alert has recovered.</div><br> |
      |NoData alert |Configure the NoData alert.<br><br><br>* Configure a trigger condition. If no data is reported for the specified resource for consecutive n cycles, a NoData alert will be triggered.<br><br>* Configure the level of the NoData alert. Valid values: **Critical**, **Warning**, and **Notice**. |
      

   * **Advanced settings**: Specify the project to which the alert policy belongs. The default project is selected by default.

   * **Alert way**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Notification method |Select an alert notification channel.  <br><br><br>* **Manual selection:**  Manually configure a notification method of the alert policy.<br><br>* **Notification policy:**  Specify a configured notification policy. For more details, refer to [Creating notification policies](https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy). |
      |Alert channel |Select one or more channels. Valid values: **Email**, **Phone**, **SMS**, and **Alert callback**.<br><br>For the limits on receiving notifications by phone calls or SMS message, see [Limit](https://docs.byteplus.com/en/docs/cloudmonitor/Limits). |
      |alert contact group |If you select one or more of the following options for **Alert channel**: **Email**, **Phone**, or **SMS**, the **Alert contact group** parameter will be displayed on the page.<br><br><br>* At least one contact group must be specified as the recipient of alert notifications.<br><br>* At most five contact groups can be specified as the recipients of alert notifications. |
      |Webhook |If you set the **Alert channel** parameter to **Alert callback**, the **Alert callback** text box will be displayed on the page.<br><br><br>* You must specify a public URL as the webhook URL. If a resource subsequently triggers an alert policy, the system will send the alert details to this URL via a POST request, enabling you to perform in\-depth data analysis.<br><br>   * You can select created webhook URLs. Up to eight webhook URLs can be selected.<br><br>   * You can enter only one webhook URL.<br><br>* We recommend that you prepare a server with the HTTP service enabled and accessible via the public network, and then specify the HTTP URL of the server as the callback URL.<br><br>* For more information about alert callbacks, see [Alert callback usage](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions).<br><br>* Alert webhooks can be associated with bots in Lark, DingTalk, and WeCom groups to automatically push alert notifications. For specific operations, see [Receiving alert notifications by Lark group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups), [Receiving alert notifications by DingTalk group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups), and [Receiving alert notifications by WeCom group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups). |
