---
title: "Alarm policy frequently asked questions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Alarm_strategy_FAQs"
---

<span id="510ef276"></span>
## How to avoid missed alarms and false alarms?

There is low latency from log writing to querying, and minimal time difference in index building. If you do not take these timing differences into account when configuring the query time range and execution cycle in the alarm policy, the query results of alarm monitoring tasks may be inaccurate, which can lead to missed alarms or false alarms.

You can avoid missing alerts and false alerts by expanding the query time range. For a detailed explanation, please refer to [Timeliness of alarm monitoring tasks](https://docs.byteplus.com/docs/tls/Alarm_Monitoring_Task_Timeliness).

<span id="3e95d090"></span>
## Why does only one trigger condition take effect when multiple are configured?

The alert trigger conditions in TLS use an OR relationship. Query and analysis results are matched sequentially according to the order of the trigger conditions. Once a query and analysis result matches the first trigger condition, the subsequent trigger conditions are no longer checked. That is, when adding multiple trigger conditions, you must configure them in order from the highest to the lowest level. For detailed steps, please refer to [Create alarm policy](https://docs.byteplus.com/docs/tls/create_alarm_policies).

<span id="536108b2"></span>
## Why is there a significant difference between the alarm trigger time and the notification time?

When using the default content notification template of TLS, the trigger time value is `{{StartTime}}`, which indicates the time when the alert was first triggered. After an alarm is triggered, if it has not recovered in the next cycle, the trigger time shown in the second alarm notification will still be the time when the alarm was first triggered in the previous cycle. If an alert remains unresolved, the alert trigger time will not be updated, which may result in a significant difference between the alert trigger time and the notification time.

<span id="06284689"></span>
## Why is the `COUNT(*)` result 0, but the "has data" alert condition I configured is still triggered?


* Phenomenon

   When creating an alarm policy, use the `COUNT(*)` function to count the number of relevant logs, and set the **trigger condition** to `has data`. When the result of `COUNT(*)` is 0, an alert is still triggered.

* Cause

   When using the `COUNT(*)` function, the returned result will always contain one row of data, which shows the result of the `COUNT(*)` function calculation. When the **trigger condition** is set to `has data`, it means that the result will be triggered whenever there are data rows in the returned result. Therefore, even if the result of `COUNT(*)` is 0, meaning that no logs meet the criteria, an alert will still be triggered.

* Solution

   Use the result columns from query and analysis to set trigger conditions. For example, setting the **trigger condition** to `there is data matching $1.num >= 1` means that the alert will be triggered only if at least one log entry meets the criteria.


<span id="3355127d"></span>
## Why do the query and analysis results have data, but the variable value is empty in the alert test notification?

Alarm testing is intended only for checking configurations such as alarm policy, query and analysis syntax, trigger expression syntax, and other related settings, and does not actually perform alarm monitoring tasks. When your alarm policy is relatively complex, the alarm test cannot detect issues, and you need to manually troubleshoot according to the alarm documentation.

<span id="15ccb575"></span>
## Why does the trigger condition expression prompt that a field does not exist?


* Phenomenon

   Note: The trigger condition expression indicates that the target field may not exist.

* Solution

   When referencing a field as a variable in a trigger condition expression, please ensure that the target field exists in the query and analysis result set. If an error still occurs when storing the target field, please ignore the error.


<span id="d3f08469"></span>
## Alarm test error codes

When creating an alarm policy, you can use the alarm test to preview alarm notifications and verify that the alarm policy configuration is correct. This document lists error codes related to alarm testing, their causes, and solutions.


|Error codes |Error message |Cause of error |Solution |
|---|---|---|---|
|AlarmProjectNotExist |Project (%s) does not exist |The alarm monitoring project has been deleted. |Create a new log project and log topic, upload logs, and then recreate the alarm policy in the new log project. |
|AlarmParseSQLErr |Failed to parse alarm execution statement %d: %s |There is a syntax error in the execution statement you entered. |In the **Execute Statement** dialog box, debug the query and analysis statement until you preview analysis results that meet the requirements. For information about query and analysis statements, refer to [Query overview](https://docs.byteplus.com/docs/tls/Query-overview-2) and [Analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview). |
|AlarmParseTriggerConditionErr |Failed to parse alarm trigger condition %d: %s |There is a syntax error in the trigger condition expression you entered. |Modify the trigger condition expression in the alarm policy according to the error message. For a detailed explanation, please refer to [the trigger condition expression](https://docs.byteplus.com/docs/tls/trigger_condition_expressions). |
|AlarmNotifyGroupNotExist |Notification group (%s) does not exist |The notification group you selected has been deleted. |Recreate the notification group, and bind the new notification group in the alarm policy. |
|ErrAlarmUserDefineMsgParseErr |Failed to parse user\-defined notification content: %s |There is a grammatical error in the notification content you entered. |Modify the notification content in the alarm policy based on the error prompts. For an explanation of notification content syntax, refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables), [content syntax](https://docs.byteplus.com/docs/tls/content_syntax), and [content functions](https://docs.byteplus.com/docs/tls/content_functions). |
|ErrAlarmWebhookBodyParseErr |Failed to parse the request body of webhook #%d in notification group (%s): %s |The syntax of the WebHook request body you provided is incorrect. |Modify the WebHook request body according to the error message. |
|ErrAlarmCallWebhookErr |The %dth webhook address in notification group (%s) is invalid |Failed to call the WebHook address. |Check the availability of WebHook addresses in the notification group. |
|ErrAlarmContentTemplateParseErr |Failed to parse content template (%s): %s |There is a syntax error in the content template you filled in. |Modify the content template according to the error message. For detailed instructions, refer to [Create a content template](https://docs.byteplus.com/docs/tls/content_templates). |
|ErrSendSmsMessageOutOfQuota |User %s has exceeded the SMS sending limit |The SMS notification frequency for the specified IAM user has exceeded the limit. |Refer to [alert limits](https://docs.byteplus.com/en/docs/tls/Limits#alarm-limits) for information about limits, and try again later. |
|ErrMobileNotVerified |The phone number of user %s is not verified. |The mobile phone number configured in the personal information of the specified IAM user has not been verified. |Complete security phone verification on the [security settings page](https://console.byteplus.com/user/security/). |
|ErrSendVmsMessageOutOfQuota |User %s's phone usage exceeds the limit |The phone notification frequency for the specified IAM user has exceeded the limit. |Refer to [alert limits](https://docs.byteplus.com/en/docs/tls/Limits#alarm-limits) to learn about the limit, and try again later. |
|ErrEmailNotVerified |User %s's email is not verified |The email configured in the personal information of the specified IAM user has not been verified. |Complete security email verification on the [security settings page](https://console.byteplus.com/user/security/). |
|ErrSendSmsFail |User %s failed to send SMS: %s |Failed to send SMS notification. |Check your phone settings as indicated by the error message, and try again later. |
|ErrSendVmsFail |Voice notification failed for user %s: %s |Voice notification failed to send. |Check your phone settings as indicated by the error message, and try again later. |
|ErrSendEmailFail |Failed to send email for user %s: %s |Failed to send email notification. |Check your email settings according to the error message, and try again later. |
|ErrWebhookIntegrationNotExist |Alert webhook integration (%s) does not exist |The WebHook integration configuration you set up has been deleted. |Recreate the WebHook integration configuration, and bind it to the notification group. |
|ErrCallWebhookIntegration |Alarm webhook integration (%s) invocation failed. Error code: %v, error message: %s |Failed to invoke the WebHook address; the HTTP status code indicates success, but sending alert notifications to Feishu, DingTalk, and WeCom failed. |Check and modify the WebHook integration configuration according to the error message, then try again later. |
|AlarmDefaultErr |Alarm test failed. Please try again later. |None. |Try again later. |
