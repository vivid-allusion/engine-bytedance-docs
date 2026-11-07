---
title: "View configuration information"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/View_configuration_information"
---

After creating an Agentic Search scene, you can view its configuration information and modify related settings according to business needs. This topic describes explains how to view the configuration information of an Agentic Search scene.

<span id="NK47nJdg"></span>
## Prerequisites

The Agentic Search scene has been created and initialized. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario) and [Initialize an Agentic Search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario).

<span id="qg9pjqDy"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, choose **My Scenes**, then click the target Agentic Search scene.

4. At the top of the page, click the **Configuration** tab to view the **Basic information**, **Inference service**, **Network configuration**, and **Access information** of the Agentic Search scenario.

   
   |**Category** |**Details** |
   |---|---|
   |Basic information |Includes the ID, name, description, creation time, updated at, and replicas of the Agentic Search scenario. You can click the edit icon next to the replicas to modify the replica count.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supports setting 2 to 50 replicas.</div><br> |
   |Inference service |Includes the models and inference services used by the Agentic Search scenario. You can click **Edit** to modify the model, inference service, and API Key. For details, see [Initialize an Agentic Search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario). |
   |Network configuration |Includes the private network, availability zone, and subnet where the Agentic Search scenario is located. |
   |Trace configuration |Includes the status of the Trace function and the Cloud Search instance for reporting observability data (if the Trace function is enabled). You can click **Edit**, then turn the Trace function on or off, or change the Cloud Search instance in the **Edit Trace configuration** dialog.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The Trace configuration currently has a whitelist feature enabled. To use it, please <a href="https://console.byteplus.com/workorder/create/?step=1">submit a ticket</a> to apply.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To enable tracing, complete the following steps in Cloud Search first:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Create an OpenSearch 3.3 instance. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/creating-instance">Create an instance</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Turn on managed OTLP function. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Enable_managed_OTLP">Enable managed OTLP</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Enable private network access point for managed OTLP and set the virtual private cloud to the one used by the current Agentic Search scenario. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/Enable_managed_OTLP#mTmBnv9S">Enable the private network endpoint</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After enabling tracing, you can view observability data in OpenSearch Dashboards. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Query_Agent_Traces_in_Dashboards">Query Agent Traces through Dashboards</a>.</div><br> |
   |Access information |Includes the private network access status, public network access status, private network access address, and public access address of the Agentic Search scenario. After turning on private network access or public network access, you can view the corresponding access address. |
