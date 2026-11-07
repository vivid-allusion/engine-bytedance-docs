---
title: "Common alert failures"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Alarm_common_faults"
---

<span id="a5c5003d"></span>
## Failure to receive alert emails


1. Check whether the contact information of the selected contacts is valid.

2. If notifications are still not received, check whether the email address used to send alert notifications has been added to the allowlist.

   The platform uses the **monitor@monitor.volces.com** email address to send alert emails. Make sure that this email address has been added to the allowlist or related policies of the contact email address to prevent alert emails from not being received or from being sent to the spam folder by default.


<span id="cf020be5"></span>
## Failure to trigger alerts

If an alert cannot be triggered, it indicates that the alert metric has reached the alert threshold, met the continuous alert constraint, and satisfied the multi\-metric condition, but the rule status has not changed to alerting, and no alert record has been generated.


1. Confirm that the alert has not been triggered.

   Check whether related alert records exist.

   * If related alert records exist, it indicates that the alert has been triggered.

   * If related alert records do not exist, it indicates that the alert has not been triggered.

2. Confirm whether the alert conditions are met.

   In the alert policy, view the monitoring dashboard for the corresponding resource and metric, and check whether the alert threshold and continuous alert constraint are met.

   * Alert threshold: The trigger condition is met when the metric value exceeds the alert threshold.

   * Continuous alert constraint: The trigger condition is met, and the metric value has exceeded the alert threshold for N consecutive periods.

   * Multi\-metric condition: When multiple metrics are configured in an alert rule, an alert is triggered if all metrics or any one of the metrics meet the condition.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The alert is triggered only if all preceding three conditions are met. Therefore, you need to confirm that all three conditions are met.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For monitoring objects with multiple nodes, make sure that the node for which the alert is triggered is selected.   </div>
   

3. If you confirm that the alert has not been triggered and the alert rule is satisfied, but the alert still cannot be triggered, submit a ticket in the console and provide a screenshot of the alert policy, a screenshot of the monitoring dashboard, and the alert policy ID in the ticket.


<span id="aa92ce6b"></span>
## Failure to receive messages or callback messages after alerts have been triggered


1. On the **Alert history** page, find the target alert record and click **Details** in the Actions column.

2. On the **Overview** page, view the **Alert notification** records.

   * If alert notifications fail to be sent, you can view the corresponding details.

   * If alert notifications have been sent but you still do not receive a message or callback message, perform troubleshooting based on the following table.

      
      |Alert notification method |Check method |
      |---|---|
      |Email |Check the spam folder. |
      |Text message |Check whether the SMS message is blocked. For example, check whether it is recognized by the phone as a spam SMS message. |
      |Phone call |Check whether the phone call is blocked. For example, check whether it is recognized by the phone as a spam call. |
      |Alert callback |* Feishu: open.feishu.cn. Cloud Monitor identifies Feishu messages based on the domain prefix. You need to check whether the callback URL is correct and whether the bot is set to filter messages by keyword.<br><br>* DingTalk: oapi.dingtalk.com. Cloud Monitor identifies DingTalk messages based on the domain prefix. You need to check whether the callback URL is correct and whether the bot is set to filter messages by keyword.<br><br>* WeCom: qyapi.weixin.qq.com. Cloud Monitor identifies WeCom messages based on the domain prefix. You need to check whether the callback URL is correct and whether the bot is set to filter messages by keyword.<br><br>* Other webhooks: Check whether the callback URL is valid. |
      

3. If you still cannot locate the issue after checking all items, submit a ticket in the Cloud Monitor console.

   To quickly locate your issue, you need to provide the following information in the ticket:

   * Screenshot displaying that the alert is triggered

   * Screenshot displaying that the alert is sent or fails to be sent

   * The interception status on the receiving terminal


<span id="cbafa184"></span>
## Alert messages are received, but related resources are normal

After an alert message is received, check whether the relevant metrics meet the alert rule. This is not directly related to whether the resources are normal.

Troubleshooting methods:


* Check whether the configured alert metrics are appropriate.

* Check whether the configured alert threshold is appropriate.


<span id="1fa1239b"></span>
## Failure to receive alert recovery notifications

Check whether the alert recovery notification feature has been enabled in the target alert rule.

<span id="7baee649"></span>
## Failure to receive event alert messages

If an event rule is configured but no message is received, perform the following steps for troubleshooting:


1. View the event list and confirm that events that correspond to the event rule exist.

   For example, if the event name in the event rule is `primary/secondary switchover (failover) of the instance`, check whether related events exist in the cloud product event list.

   * If no corresponding events exist, no event alerts will be generated.

   * If corresponding events exist, proceed with the following steps.

2. Check whether the notification address is correct.

3. If you have confirmed that the event rule and notification address are correct but still cannot receive messages, submit a ticket in the console and provide the event rule ID in the ticket.
