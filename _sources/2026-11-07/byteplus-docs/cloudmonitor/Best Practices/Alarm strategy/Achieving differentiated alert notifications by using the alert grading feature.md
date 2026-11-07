---
title: "Achieving differentiated alert notifications by using the alert grading feature"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Alarm_classification_feature_for_alarm_differentiation_notifications"
---

Cloud Monitor supports alert grading, allowing you to set different thresholds for different alert levels under the same trigger conditions and send alerts through various notification channels. This topic describes how to configure alert grading and send graded alert notifications through different channels.

<span id="qFMfq18O"></span>
## Background

<span id="8QtNbcL2"></span>
### Alert levels

In cloud resource monitoring practices, not all alerts are of the same level of urgency. Some require immediate human intervention, some require eventual human intervention, and others indicate areas that may need future attention. The common principles for classifying alert levels are shown in the following table.


|Alert level |Description |
|---|---|
|Critical |The most urgent alerts should receive special handling and be escalated to "Critical" to request immediate human attention. For example, the response time of your web application should have an internal SLA that is at least as strict as the most stringent customer\-facing SLA. Any instance where the response time exceeds the internal SLA requires immediate attention. |
|Warning |The Warning level is for issues that do require intervention, but not immediately. The data storage may be running low on disk space and should be expanded in the next few days. Combining email notifications with posts in the chat room of the service owner is an ideal method for delivering these alerts. Both channels are highly noticeable, but neither will disturb sleep during off\-hours or interrupt the workflow of engineers. |
|Notification |Many alerts are unrelated to service issues, so people may never need to be aware of them. For example, a low\-severity alert should be triggered if a user\-facing datastore becomes significantly slower than usual but not slow enough to affect overall service response times. This alert is recorded in the monitoring system for later analysis, without disrupting anyone. After all, transient issues like network congestion often resolve themselves. However, if the service starts returning a large number of timeouts, the alert data will provide valuable context for your investigation. |
|Resolved |When an anomaly detected by the monitoring system returns to normal, a recovery alert can promptly notify the ops team. This can inform the ops team that the issue has been resolved and the system or service has returned to normal operation, and help the ops team confirm that the issue has been resolved, preventing unnecessary resource investment in troubleshooting due to not being promptly informed of the recovery. After an alert is resolved, the recovery notification can be sent to a relatively independent channel or use a different notification method from the trigger alert. This helps the ops team more quickly notice that the system has returned to normal, preventing them from overlooking the recovery status amidst a flood of alert messages. |


<span id="ntcghrJH"></span>
### Alert trigger logic

Before introducing the alert trigger logic of Cloud Monitor, several key terms need to be clarified first:


* **Detection period**: The number of consecutive cycles during which the alert condition must meet the threshold to trigger an alert. This period is configurable. Each cycle is 1 minute. You can either configure 1 cycle or multiple cycles, e.g., 3, 5, and 10, for a single period.

* **Silence period**: The period during which no alert notifications are sent, even if the alert conditions continue to meet the threshold, after an alert is triggered. This period is configurable. You can set it to different time periods, e.g., 5, 10, 15, and 30 minutes.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">During the silence period, the system continues to evaluate whether the alert conditions meet the threshold. The only difference is that no alert notifications are sent, even if the threshold is reached, until the silence period ends.</div>


After Cloud Monitor adopts a graded alerting policy, its alert trigger logic is as follows:


* If a low\-severity alert threshold (e.g., notification level) is met throughout the detection period, the system sends a notification. Once the alert is sent, the system starts a silence period. In the silence period, same\-level alerts will not be re\-triggered or re\-sent.

* During the silence period of a low\-severity alert (e.g., notification level), if a high\-severity alert threshold (e.g., warning level) is met and sustained throughout the detection period, the alert escalates. A high\-severity notification is sent even during the low\-severity silence period, and the high\-severity silence period begins.

* If the triggering threshold is lower than the high\-severity threshold during a high\-severity silence period (e.g., warning), the alert is downgraded. The system will restart the low\-severity detection period.

* If multiple alert levels are triggered at the same time, only the highest\-severity alert is sent.

* Alert recovery occurs only after alerts of all severity levels are cleared.


<span id="ntcghrJH"></span>
## Prerequisites

To receive alerts in Feishu, DingTalk, or WeCom, you need to configure the relevant webhook URLs in advance. For more details, refer to the following topics:


* [Receive alert notifications via Feishu group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups)

* [Receive alert notifications via DingTalk group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups)

* [Receive alert notifications via WeCom group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups)


<span id="MOg1pTWj"></span>
## Procedure

<span id="1QDQ2axt"></span>
### Step 1: Configure alert contacts


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Notification** \> **Contacts**.

3. Click the **Contacts** tab and click **Create a contact**

4. Enter **Name**, **Email**, and **Mobile number** of the alert contact.

5. Click **Create and send verification** to verify the contact information.

   After you create the contact, Cloud Monitor will send a verification message to the specified email address or phone number. After you receive the verification message, you need to click the link in the message within 24 hours to complete the verification. Otherwise, you will not be able to receive alert or event notifications as expected.

   The following figure shows the verification message sent to an email address.

6. After verification, the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_194bb036d910b97de4b966af2f178341.png) </span>in the email and mobile columns means that the notification channel has been successfully verified.


<span id="1QDQ2axt"></span>
### Step 2: Configure alert contact group


1. In the left navigation bar, click **Notification** \> **Contacts**.

2. Click the **Contact group** tab and click **Create a contact group**. Create a contact group and add the corresponding alert contacts.

3. Click **Create** to complete the configuration.


<span id="1QDQ2axt"></span>
### Step 3: Configure a notification policy


1. In the left navigation bar, click **Notification** \> **Notification policy**.

2. On the **Notification policy** page, click **Create a notification policy** to configure an alert notification policy. In the **alert level** option, add all the alert levels and configure the notification channels for each level. (In this example, phone is selected as the alert channel for **Critical** level, email for **Warning** level, Feishu for both **Notification** and **Recovery** levels.)

3. Click **Confirm** to complete the configuration.


<span id="3rIEf6VQ"></span>
### Step 4: Configure an alert policy


1. In the left navigation bar, click **Alert Center \> Alert policy**.

2. On the **Alert policy** page, click **Create alert strategy**. Configure an alert policy. This topic uses the CPU of an ECS instance as an example.

   * Configure the basic information of the alert policy.

   * In **Alert object** section, set **Resource type** to **ECS** and **Dimension** to **Instance**.

   * Configure the alert rule. In **Trigger condition**, select **Out\-of\-band CPU usage**, and then configure the thresholds for different alert levels. (In this example, Critical \> 80%, Warning \> 60%, Notification \> 40%)

   * Configure the alert method. In **Notification method**, select **Notification policy** and choose the alert notification policy you have created, so as to assign different notification channels to different alert levels.

3. Click **Create** to complete the configuration.


<span id="zoaDVXjV"></span>
## Verifying results

<span id="1wp0fbsu"></span>
### View settings

In the alert policy list, view the created alert policies. You can see that different severity levels have different alert thresholds.

Click an alert policy name to enter the alert policy details page, where you can view the details of that policy.

<span id="wYfBnpVF"></span>
### View and receive alerts

When the threshold defined in a monitoring metric is met, the system generates an alert log based on the alert level, and then sends out alert notifications via the channels configured in the alert notification policy. For example, if a **notification** alert is triggered, you can check the alert log and receive the notification in Feishu.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, select **Alert Center \> Alert History**. View the alert log.

3. In the Feishu alert group, you can view the **notification** alerts.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In this example, when the thresholds for <strong>Warning</strong> and <strong>Critical</strong> alerts are met, you will receive notifications via both email and phone.   </div>
