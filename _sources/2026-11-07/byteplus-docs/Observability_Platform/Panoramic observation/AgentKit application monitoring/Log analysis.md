---
title: "Log analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Log_analysis"
---

AI application monitoring provides a dedicated log analysis page for runtimes created in AgentKit. This page is used to record logs generated throughout the runtime lifecycle, facilitating fault diagnosis and behavior tracing. This topic provides a detailed description of how to view log information.

<span id="exlzdDz5"></span>
## Prerequisites

Resources such as a runtime have been created on the AgentKit platform, and observability has been enabled. Learn more about [creating a runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="gIglwRxV"></span>
## Limits

The log analysis page only displays log data generated during the runtime lifecycle and does not include runtime build logs. To view runtime build logs, navigate to the **Log analysis** page on the details page of the target runtime. For more detailed information, refer to [Runtime monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/Runtime_overview).

<span id="DxxQu14Q"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Log analysis**, and select a time period. You can then view all log data and related details within the specified time period, such as time, host, log level, TraceID, and content.

* **Log ** **aggregation**: A bar chart of log counts across different time periods is displayed based on the specified aggregation time. After the **Auto refresh** option is checked, the system automatically refreshes the log aggregation chart and log list based on the specified refresh interval. In addition, full\-text search is available to support returning criteria\-matching results from the log aggregation chart and log list.

* **Log list**: Token\-based search and log data filtering by runtime name, log level, and trace ID are supported. To view host\-related metrics, such as metrics related to CPU, load, and memory, click the **host name** of the target log to navigate to the host monitoring details page. For the complete log information on a single trace throughout the entire trace path, click **Trace ID** of the target log. To view the full log content, click **Details** in the Actions column on the right side of the target log. To export a log in `txt` format to local, click **Export** in the Actions column on the right side of the target log.
