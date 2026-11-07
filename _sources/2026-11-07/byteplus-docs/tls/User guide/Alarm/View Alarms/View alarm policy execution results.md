---
title: "View alarm policy execution results"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/View_alarm_policy_execution_results"
---

The log service console provides detailed displays for all alarm policies, including basic information of the alarm policy, monitoring details, and execution information of the alarm policy.

<span id=".5p-l55yL562W55Wl5L-h5oGv"></span>
## View policy information

The **alarm policy** list displays the alarm policy name, ID, current application status, and monitored Topic object information. Click the alarm policy name to enter the **policy information** tab, which shows the basic alarm information, monitoring details, and alarm data.


* In **basic information**, you can directly enable or disable the current alarm policy.

* If the alarm policy does not meet the current business monitoring alarm requirements, click **edit** in the upper right corner to modify the current alarm policy.


<span id=".5p-l55yL5omn6KGM5L-h5oGv"></span>
## View execution information

The **execution information** tab presents recent alarm policy execution status through a built\-in dashboard. The dashboard defaults to displaying execution data for the past 30 minutes, including charts such as:


|Chart |Description |
|---|---|
|Alarm count |The number of times a monitoring task successfully executes according to the specified execution cycle. For example, the log service executes a query and analysis statement every 15 minutes based on the alarm policy and checks whether the trigger conditions and sending cycle requirements are met. If this alarm monitoring runs 10 times, the alarm count is 10. |
|Execution success rate |The ratio of monitoring tasks that are successfully or partially successfully sent to all alarm monitoring task executions.<br><br>For example, log service executes a query and analysis statement every 15 minutes according to the alarm policy, determining whether it meets the trigger conditions and sending cycle requirements. If 10 alarm monitoring tasks are executed, triggering one alarm notification which is sent successfully, the execution success rate is 10%. |
|Alarm trigger trend |The trend of alarm policy trigger counts over time. |
|Alarm history |Execution history of the alarm policy monitoring tasks. Please refer to the table below for detailed explanations.<br><br>You can also click **View Details** in the last column to go to the query and analysis page of the corresponding log topic and check the query and analysis results of this monitoring task. |


The field descriptions of **alarm history** are as follows.


|Display items |Description |
|---|---|
|Execution time |Execution time of the monitoring task under the current alarm policy. |
|Notification status |Whether the alarm notification has been sent.<br><br><br>* All sent successfully: alarm notifications have been successfully sent to the corresponding notification groups.<br><br>* Partially sent successfully: alarm notifications have been sent to the corresponding notification groups, but some users were not reached due to issues like unreachable notification channels or not set to receive that type of alarm notification.<br><br>* Sending failed: alarm notification failed to send.<br><br>* Not sent: alarm notification was not sent. Determine the specific reason based on the **execution result**. |
|execution result |The execution result of this task. For detailed information, please refer to the [execution result description](https://docs.byteplus.com/docs/6470/103029#.5omn6KGM57uT5p6c6K-05piO). |
|details |Detailed description of the specified result, used to determine the specific cause of the issue. |
|Trigger condition |Configured trigger condition and expression format in the alarm policy. |
|Monitored object |Name of the monitored topic. |
|alarm group |The notification group corresponding to the alarm policy. |
|View details |Navigate to the target log topic's inspection and analysis page to view the query and analysis statements and results set in the current alarm policy. |


<span id=".5omn6KGM57uT5p6c6K-05piO"></span>
### Execution result description

The types and descriptions of alarm execution results are as follows.


|Execution result |Description |
|---|---|
|Missing alarm policy configuration. Please check if the alarm policy and monitored object configurations are correct |No alarm policy configured.<br><br>Check whether the alarm policy and monitoring object configuration are correct. |
|The analysis statement for the monitored object has a syntax error. Please check if the statement is correct. Refer to analysis statement syntax |The monitored object's analysis statement contains search or analysis syntax errors.<br><br>Please check the syntax correctness based on the document's [search syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) and [analysis syntax](https://docs.byteplus.com/docs/tls/Analysis-overview#%E5%88%86%E6%9E%90%E8%AF%AD%E6%B3%95). |
|Analysis statement execution exception; please check the analysis statement and log topic index configuration. |The analysis statement execution encountered an exception.<br><br>Please check the syntax according to the document [query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) and [analysis syntax](https://docs.byteplus.com/docs/tls/Analysis-overview#%E5%88%86%E6%9E%90%E8%AF%AD%E6%B3%95) for correctness, and verify that the index is configured properly. |
|Failed to parse analysis result format |Failed to parse the analysis results format.<br><br>Check if the syntax is correct based on the document’s [query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) and [analysis syntax](https://docs.byteplus.com/docs/tls/Analysis-overview#%E5%88%86%E6%9E%90%E8%AF%AD%E6%B3%95). |
|Alarm triggering conditions are met, but the alarm convergence threshold is not reached, so no alarm notification is sent: the cycle convergence condition is not met, for example, the alarm triggers only after 5 consecutive monitoring cycles; the alarm interval condition is not met, for example, alarms trigger every 15 minutes |Meets the alarm trigger conditions but does not meet the **alarm sending cycle** requirements, so no alarm notification is sent temporarily. For example:<br><br><br>* Does not meet the alarm monitoring cycle requirements, such as requiring continuous monitoring for 5 cycles to trigger the alarm, but currently only 1 cycle has been continuous.<br><br>* Does not meet the alarm interval requirements, such as sending an alarm notification every 15 minutes, but only 5 minutes have passed since the last alarm notification. |
|The alarm notification type does not match the notification template (alarm notification, alarm recovery) |The alarm notification type (alarm notification, alarm recovery) does not match the notification group settings, so no alarm notification is sent. |
|alarm notification time outside the notification template period |The alarm trigger time does not match the alarm notification time period specified by the notification group, so the alarm notification will not be sent. |
|notification sending failed |The log service attempted to send alarm notifications but failed due to notification channel frequency control limitations or other reasons |
|Meets the alarm conditions and successfully notifies the alarm. |Alarm sent successfully. |
|Internal service error. Alarm execution failed |Due to some internal reasons, the alarm monitoring task failed to execute. |
|Trigger conditions not met |The analysis results of the current monitoring cycle do not meet the alarm trigger conditions. |
|Some alarms were sent successfully |Alarm notifications successfully sent through some channels. |
|Alarm expression syntax error |Syntax error in alarm trigger condition expression.<br><br>It is recommended to debug the expression using the alarm test function and confirm its correctness before enabling the alarm policy. |
|Alarm expression calculation error |The trigger condition expression failed to execute.<br><br>Check whether the analysis result contains variables referenced by the trigger condition expression. |
|Alarm expression result type error |The trigger condition calculation result is not a boolean value, so it cannot determine whether the alarm triggers based on the condition.<br><br>Verify whether the trigger condition expression is correct. |
