---
title: "Alarm policy testing"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/alarm_tests"
---

Log Service supports testing alarms and previewing alarm notifications when configuring alarm policies. This document describes the precautions and operation steps for alarm testing.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

After configuring an alarm policy in Log Service, you may encounter issues such as alarm content not meeting expectations or alarm notifications not being received. To facilitate troubleshooting of abnormal scenarios and preview alarm notifications in advance, you can debug using the alarm testing feature when creating or editing an alarm policy.

The delivery of alarm notifications is affected by multiple factors, including alarm configuration issues, callback address accessibility, and rate limits of various channels. Therefore, tests may pass but actual production alarms might not be received. For abnormal issues, please contact your account manager for assistance.

<span id=".5rWL6K-V5ZGK6K2m"></span>
## Test alarm

When creating or editing an alarm policy, you can preview the alarm notification using the alarm testing feature. After sending the alarm test message, you can view the alarm notification on the corresponding channel. Refer to [creating alarm policies](https://docs.byteplus.com/docs/tls/create_alarm_policies) for the steps to create an alarm policy.

**The testing function is used only to check whether the alarm policy configuration is correct and does not actually perform alarm monitoring tasks. During testing, the system sends alarm notifications directly without considering the alarm triggering conditions. Therefore, some alarm variables in the notification will not work, and their parsed results will be empty.** 


* If the test is successful, the page will display **test successful**.

* If the alarm triggering condition, custom interface callback address, or other alarm configurations are incorrect, the alarm test will return corresponding error messages. You can troubleshoot configuration issues based on these messages and try again. For common causes and solutions for alarm test failures, see [common reasons for test failures](https://docs.byteplus.com/docs/tls/alarm_tests#.5rWL6K-V5aSx6LSl55qE5bi46KeB5Y6f5Zug).


<span id=".5rWL6K-V5aSx6LSl55qE5bi46KeB5Y6f5Zug"></span>
## Common reasons for test failures

When creating an alarm policy, you can preview alarm notifications and verify the correctness of the alarm policy configuration through alarm testing. This article lists error codes related to alarm testing, along with their causes and solutions.


|Error Code |Error message |Error cause |How to fix it |
|---|---|---|---|
|AlarmProjectNotExist |The log project (%s) does not exist |The project monitored by the alarm has been deleted. |Create a new log project and log topic, upload logs, then recreate the alarm policy in the new log project. |
|AlarmParseSQLErr |Failed to parse alarm execution statement %d: %s |There is a syntax error in the execution statement you provided. |Debug the query and analysis statement in the **Execute Statement** dialog until the preview shows the expected analysis result. For explanations about the query and analysis statement, refer to [Query Overview](https://docs.byteplus.com/docs/tls/Query-overview-2) and [Analysis Overview](https://docs.byteplus.com/docs/tls/Analysis-overview). |
|AlarmParseTriggerConditionErr |Failed to parse alarm trigger condition %d: %s |The trigger condition expression you entered contains syntax errors. |Modify the trigger condition expression in the alarm policy according to the error message. For details, refer to [trigger condition expression](https://docs.byteplus.com/docs/tls/trigger_condition_expressions). |
|AlarmNotifyGroupNotExist |Notification group (%s) does not exist |The notification group you selected has been deleted. |Recreate the notification group and bind the new notification group in the alarm policy. |
|ErrAlarmUserDefineMsgParseErr |Failed to parse user\-defined notification content: %s |The notification content you entered contains grammatical errors. |Modify the notification content in the alarm policy according to the error message. For syntax instructions of the notification content, refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables), [content syntax](https://docs.byteplus.com/docs/tls/content_syntax), and [content functions](https://docs.byteplus.com/docs/tls/content_functions). |
|ErrAlarmWebhookBodyParseErr |Failed to parse the request body of the %dth webhook in the notification group (%s): %s |The WebHook request body you provided contains syntax errors. |Modify the WebHook request body according to the error message. |
|ErrAlarmCallWebhookErr |The %dth webhook address in notification group (%s) is incorrect |Failed to call the WebHook address. |Check the availability of the WebHook address in the notification group. |
|ErrAlarmContentTemplateParseErr |Content template (%s) parsing failed: %s |There is a syntax error in the content template you provided. |Modify the content template according to the error message. For detailed instructions, please refer to [creating content templates](https://docs.byteplus.com/docs/tls/content_templates). |
|ErrSendSmsMessageOutOfQuota |User %s exceeded the SMS sending limit |The SMS notification frequency of the specified IAM user exceeds the limit. |Refer to [Alarm Limits](https://docs.byteplus.com/docs/tls/Limits#.5ZGK6K2m) for quota details and try again later. |
|ErrMobileNotVerified |User %s phone not verified |The phone number configured in the personal information of the specified IAM user has not been verified. |Complete phone verification on the [Security Settings page](https://console.byteplus.com/user/security/). |
|ErrSendVmsMessageOutOfQuota |User %s phone exceeds the limit |The specified IAM user's phone notification frequency exceeds the quota. |Refer to [alarm limits](https://docs.byteplus.com/docs/tls/Limits#.5ZGK6K2m) for quota details and try again later. |
|ErrEmailNotVerified |User %s email is not verified |The specified IAM user's email configured in their profile is not verified. |Complete the email verification on the [security settings page](https://console.byteplus.com/user/security/). |
|ErrSendSmsFail |User %s failed to send SMS: %s |SMS notification failed to send. |Check your phone settings according to the error prompt and try again later. |
|ErrSendVmsFail |User %s voice notification failed: %s |Failed to send voice notification. |Check your phone settings according to the error message and try again later. |
|ErrSendEmailFail |User %s failed to send email: %s |Failed to send email notification. |Check the email settings based on the error message and try again later. |
|ErrWebhookIntegrationNotExist |The alarm webhook integration (%s) does not exist. |The WebHook integration configuration you set has been deleted. |Recreate the WebHook integration configuration and bind the new WebHook integration configuration in the notification group. |
|ErrCallWebhookIntegration |Alarm webhook integration (%s) call failed, error code: %v, error message: %s |Calling the WebHook address failed. HTTP status code shows success, but sending alarm notifications to Feishu, DingTalk, and WeChat Work failed. |Check and modify the webhook integration configuration according to the error prompt and try again later. |
|AlarmDefaultErr |Alarm test failed, try again later |None. |Try again later. |
