---
title: "Monitor alarm policies"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/view_alarm_policy"
---

This article describes how to monitor alarm policies and promptly receive execution results.

<span id="ab55d3be"></span>
## Background information

By default, after creating an alarm policy, you can view its execution results in the **alarm history** statistics chart. However, the system does not automatically send notifications of execution results by default. For operations on viewing execution results, refer to [view execution information](https://docs.byteplus.com/en/docs/tls/View_alarm_policy_execution_results#.5p-l55yL5omn6KGM5L-h5oGv).

To help you stay informed about the execution of alarm policies, Log Service provides the function to monitor alarm policies. When you create an alarm for a specified alarm policy, if the policy fails during execution, the system automatically triggers an alarm and sends a notification to the specified notification group.

Currently, Log Service offers a template for alarm policies that triggers when an alarm policy execution fails. This template comes pre\-configured with query and analysis statements, trigger conditions, and alarm sending intervals. You only need to add a notification group to complete the alarm policy setup. When the alarm policy encounters the following errors, the system will promptly send notifications to your designated notification group.


|Error Code |Description |
|---|---|
|QueryError |Query execution exception. Check the query and log topic index configuration. |
|AlarmConfigNotFound |Alarm policy configuration is missing. Check if the alarm policy and monitoring object configurations are correct. |
|QuerySyntaxError |The query for the monitored object contains syntax errors. Verify the query is correct. |
|QueryResultParseError |Failed to parse analysis result format. |
|SendFail |Notification sending failed. |
|InternalServerError |Internal server error. |
|PartialSent |Partial alarms sent successfully. |
|AlarmConditionSyntaxError |Syntax error in alarm expression. |
|AlarmConditionEvaluateError |Error calculating alarm expression. |
|AlarmConditionValueTypeError |Alarm expression result type error. |


<span id="247b3eb6"></span>
## Prerequisites

The alarm policy has been created.

The notification group has been created. 

<span id="93fa0586"></span>
## Procedure


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, find the alarm policy with execution failure, then select  **···**  \> **Create execution failure alarm** in its **Actions** column.

5. On the **Create alarm policy** page, select the **notification group**. Keep other parameters at their default settings, then click **Create**.
