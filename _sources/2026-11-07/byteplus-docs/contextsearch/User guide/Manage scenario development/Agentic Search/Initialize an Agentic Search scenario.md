---
title: "Initialize an Agentic Search scenario"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario"
---

An Agentic Search scenario can autonomously plan and execute complex search tasks, dynamically breaking down tasks based on your questions, invoking retrieval tools, and integrating search results to generate more accurate and comprehensive answers. This topic describes how to initialize the Agentic Search scenario through basic configuration.

<span id="rnWkIlfW"></span>
## Prerequisites

An Agentic Search scenario is created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

<span id="aGMFrCWi"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My scenarios** in the left navigation bar, then click the target Agentic Search scenario.

4. In the **Welcome to Agentic Search** dialog, configure the following parameters, then click **Try Now**.

   
   |Parameter |Description |
   |---|---|
   |Select model/inference service |Select the model and inference service used by the scenario from the dropdown list. Currently supporting **Public model** and **Ark model**.<br><br>If you need a new inference service, click **Create an inference service**. For detailed steps to create a common model, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service).  |
   |API Key |Select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |
   |Private network |To ensure smooth intranet visit, select the Virtual Private Cloud in the region where your existing cloud services are located. Subnets in different availability zones within the same Virtual Private Cloud are interconnected.<br><br>If a new Virtual Private Cloud is needed, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Replicas |Set the number of replicas for the Agentic Search scenario. You can set between 2 and 50 replicas. |
   |Enable Trace (optional) |Select whether to enable tracing. When enabled, the scenario can report observability data through the Cloud Search OpenSearch instance, helping you analyze the execution chain and runtime status.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Trace configuration is currently a whitelist feature; to use it, please <a href="https://console.byteplus.com/workorder/create/?step=1">submit a ticket</a> to apply.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To enable tracing, complete the following steps in Cloud Search first:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Create an OpenSearch 3.3 instance. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/creating-instance">Create an instance</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Turn on managed OTLP function. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Enable_managed_OTLP">Enable managed OTLP</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Enable private network access point for managed OTLP and set the virtual private cloud to the one used by the current Agentic Search scenario. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/Enable_managed_OTLP#mTmBnv9S">Enable the private network endpoint</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After enabling tracing, you can view observability data in OpenSearch Dashboards. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Query_Agent_Traces_in_Dashboards">querying Agent Traces through Dashboards</a>.</div><br> |
   |Cloud Search Instance |Select the OpenSearch instance to report observability data from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only visible when the <strong>Enable Trace</strong> toggle is turned on.</div><br> |
