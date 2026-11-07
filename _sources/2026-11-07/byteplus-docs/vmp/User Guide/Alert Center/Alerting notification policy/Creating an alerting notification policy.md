---
title: "Creating an alerting notification policy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules"
---

The alerting notification policy is used to specify contact groups that will receive alerts when alerts at different levels are triggered. This topic describes how to configure an alerting notification policy.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The new Alert Center is available. It provides comprehensive upgrades and optimizations for features such as notification policies, notification templates, aggregation policies, and suppression policies. We recommend configuring notification policies in the new <a href="https://console.byteplus.com/observe/alert/notify/rules">Alert Center</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A contact is created, and the alert reception method is configured for the contact. For more details, see [Creating contacts](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receivers).

* An alerting contact group is created. For more details, see [Creating contact groups](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receiver-groups).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A root account and its IAM users can create up to 20 alert notification policies in total.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting notification policy**. Click the **Policy list** tab.

4. Click **Create notification policy** and configure the alerting notification policy.

   * **Basic information**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Notification policy name |Specify the name of the alerting notification policy. |
      |Description |Specify the description of the alerting notification policy. |
      

   * **Alert notification policy**

      Specify the alert level, notification recipient, and notification method for the alert notification policy based on the following table.

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Alert Level |Select an alert level from the drop\-down list. Valid values: P0, P1, P2, and Resolved.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can configure only one alerting notification policy for each level of alert. If the alert level in the list is unavailable, an alerting notification policy is already configured for the level of alert.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Resolved: The resolved state level after an alert is triggered, which is used to indicate that the alert has returned to normal (The metric value has returned to within the normal threshold range). This prevents operation and maintenance personnel from repeatedly troubleshooting issues that are already addressed.</div><br> |
      |Notifier |In the **All contact groups** section, select the check boxes before the names of the contact groups that need to receive alerts to add them to the **Selected contact group** section. |
      |Notification method |Select an alerting notification method from the Notification method list. Valid values:<br><br><br>* **Generic webhook**: Alerting notifications are received by standard webhook. For the format of the generic webhook, see [Generic webhook format description](https://docs.byteplus.com/en/docs/vmp/general-webhook-format).<br><br>* **Mail**: Alerting notifications are received by email. For more details, see [Receiving alerting notifications by email](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email).<br><br>* **Larkbot**: Alerting notifications are received by Larkbot. For more details, see [Receiving alerting notifications by custom Larkbot](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark).<br><br>* **Lark application bot**: Alerting notifications are received by Lark application robot. For more details, see [Receiving alerting notifications by Lark application robot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot).<br><br>* **DingTalk robot**: Alerting notifications are received by DingTalk robot. For more details, see [Receiving alerting notifications by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk).<br><br>* **WeCom robot**: Alerting notifications are received by WeCom robot. For more details, see [Receiving alerting notifications by WeCom](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom).<br><br>* **Telephone**: Alerting notifications are received by phone. For more details, see [Receiving alerting notifications by phone](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone).<br><br>* **SMS**: Alerting notifications are received by text message. For more details, see [Receiving alerting notifications by text message](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-SMS).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Phone notifications are supported only by P0\-level alerts.</div><br> |
      

   * Configure message templates. Configure custom message templates sent across different channels. If you have not configured a template, the system default template is used to send notifications. For more details, see [Creating notification templates](https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template).

5. Click **Confirm** to complete the configuration.
