---
title: "Model monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Model_monitoring"
---

AI application monitoring is seamlessly integrated with AgentKit, providing automatic trace information collection, automatic metric generation for deployed agents, and comprehensive observability support, such as trace search and log search. This topic provides a detailed description of how to view monitoring information related to large models.

<span id="yF8eIRVS"></span>
## Background

AI application monitoring provides deployed probes for applications in AgentKit. When an AI agent calls model services, this feature enables you to monitor model calls, token consumption, TTFT, and other performance metrics from both model and service perspectives.

<span id="OC75Dxk3"></span>
## Prerequisites

Large models have been called when the AI agent executes tasks such as text generation and question answering.

<span id="F7bBEdD2"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Model monitoring**, and select the time range and model whose monitoring information you want to view. You can then view the model's monitoring information within the specified time period.



|**Dashboard name** |**Descriptions** |
|---|---|
|Total model call count |Displays the total number of calls to the specified model. |
|Average duration of model calls |Average duration of calls to the specified model. |
|Model call error count |Displays the number of failed calls to the specified model. |
|Total token consumption |Displays the total token consumption (input + output) of the specified model. |
|Model call count |Displays the trend of the number of calls to the specified model. |
|Average duration of model calls |Displays the trend of average duration of calls to the specified model. |
|Model call error |Displays the trend of the number of failed calls to the specified model. |
|Token consumption |Displays the total token consumption (input + output) trend of the specified model. |
|Runtime ranking (TOP 5) based on model calling |Displays the top 5 runtimes ranked by call count for the specified model. |
|Runtime ranking (TOP 5) based on average duration of model calls |Displays the top 5 runtimes ranked by average duration of calls to the specified model. |
|Runtime ranking (TOP 5) based on model call errors |Displays the top 5 runtimes ranked by error count of calls to the specified model. |
|Runtime ranking (TOP 5) based on token consumption |Displays the top 5 runtimes ranked by token consumption for calls to the specified model. |
|Model request duration quantiles |Displays duration quantiles for calls to the specified model, including P99/P90/P75/P50. |
|TTFT quantiles |Displays average duration quantiles of the time for receiving the first packet of data returned by calls to the specified model, including P99/P90/P75/P50. |
|TPOT quantiles |Duration quantiles for each token output interval after the first Token is output during a model call. |
