---
title: "API Release History"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/API_Release_History"
---

<span id="9a63a185"></span>
# January 26, 2026


|API |Release date |Change log |Related features |
|---|---|---|---|
|Deep research |2026\-01\-26 |* Added support for the `exportConfig` parameter. Deep research reports obtained via OpenAPI now support downloading PDF files, images, and raw data.<br><br>* Added support for multiple parameters:<br><br>   * `mcpConfig`, `OpenApiMcpConfig`, `RegisteredMcpServer`, `McpTool`: Used for MCP service calls.<br><br>   * `sessionName`: Used to set the session name.<br><br>   * `enableAgentDataSet`: Sets whether to use the vertical agent dataset.<br><br>   * `enableDeepThinkingMode`: Sets whether to enable deep research mode. |[Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task) |
|General |2026\-01\-26 |The HiAgent interface is enabled by default. When users connect the intelligent analysis Agent to HiAgent, there is no need to contact the intelligent analysis Agent team for activation. |None |


<span id="40f61939"></span>
# December 5, 2025


|API |Release date |Change log |Related features |
|---|---|---|---|
|Smart Query OpenAPI<br><br>(New version) |2025\-12\-05 |Smart Query offers the new version of the OpenAPI interface. The capabilities of the new OpenAPI interface are generally aligned with those of the Smart Query UI, allowing more flexible data queries via the interface. |[Intelligent Data Query API Description and Common Parameters (new version)](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_API_Description_and_Common_Parameters_new_version) |
|Smart Query OpenAPI<br><br>(Old version) |2025\-12\-05 |The old version of the Smart Query OpenAPI interface now supports specifying the dataset for data queries in Smart Query requests via the dataset parameter (dataSetId). |[Intelligent Data Query for Lark Client](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_Lark_Client)<br><br>[Intelligent Data Query for PC](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_PC) |


<span id="d917af3d"></span>
# November 15, 2025


|API |Release date |Change log |Related features |
|---|---|---|---|
|Deep Research OpenAPI |2025\-11\-15 |The OpenAPI for executing deep research reports supports returning the content of the reasoning process. The request parameter `enableRunningStepOutput` controls whether to return detailed reasoning steps. |[Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task) |


<span id="b92bd653"></span>
# November 5, 2025


|API |Release date |Change log |Related features |
|---|---|---|---|
|Smart Query OpenAPI |2025\-11\-05 |Smart Query OpenAPI adds a request parameter to enable or disable chart analysis: `enableAnalysis`. |[Intelligent Data Query for Lark Client](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_Lark_Client)<br><br>[Intelligent Data Query for PC](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_PC) |


<span id="c303112e"></span>
# October 28, 2025


|API |Release date |Change log |Related features |
|---|---|---|---|
|Deep Research OpenAPI |2025\-10\-28 |The OpenAPI request parameters for deep research reports now support the html_id parameter, making it easier to hide unnecessary page header information when calling OpenAPI to obtain research reports. |[Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task) |


<span id="46ec30c6"></span>
# September 30, 2025


|API |Release date |Change log |Related features |
|---|---|---|---|
|Deep Research OpenAPI initial release |2025\-09\-30 |Added support for OpenAPI interfaces related to deep research functionality. |[Deep Research API Description and Common Parameters](https://docs.byteplus.com/docs/dataagent/Deep_Research_API_Description_and_Common_Parameters) |


<span id="b378d304"></span>
# June 9, 2025


|API |Release date |Change log |Related features |
|---|---|---|---|
|Initial release |2025\-06\-09 |The product was released for the first time, and some OpenAPI interfaces were made available externally. |[Intelligent Data Query API Description and Public Parameters (old version)](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_API_Description_and_Public_Parameters_old_version) |
