---
title: "LLM monitoring dashboard"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/LLM_monitoring_dashboard"
---

The AI application monitoring probe supports observability of large language model (LLM) applications. After the self\-developed Python probe is integrated with LLM applications, you can intuitively view model calls, token consumption, TTFT, and other performance metrics from both model and service perspectives. This topic provides a detailed description of how to view LLM\-related monitoring information.

<span id="2QhK4q8e"></span>
## Prerequisites

Your LLM application has been integrated with Server\-side Monitoring, and auto\-instrumentation is enabled. For specific steps, see [Python application integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications).

<span id="1FtRB4RD"></span>
## Operation Procedure

<span id="ymDDhjHE"></span>
### View LLM monitoring dashboards


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **LLM Monitoring Dashboard**.

3. Select a time range and model whose monitoring information you need to view. You can then view related monitoring information within the specified time period.


&nbsp;


|**Dashboard name** |**Description** |
|---|---|
|Total model call count |The total number of calls to the specified LLM. |
|Average duration of model calls |The average duration of calls to the specified LLM. |
|Model call error count |The number of failed calls to the specified LLM. |
|Total token consumption |The total tokens consumed (input + output) by the specified LLM. |
|Model call count |The trend chart indicating the number of calls to the specified LLM. |
|Average duration of model calls |The trend chart indicating the average duration of calls to the specified LLM. |
|Model call error |The trend chart indicating the number of failed calls to the specified LLM. |
|Token consumption |The trend chart indicating the total tokens consumed (input + output) by the specified LLM. |
|Application ranking based on model calls (TOP 5) |The list of the top 5 applications that most frequently call the specified LLM. |
|Application ranking based on the average time of model calls (TOP 5) |The list of the top 5 applications with the highest average call latency to the specified LLM. |
|Application ranking based on failed model calls (TOP 5) |The list of the top 5 applications with the highest number of failed calls to the specified LLM. |
|Application ranking (TOP 5) based on token consumption |The list of the top 5 applications that consumed the most tokens with the specified LLM. |
|Model request duration quantiles |Latency percentiles (P99, P90, P75, P50) for calls to the specified LLM. |
|TTFT quantiles |Quantiles of the average first\-packet return time for calls to the specified LLM: P99/P90/P75/P50. |
|TPOT quantiles |Duration quantiles for each token output interval following the output of the first token during LLM calls. |


<span id="8lh4e1mr"></span>
### View LLM application performance


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar. 

2. In the left navigation bar, select **Service Monitoring \> Service List**.

3. Click the name of the target AI application to go to the service details page. Select the **LLM performance** tab to view the relevant monitoring dashboards.



|**Dashboard name** |**Description** |
|---|---|
|Total model call count |The total number of LLM calls by the current application. |
|Average duration of model calls |The average duration of LLM calls by the current application. |
|Model call error count |The number of failed LLM calls made by the current application. |
|Model call count |The trend chart indicating the LLM calls by the current application. |
|Average duration of model calls |The trend chart indicating the average duration of LLM calls made by the current application. |
|Model call error |The trend chart indicating the number of failed LLM calls by the current application. |
|Ranking based on the model call count (TOP 5) |The list of the top 5 LLMs most frequently called by the current application. |
|Ranking based on the average time of model calls (TOP 5) |The list of the top 5 LLMs ranked by average call latency for the current application. |
|Ranking based on model call errors (TOP 5) |The list of the top 5 LLMs with the highest number of failed calls by the current application. |
|Model request duration quantiles |Latency percentiles (P99, P90, P75, P50) for calls to the LLM by the current application. |
|TTFT quantiles |Quantiles of the average first\-packet return time for LLM calls initiated by the current application: P99/P90/P75/P50. |
|TPOT quantiles |Duration quantiles for each token output interval following the output of the first token during LLM calls made by the current application. |


<span id="HFnAsSh6"></span>
### View token usage of the LLM application


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar. 

2. In the left navigation bar, select **Service Monitoring \> Service List**.

3. Click the name of the target AI application to go to the service details page. Then, select the **Token usage** tab to view the monitoring dashboards related to token usage of the LLM application.



|**Dashboard name** |**Description** |
|---|---|
|Total token consumption |The total token consumption for all LLM calls by the current application. |
|The token consumption per LLM call |The token consumption per call to the LLM by the current application. |
|Model ranking (TOP 5) based on token consumption |The list of the top 5 LLMs ranked by total token usage for all LLM calls for the current application. |
|Total token consumption |The trend chart indicating total token consumption for all LLM calls by the current application. |
|The token consumption per LLM call |The trend chart indicating token consumption per LLM call for the current application. |
