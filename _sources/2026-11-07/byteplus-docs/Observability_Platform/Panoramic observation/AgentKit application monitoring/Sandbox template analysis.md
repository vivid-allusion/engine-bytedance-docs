---
title: "Sandbox template analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Tool_analysis"
---

AI application monitoring provides detailed data monitoring for sandbox templates. This enables you to view key metrics such as call count, error rate, and average response time for sandbox templates, making it easier to monitor system stability and improve your experience. This topic describes how to view sandbox template analysis data.

<span id="NcGLECP4"></span>
## Background

Sandbox templates provide multiple runtime environments that agents need to execute tasks and support quick integration and easy invocation. For more details, see [Sandbox template types](https://docs.byteplus.com/en/docs/agentkit/Tool_type).

<span id="86xxV1JT"></span>
## Prerequisites

You have created a sandbox template in AgentKit and integrated it into your agent code. For more information, see [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools).

<span id="z6y7N2gp"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. Log in to the AgentKit console.

2. In the left navigation bar, select **AgentKit Application Observability**. In the left navigation bar, select **Observability**.

3. Click **Sandbox template analysis**. Select a time range to view sandbox template data and details during that period, such as the number of sandbox templates, call count, and error count.

   
   |Metric |Description |
   |---|---|
   |Number of sandbox templates |The total number of sandbox templates queried within the specified time range. A sandbox template list is provided where you can view all sandbox templates and basic information. |
   |Call count |The total call count of all sandbox templates within the specified time range. A call trend chart is provided to help you understand how frequently sandbox templates are used across different time periods and plan resources accordingly. |
   |Error count |The number of failed sandbox template calls within the specified time range. |
   |Error rate |The error rate of sandbox template calls during the specified time period. Error rate = error count/call count. An error rate trend chart is provided, helping you monitor system stability and improve user experience. |
   |Average response time |The average response time of sandbox template calls during the specified time period. Average response time = total response time of all sandbox template calls/total number of calls. An average response time trend chart is provided, facilitating performance evaluation and quality of service assurance. |
   

4. Click the name of the target sandbox template or click ** Monitoring details** in the Actions column on the right. You will be directed to the ** Sandbox template runtime overview** tab on the sandbox template details page to view detailed data for that specific sandbox template within the specified time range.

5. Switch to the **Trace analysis** tab to view detailed trace information associated with the current sandbox template during the specified time period. You can view the span list, performance analysis, and error propagation chain analysis related to the current sandbox template. You can filter data by span attribute, sandbox template name, trace ID, span type, interface name, and other criteria. For more details, refer to [Trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis).

6. To view the complete trace associated with the current sandbox template and the full trace logs, click the target trace ID in the span list to navigate to the single trace details page.
