---
title: "Prompt Configuration Practices"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Prompt_Configuration_Practices"
---

<span id="6db67e0b"></span>
# Functionality principles

A prompt is an instruction or requirement that applies globally to the intelligent agent. Prompts are added to all user queries, so they have a significant impact on the overall performance of the intelligent agent. They are typically used to define the agent's role, general response logic, and similar scenarios.

<span id="4f12f6d4"></span>
# General configuration approach


1. In the vast majority of scenarios, configuring a prompt is not necessary. Global prompt configuration for the intelligent agent may unexpectedly degrade the quality of many responses. Exercise extreme caution when adding global prompts.

2. In prompts, do not mention or refer to any table names, as the model does not know the dataset names. Mentioning table names only leads to negative optimization.

3. There is also no need to mention or use chart\-related expressions in prompts, as they will not take effect.

4. Default filter conditions should be implemented through filter configurations on the dataset at the engineering level. Do not specify such requirements in the prompt configuration.

5. For data formats, do not use prompt configuration to require the model to implement them. For formats not supported at the engineering level or in problematic cases, submit a feature request to the product and R&D team of BytePlus for resolution.


<span id="0fdffdf4"></span>
# Configuration examples

<span id="d92c4e26"></span>
## Clearly specify the logic, data scope, data units, and so on for the returned results


|Type |Prompt |
|---|---|
|Note |The current user is an administrator. Understand and address questions from the perspective of a senior manager. When handling questions related to contracts, orders, shipments, revenue recognition, or payment collection, in addition to providing the main data metrics, also provide customer information, sales department, and other information associated with the main issue based on the context, as well as other metrics related to the main indicators, such as sales volume, power, amount, and so on. |
|Note |A loss\-making Sales representative and a loss\-making contract have the same meaning and should be answered using the same logic. The response must include the contract number, sales department, Sales representative, contract gross profit, and other relevant information. |
|Note |When answering questions related to "each\*", group and aggregate according to the field name that follows "each". |
|Requirements |If the question ends with "how many people are there for different employment types", select the "Employment mode – usage of in\-service workforce" field as the dimension for the query; if the question ends with "what is the proportion of non\-frontline", select the "Employment mode – usage of non\-frontline workforce proportion" field as the dimension. |
|Requirements |For amount\-related metrics, convert yuan to units such as ten thousand yuan, hundred million yuan, depending on the data size. |
|Requirements |All metric query results must be accurate to two decimal places. |


<span id="a04f5511"></span>
## Indicate the business meaning


|Type |Prompt |
|---|---|
|Note |TOPCon, PERC, and HJT refer to technology types and are not primary financial categories. |


<span id="a14f9420"></span>
# Common issues

<span id="09c23588"></span>
## Prompt configuration not effective


|Prompt configuration example |Issue phenomenon & possible causes |Optimization approach |
|---|---|---|
|A "Note" type Prompt was configured in the intelligent agent: The name of the primary financial category is composed of "product specification", "structural features", and "technical route". |When using the intelligent agent for queries, it was found that this rule did not take effect. When querying metric data for a certain primary financial category name, the data matching was incorrect.<br><br>Possible causes:<br><br><br>* The business meaning of this Prompt rule is relatively complex.<br><br>* During recall before table selection in the intelligent agent, the Prompt rule is recalled last. Before that, more suitable datasets have already been found based on recall results from datasets and knowledge, so this Prompt rule did not take effect. |For Prompts with relatively complex rules, it is recommended to configure semantic models for each dataset field involved in the business meaning within the intelligent agent's datasets. |
