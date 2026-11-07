---
title: "Intelligent Analysis Agent Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Analysis_Agent_Overview"
---

**The Intelligent Analysis Agent (hereinafter referred to as the Analysis Agent or intelligent agent) is an expert advisor based on AI deep reasoning and big data analysis**, integrating the deep reasoning capabilities of large models and balancing flexible intelligent data querying with in\-depth research reports. This article provides a brief introduction to the functional overview, applicable scenarios, and general operation process of the Intelligent Analysis Agent.

<span id="68c0a274"></span>
# Functional overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b6f62784d8441289e7f91096900fe72~tplv-goo7wpa0wc-image.image) </span>

<span id="02fdc246"></span>
### Intelligent analysis


|Intelligent query Agent |In\-depth research Agent |
|---|---|
|* As a flexibly configurable intelligent query tool, it supports querying multiple datasets, leverages semantic model parsing and business knowledge, and can accurately understand user requirements.<br><br>* Provides question recommendation and bookmarking, personalized notifications, supports multi\-turn interactive querying and attribution analysis, and meets diverse data query needs through simple conversations. |* An expert advisor for advanced AI reasoning and big data analysis, based on data queries as the foundation for interaction, integrating the deep thinking capabilities of large models.<br><br>* Automatically parses natural language requirements, builds a complete analysis framework, generates SQL and Python code to gain insights from data, outputs in\-depth research reports, assists enterprises in efficient decision\-making, and drives the intelligent transformation from raw data to business insights. |


<span id="0151e956"></span>
### Model integration

Model integration refers to the capability of the Intelligent Analysis Agent to adapt to large language models, including integration with Volcano Ark's cloud\-based models and private/local models in customer environments.

The currently supported models, along with detailed descriptions of application scenarios and deployment resource requirements, are as follows.


|Model types ||Supported model names |Supported environments |Application scenarios and deployment resource requirements |
|---|---|---|---|---|
|Cloud\-based models ||The intelligent analysis Agent provides a finely tuned combination of multiple models (best performance). |* SaaS<br><br>* Private deployment |* Can be used for vectorization, inference, and other end\-to\-end scenarios.<br><br>* Direct use in SaaS environments does not involve model deployment; for deployment in private environments, BytePlus technical support personnel will handle deployment. Resource requirements for deployment:<br><br>   * GPU: NVIDIA T4 or NVIDIA cards with more than 16 GB of memory<br><br>   * Machine hardware brand, operating system, and resource requirements for private product deployment are the same. |
|Local models |Inference models |Use intelligent query Agent and in\-depth research Agent:<br><br><br>* DeepSeek\-V3.1 (latest version)<br><br>* DeepSeek\-V3 (the latest version) |* Private deployment |* Used for code generation, inference, and other primary workflow scenarios, requiring strong capabilities to complete complex tasks.<br><br>* Model requirements: Support function calls, enable stateless mode, and support 128k context.<br><br>* When deploying in a private environment, deployment is performed by the customer. Recommended resources:<br><br>   * DeepSeek\-V3: H20 \* 8 or NVIDIA cards with equivalent memory configuration.<br><br>   * Qwen3\-235B: H20 \* 4 or NVIDIA cards with equivalent memory configuration. |
|||For using only the intelligent query feature:<br><br><br>* DeepSeek\-V3.1 (latest version)<br><br>* DeepSeek\-V3 (latest version)<br><br>* Qwen\-235b (latest version) |* Private deployment ||
||Vectorization model |Customer self\-deployed model:<br><br><br>* BGE\-M3 |* Private deployment |* Used for vectorization<br><br>* When deploying in a private environment, deployment is performed by the customer. Recommended resources:<br><br>   * GPU: NVIDIA T4 or NVIDIA cards with more than 16GB memory<br><br>   * After deployment is completed, provide the URL of the deployed instance to BytePlus deployment personnel |
|||Finely tuned models provided by the intelligent analysis agent<br><br>(Customer provides deployment resources, BytePlus provides the model and performs deployment) |* Private deployment |* Used for vectorization<br><br>* When deploying in a private environment, deployment is performed by BytePlus technical support personnel. Resource requirements for deployment:<br><br>   * GPU: NVIDIA T4 or NVIDIA cards with more than 16GB memory<br><br>   * The machine hardware brand, operating system, and resources are the same as those used for private product deployment |


<span id="f40be45d"></span>
### Data preparation


* The Intelligent Analysis Agent platform can connect to external data sources, offline data, public data, and data from the BytePlus data product matrix, allowing data from these sources to be added to the Agent platform for data processing and integration, enabling intelligent data querying.

* The Intelligent Analysis Agent platform is equipped with ByteHouse, a proprietary high\-speed engine, as a query acceleration engine, significantly improving data query and write speeds and delivering an excellent user experience with second\-level queries for tens of billions of records.

* The Intelligent Analysis Agent platform also supports data processing, enabling data transformation through visual modeling. This prepares data for subsequent consumption, including data cleansing, transformation, integration, and pre\-computation, while also facilitating dataset management and maintenance.


<span id="e5195afd"></span>
### Configuration management

The Intelligent Analysis Agent provides a comprehensive set of configuration tools to optimize intelligent data querying, covering semantic models, enterprise knowledge engine configuration, recall logic customization, prompt intervention, recommended question/indicator summary management and operations, helping data querying tools integrate into business scenarios and become a professional assistant for business data queries.

<span id="87bb13c3"></span>
### Open integration

The Intelligent Analysis Agent supports integration with Feishu bots, supports embedding into customer application systems via H5, supports secondary open integration through OpenAPI, and supports embedding with BytePlus's HiAgent product to enable collaborative applications.

<span id="02a242a1"></span>
# Applicable scenarios


|Data integration and efficient analysis effectively drive e\-commerce GMV growth |Data insights drive business strategies, implementation, and forward\-looking decision\-making |Qualitative insights and quantitative analysis jointly empower intelligent incubation of new products |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddde5d0ac6e44f659bda3f2f23ca4778~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7587321c7f954ec98a9f77ab43cde382~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaf2dd51168041248663328fdd1bf213~tplv-goo7wpa0wc-image.image) </span> |


<span id="f4606ae9"></span>
# Caution and limitations

<span id="54552b6a"></span>
## Supported regions

The currently supported regions are:


* North China 2 (Beijing), RegionID is cn\-beijing

* East China 2 (Shanghai), RegionID is cn\-shanghai


<span id="93082850"></span>
## Intelligent query limitations

To achieve better intelligent query results and experience, ensure that your configuration and usage meet the following requirements.


|Sub\-items |Detailed description of restriction requirements |
|---|---|
|Number of datasets |The number of datasets associated and bound to a single agent must not exceed 5. |
|Total number of fields |The total number of fields in all datasets associated and bound to a single agent must not exceed 300. |
|General intelligent query |* A single agent supports only one scenario. Do not mix multiple business scenarios involving data queries and in\-depth research within a single agent. Having too many business scenarios usually results in numerous, scattered business datasets, leading to poor data query and analysis outcomes.<br><br>* Indicators that cannot be processed through ETL are not supported during intelligent query; it is also recommended to process ETL\-compatible indicators in advance.<br><br>* When using the intelligent analysis Agent to ask questions, do not include multiple intents in a single interaction. That is, each question should query only one data point.<br><br>   **Incorrect example**: `Which are the top 10 products with the highest profit in 2024?` `What are the year-over-year and month-over-month changes in profit and sales revenue for these products, respectively?` `Which product has the largest year-over-year increase?` — In this example, multiple sub\-intents are included in a single interaction. |


<span id="a090e53e"></span>
## In\-depth analysis limitations

To achieve better in\-depth analysis results and experience, ensure that your configuration and usage meet the following requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using deep analysis, data query capabilities are usually involved, so the limitations described in the above "intelligent query restrictions" section should also be considered.</div>



|Sub\-items |Detailed description of restriction requirements |
|---|---|
|Analysis template character count |The character count of an analysis template must not exceed 2,000. |


<span id="a7e43a72"></span>
## Usage recommendations and practical references


* When using the Intelligent Analysis Agent, you can review the chart types currently supported by intelligent analysis and refer to the usage practices for each chart. For details, see [Best Practices: Supported Chart Types and Usage Practices](https://docs.byteplus.com/docs/dataagent/Best_Practices_Supported_Chart_Types_and_Usage_Practices).

* To achieve better usage results (query accuracy), you can review the current recommendations and practices for intelligent query prompts. For details, see [Best Practices: Recommendations and Examples for Intelligent Data Query Questions](https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions).


<span id="33638202"></span>
# General operation process

<span id="2d52ec15"></span>
## Purchase and activate the Intelligent Analysis Agent

Starting from May 30, 2025, new customers can purchase the Intelligent Analysis Agent independently or combine it with DataWind as needed. Existing DataWind customers can quickly upgrade by adding the Intelligent Analysis Agent module. For specific product/service billing, see [Billing for BytePlus DataAgent Products and Services](https://docs.byteplus.com/docs/dataagent/Billing_for_BytePlus_DataAgent_Products_and_Services).

<span id="79d24965"></span>
## Create projects and authorize

Users can create projects based on business scenarios and set data access and functional operation permissions for different users or user groups according to internal personnel responsibilities and data security requirements. For details, see [Project Information](https://docs.byteplus.com/docs/dataagent/Project_Information) and [User Management](https://docs.byteplus.com/docs/dataagent/User_Management).

<span id="bb7e7b19"></span>
## Data access and processing

Through the data connection feature, the Intelligent Analysis Agent can connect to external data sources, offline data, public data, and data from the BytePlus data product matrix, and supports data processing through visual modeling. For details, see [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview).

<span id="9d0eaace"></span>
## Create and configure the Intelligent Analysis Agent

Configure semantic models, business knowledge, recommended questions, fuzzy question decomposition, metric summaries, prompts, and more to ensure the intelligent analysis Agent aligns with business requirements, accurately understands user questions, and provides effective analysis. For details, please refer to [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures).

<span id="d5ecd9dc"></span>
## Use the intelligent analysis Agent

Users initiate data queries or analysis requests in natural language. The intelligent analysis Agent receives instructions, parses and processes them, provides query results or in\-depth analysis reports, and supports multi\-turn interactions to refine the analysis. For details, please refer to [Intelligent Query Agent](https://docs.byteplus.com/docs/dataagent/Intelligent_Query_Agent) and [Deep Research Agent](https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent).
