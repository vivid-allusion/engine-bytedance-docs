---
title: "Alarm overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/alert_overview"
---

The log service provides an integrated monitoring and alarm function. The log service alarm supports real\-time data monitoring, alarm policy, and notification management, suitable for operation and maintenance scenarios.

<span id=".5Yqf6IO95LuL57uN"></span>
## feature introduction

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The log service alarm feature is currently in public beta and does not charge any fees for SMS or voice notifications. Please refer to future product announcements for the end of the public beta period and billing policies.</div>


In enterprise\-level operation and maintenance scenarios, once massive log data is collected and stored in the log service, you can use the log service alarm feature to monitor various application service data indicators in real time and realize alarm process management. When using the log service alarm feature, you need to set alarm policies and notification groups for the specified log topic. The log service runs monitoring tasks regularly according to the cycle specified in the alarm policy to retrieve and analyze data within the monitoring scope. If the retrieval and analysis results meet the trigger conditions, alarm notifications are sent to the specified recipients.

The log service alarm offers the following features:


* **real\-time data monitoring**: The log service provides real\-time log data monitoring based on query and analysis functions. You can configure query and analysis statements in the alarm policy. The log service regularly runs these statements based on the specified policy to monitor changes in the query and analysis results. Query and analysis statements must comply with the log service's query and analysis syntax. For details, refer to [query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) and [analysis syntax](https://docs.byteplus.com/docs/tls/Analysis-overview#.5YiG5p6Q6K-t5rOV).

* **Alarm policy management**: The log service supports setting alarm rules based on real\-time monitoring results of log data to monitor the running status of services. The alarm policy determines the data monitoring scope, alarm trigger timing, notification methods, and other logic.

* **Notification group management**: The log service manages alarm notification channels through notification groups. Once an alarm policy binds to a notification group, alarm notifications are sent to all recipients defined in the group using the specified methods, facilitating timely delivery of alarm information and restoring business operations. Supported channels include email, SMS, phone calls, Feishu, WeCom, DingTalk, custom Webhook, and others.

* **Alarm notification**: Alarm notification content can be set as plain text or designed with content syntax, functions, and variables to deliver more detailed and clear alarm information.

* **Open alarm capabilities**: The log service supports integration with third\-party alarm platforms, such as through [Ruixiang Cloud](https://www.aiops.com/) Cloud Alert's monitoring tool integration, enabling alarm capability connection via a third\-party alarm platform. You can manage log service alarm events through Ruixiang Cloud for streamlined alarm management.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Category |Limit items |Description |
|---|---|---|
|Alarm monitoring |Number of alarm policy |A maximum of 100 alarm policies can be created per log project. A maximum of 10 alarm policies can be created per log topic. |
||Field value length |If the value of a field exceeds 1024 characters, only the first 1024 characters are used for analysis. |
||Time range for query and analysis |The time span of each query and analysis statement can not exceed 24 hours. |
||Query and analysis results |* When there is no aggregation operation, the monitoring task selects up to the first 1000 rows of query and analysis results for alarm triggering; when aggregation operations exist, the monitoring task selects up to the first 1000 rows from the aggregation results for alarm triggering.<br><br>* When associating three monitoring aggregations, the monitoring task selects up to the first 100 rows from each query and analysis result for aggregation. |
||Alarm expression length |The alarm expression length ranges from 4 to 1024 characters. |
|Notification management |Number of notification groups |A maximum of 100 notification groups can be created per region. |
||number of notification channels |For each notification group, up to 10 notification channels can be created. |
||Notification content |The maximum length of notification content is 4096 Chinese characters. |
||Channel notification frequency |The notification frequency limits for each alarm channel in Log Service are as follows.<br><br><br>* Email: no limit.<br><br>* SMS: the maximum frequency for SMS alarm notifications to the same phone number is 10 messages per minute, 100 per hour, and 300 per day.<br><br>* Call: the maximum frequency for voice alarm notifications to the same phone number is 10 calls per minute, 100 per hour, and 300 per day.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports domestic (+86) phone numbers.</div><br> |


<span id=".5L2_55So5rWB56iL"></span>
## Workflow


1. Create content templates.

   Content templates are predefined text templates used to specify the content and format of alarm notifications. Content templates support adding variables, functions, text, and other elements. Log Service supports adding content templates for various notification channels, including email, SMS, phone calls, Feishu, WeCom, DingTalk, and custom Webhook. For detailed steps, refer to [Create content templates](https://docs.byteplus.com/docs/tls/content_templates).

2. Create notification groups.

   Notification groups require configuration of notification types, channels, and other settings. If the notification channel is Feishu, WeCom, DingTalk, or a custom Webhook, you can manage the Webhook address through Webhook integration configuration. For detailed steps, refer to [Create notification groups](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups).

3. Create alarm policies.

   Alarm policies require setting monitoring tasks and alarm rules, and binding notification groups. The monitoring task section defines the monitoring targets, query and analysis statements, and execution cycles for alarm monitoring, while the alarm rule section defines trigger conditions and alarm sending cycles. For detailed steps, refer to [Creating an alarm policy](https://docs.byteplus.com/docs/tls/create_alarm_policies).

4. View alarm details.

   The Log Service regularly executes monitoring according to the specified alarm policy. After an alarm is triggered, you can view detailed alarm information through the no\-login link in the alarm notification or check alarm history via the console. For detailed steps, refer to [Accessing alarm details without login](https://docs.byteplus.com/docs/tls/cccess_the_alarm_details_page_without_logon) and [Viewing alarm history](https://docs.byteplus.com/docs/tls/alarm_history).


<span id=".5Z-65pys5qaC5b-1"></span>
## Basic concepts


|Basic concepts |Description |
|---|---|
|alarm policy |An alarm policy defines how data is monitored and the alarm rules. You need to specify monitoring tasks, alarm rules, alarm notification methods, and other configurations in the policy. |
|Notification group |A notification group is a collection of alarm notification policies that defines the alarm notification type, receiving channels, recipients, and other information. |
|Alarm trigger |Alarm trigger is a type of alarm notification. Send an alarm notification when the monitoring result meets the alarm trigger expression. |
|Alarm recovery |Alarm recovery is a type of alarm notification. Send a recovery notification when the monitored object returns to normal. |
|Content template |The alarm notification content template is a predefined text template used to specify the content and format of alarm notifications. Variables can be added to the content template and will be replaced with actual values when sending notifications. |
|Webhook integration |Log Service supports managing alarm notification channels such as Feishu, DingTalk, and WeCom through Webhook integration. |
