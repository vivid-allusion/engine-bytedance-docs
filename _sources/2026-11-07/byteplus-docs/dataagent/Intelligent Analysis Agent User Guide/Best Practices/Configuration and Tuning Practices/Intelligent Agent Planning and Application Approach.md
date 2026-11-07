---
title: "Intelligent Agent Planning and Application Approach"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Agent_Planning_and_Application_Approach"
---

Before using the Intelligent Analysis Agent, it is recommended to first review and plan the main business scenarios in conjunction with your business analysis context, prepare the intelligent agent application plan in advance, and understand the optimization approach for intelligent agent applications to facilitate better use of the Intelligent Analysis Agent in the future.

<span id="3fd027b8"></span>
# Business review and planning

Before creating and using the Intelligent Analysis Agent, you need to research and review the main business scenarios where intelligent agents will be used in the future. It is recommended to include:


* Which business scenarios require the use of intelligent agents

* Which roles will use intelligent agents for query analysis

* What are the main issues that each user role may encounter


The following is a simple example for your reference. You can use this example for business review and planning.


|Sub\-items |Organize details |Key points for organizing ideas |
|---|---|---|
|Business scenario description |The agent for the *sales management team* is mainly used in the following scenario: *The management hopes to quickly understand the overall sales operations, shipments, revenue, and gross profit, and to analyze the key factors affecting revenue and gross profit*. |Clearly define business scenarios. Business scenarios with significant differences should be separated. In principle, it is recommended to use one agent to address the issues of a single business scenario. |
|User role 1: *Company executive* |Main questions include:<br><br><br>* *What was the sales revenue for the past month?* <br><br>* *What is the sales gross profit for this year?* <br><br>* *Which region has the fastest sales revenue growth?* <br><br>* *Which product model (board type) has the highest sales revenue?* <br><br>* *Which product has the highest gross profit?* <br><br>* *Who are the top ten customers by sales revenue?*  |* Sort out typical user roles and potential questions.<br><br>* Subsequent planning for the agent's dataset, knowledge, and other important aspects of configuration and optimization approaches should be based on this analysis. |
|User role 2: *Sales manager* |Main questions include:<br><br><br>* *Which type of customer (A/B/C, domestic/overseas, state\-owned/central SOE/non\-state\-owned, centralized/distributed) has the highest sales revenue?* <br><br>* *Which type of customer has the fastest sales revenue growth?* <br><br>* *Which sales representative has the highest opportunity conversion rate?* <br><br>* *Which sales representative has the highest sales gross profit?* <br><br>* *Which region (domestic/overseas, South China/Central China/North China/East China) generates the most sales revenue?* <br><br>* *Which customer has the highest accounts receivable?* <br><br>* *Which customer has the longest overdue period?*  ||
|User role 3: xxx |Main questions include:<br><br><br>* *xxxx*<br><br>*  *……*  ||


<span id="c22e2100"></span>
# Model and resource planning

<span id="8f565ef3"></span>
#### Resource consumption:

The following provides model resource consumption data evaluated based on empirical values (sample statistics), which you can use to assess model resource planning.


* Single query: generates 12 model calls (4 basic, 2 simple analyses, 6 parallel processes), with each query consuming an average input of 20,000 tokens.

* Single in\-depth research report: generates 30–40 model calls, with a total consumption of approximately 400,000–600,000 tokens.


<span id="7bf0cc0a"></span>
#### Model requirements:


|Model types ||Supported model names |Supported environments |Application scenarios and deployment resource requirements |
|---|---|---|---|---|
|Cloud\-based models ||The intelligent analysis agent provides a fine\-tuned multi\-model combination (best performance) |* SaaS<br><br>* On\-premises |* Can be used for full\-link scenarios such as vectorization and inference.<br><br>* SaaS environments can be used directly without model deployment; for on\-premises environments, deployment is performed by BytePlus technical support personnel. Deployment resource requirements:<br><br>   * GPU: NVIDIA T4 or NVIDIA cards with more than 16 GB of VRAM<br><br>   * Machine hardware brand and operating system are the same as those required for on\-premises product deployment |
|Local models |Inference models |For use with Smart Query and Deep Research:<br><br><br>* DeepSeek\-V3.1 (latest version)<br><br>* DeepSeek\-V3 (latest version) |* Private deployment |* Used for primary scenarios such as code generation and inference, requiring strong capabilities to complete complex tasks.<br><br>* Model requirements: Support function calls, enable non\-thinking mode, and support a context length of 128k.<br><br>* When deploying in a private environment, deployment is performed by the customer. Recommended resources:<br><br>   * DeepSeek\-V3: H20 \* 8 or NVIDIA card with equivalent memory configuration.<br><br>   * Qwen3\-235B: H20 \* 4 or NVIDIA card with equivalent memory configuration. |
|||Only use the intelligent query function:<br><br><br>* DeepSeek\-V3.1 (latest version)<br><br>* DeepSeek\-V3 (latest version)<br><br>* Qwen\-235b (latest version) |* Private deployment ||
||Vectorization model |Customer self\-deployed model:<br><br><br>* BGE\-M3 |* Private deployment |* Used for vectorization<br><br>* When deploying in a private environment, deployment is performed by the customer. Recommended resources:<br><br>   * GPU: NVIDIA T4 or NVIDIA card with more than 16 GB of memory<br><br>   * After deployment is complete, provide the deployed URL to BytePlus deployment personnel |
|||Fine\-tuned model provided by the Intelligent Analysis Agent<br><br>(Customer provides deployment resources, BytePlus provides the model and performs deployment) |* Private deployment |* Used for vectorization<br><br>* When deploying in a private environment, deployment is performed by BytePlus technical support personnel. Resource requirements for deployment:<br><br>   * GPU: NVIDIA T4 or NVIDIA card with more than 16 GB of memory<br><br>   * The machine hardware brand and operating system must be the same as those used for private product deployment resources |


<span id="b157cbc9"></span>
# Configuration and optimization approach

<span id="291adad3"></span>
## Single agent principle


* Each intelligent agent supports only one single scenario. Do not combine multiple business scenarios involving both data queries and in\-depth research within a single intelligent agent. Usually, having too many business scenarios leads to numerous and scattered associated business datasets, resulting in poor data query and analysis performance.


<span id="4dbcb82e"></span>
## Dataset quantity & no cross\-table principle


* The number of datasets associated with a single intelligent agent must not exceed 5; the total number of fields across all datasets associated with a single intelligent agent must not exceed 300.

* The dataset fields and dimension values of the agent must be governed to reduce or eliminate ambiguity and conflicts (for example, fields with the same name but different meanings).

* When different roles use the agent, the main issue is that, in principle, cross\-table queries should be avoided to prevent data quality problems caused by such queries.

* Whenever possible, perform data ETL in advance to avoid real\-time multi\-table join calculations; if unavoidable, it is recommended that the number of rows in datasets involved in multi\-table joins does not exceed 10,000.


<span id="7880119b"></span>
## Single intent principle


* When asking questions using the intelligent analysis Agent, do not include multiple intents in a single interaction. That is, each question should address only one intent.

   **Incorrect example**: `Which are the top 10 products with the highest profit in 2024?` `What are the year-over-year and month-over-month changes in profit and sales for each of these products, respectively?` `Which product has the largest year-over-year increase?` — In this example, multiple sub\-intents are included in a single question interaction.


<span id="6e6734af"></span>
## Optimization priority

When optimizing the agent, the recommended optimization priority is: dataset quality (dataset governance) \> dataset\-semantic model definition \> dataset\-knowledge base configuration. After configuring these aspects, making the question descriptions as clear as possible can further improve the quality of the results.

In other words, prioritize optimizing the dataset quality involved in the business scenario, then optimize the agent's knowledge configuration, and finally optimize based on the question configuration or description.


* [Best Practices: Data ETL Processing Guidelines](https://docs.byteplus.com/docs/dataagent/Best_Practices_Data_ETL_Processing_Guidelines).

* [Best Practices: Recommendations and Examples for Intelligent Data Query Questions](https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions).

* [Dataset Configuration Practices](https://docs.byteplus.com/docs/dataagent/Dataset_Configuration_Practices).
