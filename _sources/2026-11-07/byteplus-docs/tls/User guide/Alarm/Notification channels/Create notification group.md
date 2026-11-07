---
title: "Create notification group"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/create_alarm_notification_groups"
---

Log Service notification groups collect alarm notification channels used to specify action strategies after an alarm is triggered. You can add notification rules, and Log Service will intelligently assign different alarm notification channels based on these rules. This document describes the steps to create a notification group.

<span id="2c646d92"></span>
## Prerequisites


* When alarm notification channels are email, ensure that IAM users or groups are created, and that IAM users have completed security phone and email verification on the [security settings page](https://console.byteplus.com/user/security/).

* The alarm notification channels are DingTalk and WeCom. When the **alert method** is set to **specified person**, please ensure that an IAM user or user group has been created and that the IAM user has completed mobile phone and email verification on the [security settings page](https://console.byteplus.com/user/security/).

* When the alarm notification channels are DingTalk, WeCom, or custom Webhook, please ensure that the Webhook integration configuration has been created. Please refer to [Creating Webhook integration configuration](https://docs.byteplus.com/en/docs/tls/Create_Webhook_Integration_Configuration) for the operation steps.

* When creating a notification group using an IAM user, please ensure that this IAM user has permission to view other IAM users, specifically including `iam:ListUsers` in its permission policy.


<span id="705b0f13"></span>
## Background

Log Service manages alarm notification action policies and notification entities through notification groups. Using the notification rules and channels defined in a notification group, Log Service can dynamically assign different alarm notification channels for each alarm. Alarms triggered during off\-hours are sent via email, etc.

The following notification channels are supported by Log Service:


* Email: recipients are specified IAM users or all users in the specified IAM user group. Alarm notifications are sent via email to the IAM user's mobile phone or mailbox.

* DingTalk, WeCom, custom Webhook: manage DingTalk/WeCom robot WebHook addresses or other custom Webhook addresses, such as self\-built systems or third\-party alarm systems  [Ruixiang Cloud](https://www.aiops.com/)  Cloud Alert, through WebHook integration configuration. After binding the corresponding Webhook integration configuration in the notification group, the alarm system sends alarm notifications to the specified Webhook address according to that configuration. For detailed instructions, refer to [Creating Webhook Integration Configurations](https://docs.byteplus.com/en/docs/tls/Create_Webhook_Integration_Configuration).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Steps


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **log alarm** \> N**otification management**.

4. On the N**otification management** page, under the N**otification groups** tab, click **Create Notification Group**.

5. Set the N**otification group name**.

6. Set the N**otification policy**.

   The notification policy controls the channels for alarm notifications, including notification rules and notification channels.

   1. Click A**dd rule**.

   2. Add alarm notification rules in the **rule** dialog.

      * Notification rules can be specified by notification type, alarm level, alarm policy name, alarm policy ID, duration, and notification time. Multiple conditions can be combined with AND or OR logic.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The recovery notification content automatically ignores any additional notification content set when creating the alarm policy. You can set the <code>{{NotifyType}}</code> variable in the content template to distinguish between recovery notifications and alarm notifications.         </div>
         

      * Alarms match rules sequentially from top to bottom. When a rule is met, the notification channel for that rule sends the alarm notification.

      * Each notification group can have up to 50 rules, and each rule can include up to 10 notification channels.

   3. Set the notification channel in the **notification channel** dialog.

      
      |Configuration |Description |
      |---|---|
      |Notification period |The time period during which Log Service sends alarm notifications. The logging service sends alarm notifications only when the alarm is triggered within the specified notification period. |
      |Channel Type |The channels used by the log service to send alarm notifications. After triggering an alarm, the log service reads the recipient's information and sends an alarm notification. Supports setting one or more channels. The details are as follows:<br><br><br>* Email: Sends alarm notifications to IAM users or user groups via email.<br><br>* Custom Webhook: Send alarm notifications to a specified Webhook address.<br><br>* DingTalk: Send alarm notifications to a DingTalk group.<br><br>* WeCom: Send alarm notifications to a WeCom group.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting a receiving channel, ensure the specified channel can reach the target users. You can also verify channel accessibility using the alarm test function when creating an alarm policy.</div><br> |
      |Receiving channels |When setting the **channel type** to Email, or custom Webhook, select one or more notification channels. |
      |Recipients |The IAM user or user group receiving alarm notifications. If specified as a user group, alarm notifications will be sent to all IAM users in this notification group. For details, please refer to [user group management](https://docs.byteplus.com/en/docs/tls/manage_alarm_notification_groups).<br><br>This setting is required only when **receiving channels** include **email**. |
      |Webhook |Webhook integration configuration.<br><br>You can click **Create** to create a new Webhook integration configuration or click the **Webhook** dropdown to select an existing Webhook integration configuration. For detailed instructions, refer to [Creating Webhook Integration Configuration](https://docs.byteplus.com/en/docs/tls/Create_Webhook_Integration_Configuration).<br><br>When the **channel type** is DingTalk, WeCom, or custom Webhook, configuration is required. |
      |Content Template |The specific content of the alarm notification. The log service will send alarm notifications according to the content defined in the template.<br><br>You can click **New** to create a new content template, or click the content template dropdown to select an existing template. For detailed instructions, refer to [Creating Content Template](https://docs.byteplus.com/docs/tls/content_templates).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When setting the <strong>alert method</strong> to <strong>everyone</strong> or <strong>specified people</strong>, WeCom notifications use plain text format and do not support Markdown format.</div><br> |
      |Alert method |Set alert notification methods for DingTalk groups, and WeChat Work groups.<br><br><br>* **No alert**: only send alert notifications to DingTalk groups, or WeChat Work groups.<br><br>* **Everyone**: send alert notifications to DingTalk groups, or WeChat Work groups and notify all group members to check the alert.<br><br>* **Specified people**: send alert notifications to DingTalk groups or WeChat Work groups and notify designated group members to check the alert.<br><br>   When setting the **notification channel** to **DingTalk** or **WeChat Work**, specifying individuals is supported, meaning you can designate the corresponding IAM users or user groups.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When setting the <strong>alert method</strong> to <strong>Specified people</strong>, the IAM user's phone number must be a mainland China number.   </div><br>    |
      

7. Select the **associated project**.

   Select the IAM project to which the newly created notification group belongs from the dropdown list.

   If you have not created any IAM project or cannot find a suitable one, click **Create new project** to create an IAM project. If no IAM project is specified, the log service adds the notification group to the IAM project named `default`.

8. Click **Create notification group**.


<span id="4bc03d47"></span>
## Related actions

Disable recovery notifications:

The log service sends alarm notifications and recovery notifications to specified channels by default. If you do not want to receive recovery notifications, you can specify to receive only alarm notifications through **notification types**. For detailed steps, refer to [How to disable alarm recovery notifications?](https://docs.byteplus.com/en/docs/tls/Alarm-faq).
