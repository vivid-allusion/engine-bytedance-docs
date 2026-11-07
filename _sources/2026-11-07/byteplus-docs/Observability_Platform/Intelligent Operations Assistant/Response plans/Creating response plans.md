---
title: "Creating response plans"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/create-response-plan"
---

A response plan is a condition\-triggered automated analysis workflow. After an alert is triggered, the system automatically performs a fault check based on the process defined in the Runbook. It then outputs repair recommendations for manual confirmation and as a remediation reference. This topic describes how to create a response plan.

## Background

Response plans currently support automatic responses for alert monitoring. When an alert is triggered, the response plan is executed automatically without requiring on\-call personnel to investigate each alert manually. When configuring a response plan for an alert rule, select the event source and alert rule, and associate an expert agent and a remediation Runbook. When an alert is triggered, the response starts automatically according to the plan. The system performs evidence collection and root cause analysis according to the Runbook, and then provides repair recommendations. On\-call personnel only need to confirm and make decisions at key steps.

## Prerequisites

* An alert rule has been configured for the target event source. For configuration examples, see [Creating Cloud Monitor alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_rules), [Creating cloud service event rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_cloud_service_event_rules), [Creating VMP alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rules), and [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).

* (Optional) If you use a custom expert agent to execute the response plan, create the expert agent in advance. For more information, see [Creating expert agents](https://docs.byteplus.com/en/docs/observability/Configuring_expert_agents).

## Limits

* A response plan uses the expert agent only to query alert data, analyze alert causes, and provide repair recommendations. It does not automatically execute remediation actions.

* The expert agent used for the response plan must have query permissions for the target resources and events and must have fault diagnosis skills. Otherwise, it cannot provide accurate repair recommendations.

## Procedure

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Response plan**.

3. Click **Create Response Plan** in the upper\-right corner. Configure the relevant parameters for the response plan and click **Confirm**.

   |Parameter |Description |
   |---|---|
   |Plan Name |Enter a name for the response plan. |
   |Event Source |The data source that triggers the response. The following sources are currently supported: Cloud Monitor, cloud product events, VMP, and Server\-side Monitoring. |
   |Alert rules |The trigger condition for the response plan. Alert rules are currently supported as trigger conditions. When observability data meets the condition configured in the alert rule, the alert is triggered, and the response plan is executed automatically at the same time. The system collects basic alert information such as the alert rule, alert trigger time, and investigation target, performs root cause analysis, and provides repair recommendations. |
   |Trigger Frequency |The execution frequency when the response plan is triggered multiple times. The default is 1 hour, and the frequency cannot be set lower than 1 hour. For example, if an alert is triggered multiple times within 1 hour, the response plan is triggered only on the first alert.<br><br>> **tip**<br><br><br>> A response plan only provides alert\-cause analysis and repair recommendations. It does not automatically resolve alerts. We recommend that you configure a reasonable trigger frequency based on the time required for manual remediation. Otherwise, the same alert may trigger the response plan multiple times.<br> |
   |Expert agent |The expert agent used to query data, analyze causes, and summarize conclusions during the execution of the response plan. The VeOps Agent is used by default. You can also select an appropriate expert agent based on your scenario.<br><br>We recommend that the expert agent used to execute the response plan meet the following requirements. Otherwise, it cannot provide accurate repair recommendations:<br><br><br>* It has query permissions for information related to the target resources and events.<br><br>* It has skills specifically designed for investigating alert events and handling faults. |
   |Handling Runbook |The runbook for handling alerts after the response plan is triggered. The runbook must include fault diagnosis methods, fault verification methods, and remediation recommendation output requirements.<br><br>You can manually write the runbook in the input box based on your experience, or click "**AI generated instruction**" to automatically generate a runbook based on a custom prompt and alert policy. |

## What to do next

After a response plan is triggered, the system collects basic alert information such as the alert rule, alert trigger time, and investigation target. It then performs root cause analysis and provides repair recommendations. Follow the steps below to go to the execution session, view the repair recommendations, and perform manual confirmation and remediation.

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Response plan**.

3. Click the target response plan to go to the task details page.

4. In the execution history, click "**Go to Session**" in the "Actions" column of a target record. The session shows the execution conclusion, repair recommendations, and other details.
