---
title: "Observability"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Observability-"
---

AgentKit features seamless integration with AI application performance monitoring. For resources deployed on AgentKit, simply enabling application monitoring will automatically ingest their monitoring data. After the monitoring integration is completed, the system supports automatic trace collection, automatic metric generation, as well as call chain and log search capabilities.

<span id="gr3U5g9c"></span>
## Resources supporting observability


* Agent Runtime

* Memory

* Knowledge Base


<span id="4tWIz2A3"></span>
## Prerequisites

To view the monitoring data of the items listed in the following table, you need to first enable the observability service for the corresponding resources. The methods for enabling the observability service for each resource are as follows:


|Monitoring |How to enable |
|---|---|
|Runtime overview |* Create an agent runtime and enable the observability service. The methods for creating an agent runtime include:<br><br>   * [Deploying agent runtimes with one click by using scenario-based templates](https://docs.byteplus.com/en/docs/agentkit/Using_scenario-based_templates)<br><br>   * [Creating runtime in console](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>   * [Creating runtimes via CLI tool](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)<br><br>* After an agent runtime is created, enable the observability service. For more information, see [Enabling/Disabling observability service](https://docs.byteplus.com/en/docs/agentkit/Enabling_or_Disabling_observability_service). |
|Session analysis ||
|Trace analysis ||
|Model monitoring ||
|Log analysis ||
|Alert template |The first time you use server\-side monitoring, you need to activate it. For details, refer to [Activate server-side monitoring](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring). |


<span id="pZ1sx5bi"></span>
## View observability data


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the top menu bar, select the project and region of Observability.

3. In the left\-side navigation pane, select "Observability" to view the following information:

   
   |Monitoring item |Description |
   |---|---|
   |[Runtime overview](https://docs.byteplus.com/en/docs/Observability_Platform/Runtime_overview) |AI application performance monitoring delivers comprehensive observability capabilities for agents deployed on AgentKit, including automatic trace collection, metric auto\-generation, call chain analysis, and log search. These capabilities enable real\-time visibility into the performance and reliability of the agents. |
   |[Memory analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Memory_analysis) |AI application performance monitoring enables real\-time monitoring of the resource performance, accuracy, retrieval effectiveness, and reliability of the monitored memory in AgentKit, based on key metrics, traces, logs, and specified time ranges. |
   |[Knowledge base analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Knowledge_base_analysis) |AI application monitoring supports tracking knowledge verification metrics including API calls, average latency, and total error rate. These metrics can be leveraged for resource optimization, system stability assurance, and user experience enhancement, while providing a data\-driven foundation for business decision\-making. |
   |[Session analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Session_analysis) |AI application performance monitoring provides a dedicated session analysis page for AgentKit and its deployed agents. This page is used to track the complete interaction process between a single user and an agent within a specific time period, facilitating problem identification. |
   |[Trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis) |AI application monitoring provides a dedicated trace analysis page for AgentKit and its deployed agents. This page is used to track the full call chain of agent applications, facilitating query of call relationships and analysis of chain\-related issues. |
   |[Model monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/Model_monitoring) |AI application monitoring features seamless integration with AgentKit. It delivers out\-of\-the\-box observability capabilities for agents deployed on AgentKit, including automatic trace collection, metric auto\-generation, call chain search, and log search. |
   |[Log analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Log_analysis) |AI application monitoring provides a dedicated log analysis page for agent runtimes created in AgentKit. This page is used to record logs generated throughout the agent runtime lifecycle, facilitating fault diagnosis and behavior tracing. |
   |[Sandbox templates analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Tool_analysis) |AI application monitoring provides detailed metrics for monitoring sandbox templates, including the number of sandbox template calls, error rate, and average response time. It helps detect system instability and improve user experience. |
   |[Insight dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Insight_dashboards) |AI application monitoring provides an independent insight dashboard for AgentKit. The dashboard provides an overview of AgentKit and agent\-related statistics and trend analytics, facilitating health checks, performance optimization, and exception detection. |
   |[Alert template](https://docs.byteplus.com/en/docs/Observability_Platform/Alert_management) |AI application performance monitoring provides alerting and monitoring capabilities for agent runtime, tools, and other resources in AgentKit. It not only supports the creation of custom alert tasks but also enables quick creation of alert tasks using system\-provided preset alert templates. |
