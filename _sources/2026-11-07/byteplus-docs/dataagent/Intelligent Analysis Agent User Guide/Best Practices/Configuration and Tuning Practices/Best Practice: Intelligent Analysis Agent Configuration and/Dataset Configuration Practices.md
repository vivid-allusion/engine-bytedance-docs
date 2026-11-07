---
title: "Dataset Configuration Practices"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_Configuration_Practices"
---

The dataset of the intelligent agent serves as the data source for the Intelligent Analysis Agent when performing data queries. The data quality and related configuration of the dataset directly affect the data query results of the intelligent agent. Once you have ensured the data quality of the intelligent agent's dataset through data cleansing and other operations, optimizing the dataset configuration becomes crucial for influencing the data query results. This article introduces recommended approaches and practical scenarios for data configuration.

<span id="7c624aef"></span>
# Background information


* When optimizing the configuration of a dataset, you need to consider the application scenarios of the intelligent agent and have a certain understanding of typical questions and frequently asked business metrics. Configure the dataset based on these application scenarios.

* The data quality of the dataset itself has the greatest impact on the effectiveness of the intelligent agent's application. Therefore, when the query results do not meet expectations, you should first check whether the data quality of the dataset itself can be optimized, and whether it needs to be processed using ETL methods. For example, frequently asked or easily misunderstood business metrics should be handled through ETL first. For related practical references, see [Best Practices: Data ETL Processing Guidelines](https://docs.byteplus.com/docs/dataagent/Best_Practices_Data_ETL_Processing_Guidelines).


<span id="c436fe18"></span>
# Dataset\-semantic model configuration practices

<span id="294f87d5"></span>
## General configuration approach

It is recommended that you first clarify the current status of the datasets required by the intelligent agent and the fields in each dataset, including synonyms that may be involved in business query scenarios for each field. Then, configure based on the results of this clarification. The semantic model configuration for an agent consists of two main parts: the semantic configuration for the entire dataset and the semantic configuration for each field within the dataset.


* Semantic configuration for the entire dataset: An agent typically contains multiple datasets. When the agent selects a table, it will prioritize matching the semantic model results of the dataset (name, description, features). It is recommended to carefully review the user's question set to identify features that can significantly distinguish between datasets, so that for most user queries, datasets can be differentiated by identifying features.

* Semantic configuration for each field within the dataset:

   * It is recommended to enable only the necessary fields. If there are multiple date fields with identical values, only one needs to be enabled, with priority given to the partition field.

   * For [field name synonyms], if there are multiple expressions for a field name in the user's question set, add these expressions here.

      Caution: When adding, be sure to strictly follow the expressions used in the question set. More is not always better. As long as the question set is satisfied, the fewer, the better.


<span id="dee791f9"></span>
## Planning and configuration examples


|Dataset name |Basic information of the semantic model |Required fields |Field synonyms |
|---|---|---|---|
|Contract detail execution summary_CK |Statistics on customer contract execution, including information such as sales organization, sales department, product, and more.<br><br>Feature information: technology type |Customer name |Customer, customer company, buyer, user, end user |
|||Sales organization name |Sales company, subsidiary, marketing company |
|||Marketing department name |Sales department, sales division, marketing department, department |
|||Sales region name |Sales region, region |
|||Salesperson name |Businessperson, salesperson, personnel |
|||Material name |Product, product name |
|||Component model |Model, sheet type |
|||PN junction type |Junction type |
|||Technology type |Technology route |
|||Order quantity |Sales volume, sales quantity, order quantity |
|||Order amount |Sales amount |
|||Outbound quantity |Delivery quantity, outbound capacity, delivery capacity, outbound power, delivery power |
|Contract full cycle summary_CK |Sales contract full cycle data |Contract number |Contract code, contract |
|||Contract name |Contract name, contract title, customer contract |
|||Contract signing time |Contract signature time, contract signing time, contract effective time, effective time |
|||Contract signing company name |Contract signing company, contract signed company, signing company |
|||Sales company name |Sales company, contract execution company, contract principal company, contract company |
|||Marketing department |Marketing department, sales department, sales division, affiliated department |
|||Marketing department name |Marketing region, sales region, sales area |
|||Salesperson name |Salesperson, businessperson |
|||Ordering customer name |Customer, user, customer company |
|||Final customer name |Final user, end user |
|||Contract total amount_W |Contract sales volume, contract capacity, contract power |
|||Order quantity |Order power, order capacity, order volume, purchase order quantity, purchase order power, purchase order capacity |
|||Order unit price |Order unit price excluding tax |
|||Order amount |Purchase order amount, order amount excluding tax, purchase order amount excluding tax |
|||Total order price including tax |Total order price and tax, order price and tax amount |
|||Outbound quantity |Number of pieces shipped |


<span id="4684c75c"></span>
# Dataset–knowledge base configuration practices

<span id="5ef3eebc"></span>
## General configuration approach


* **The knowledge base name should be precise:**  Currently, the knowledge base uses a name/description key\-value (KV) structure. The system recalls knowledge based on the similarity between the user's question and the knowledge name. Therefore, the definition of the knowledge name must be precise and should match the question as closely as possible. Avoid using broad names.

* **Be cautious when defining knowledge**: If a question can be resolved by defining an expression in the dataset or by defining synonyms in the semantic model, there is no need to use the knowledge base.

* **Pay attention to generalization**: If defining knowledge resolves the current issue, it is recommended to perform regression testing to check whether the definition of this knowledge causes performance degradation for other questions.


<span id="0781ebac"></span>
### **Principle 1: Use custom rules to recall whenever possible**


* It is recommended to use "custom rules" as much as possible when configuring the knowledge base. The recall rules for the vast majority of knowledge can be identified by carefully configuring the rules.

* Providing information to the large model for reference every time is not the optimal way to configure the system. Unless there are special circumstances, frequent use of this approach is not recommended. It is recommended not to use the default recall method just for convenience, as this may unexpectedly worsen the quality of answers to certain questions.


<span id="ab17b23d"></span>
### **Principle 2: When a piece of knowledge applies to multiple scenarios, multiple precise rule\-based knowledge entries should be added, rather than a single vague rule\-based entry.** 

For example: Suppose a user asks a question related to the Doubao large model, this knowledge applies; at the same time, if the user asks a question related to the Doubao small model, this knowledge also applies. It is recommended not to use the default recall method just for convenience, but instead to configure two knowledge entries: one for rule\-based recall with the Doubao large model, and another for rule\-based recall with the Doubao small model.

When using rule\-based recall, business terms are not critical; simply write the beginning of the sentence where you wish to add the knowledge. In addition, special attention must be paid to the "preview" section, as this is the content ultimately transmitted to the large model. Ensure its accuracy. In rule\-based recall mode, business terms, conjunctions, and explanations can be arranged as needed. The key is to ensure the accuracy of the preview content.

Based on all question types in the question set and the fields in the dataset, determine the most precise rules so that the rule only applies to questions requiring the knowledge, while avoiding impact on other questions that do not require the knowledge.

Caution: If a piece of knowledge is added solely for calculation using certain fields, it is recommended to add a calculation expression field in the dataset to achieve this, rather than directly adding the knowledge. Otherwise, the outcome may unexpectedly worsen.

<span id="78425fec"></span>
## Planning & configuration examples

Usually, you can configure the internal terminology, jargon, and metric calculation logic related to the current dataset's business scenario in the knowledge base for this dataset. It is recommended to review each field of the current dataset individually. An example is shown below.


* Internal terminology and jargon

   
   |Dataset name |Business term |Synonym |Explanation (term definition) |Relevant dataset fields |
   |---|---|---|---|---|
   |Contract detail execution summary_CK |How are sales performing |Sales volume |“How are sales performing” refers to [purchase order quantity] and the corresponding [purchase order amount] |Order quantity, order amount, quantity shipped |
   ||Technology type |Technology route |Technology type indicates the product's technology type, including PERC, TOPCon, HJT, and other types | |
   |xxx shopping omnichannel analysis |Live/recorded broadcast |Program playback type |Among the playback types,<br><br>Live broadcast: playback type ≠ replay;<br><br>Recorded broadcast: playback type = replay; | |
   

* Metric calculation logic

   
   |Dataset name |Business term |Explanation (term definition) |
   |---|---|---|
   |xxx shopping omnichannel analysis |Cancellation rate |Cancellation amount / order amount |
   ||Outbound rate |Outbound amount / order amount |
   ||Delivery completion rate |Delivery completion amount / outbound amount |
   ||Return rate |Return amount / outbound amount |
   ||Conversion rate (quantity) |Sales quantity / order quantity |
   ||Conversion rate (amount) |Sales amount / order amount |
   ||Gross profit margin |Sales profit / sales revenue |
   ||Live broadcast conversion rate |Number of live broadcast transactions / number of live broadcast viewers |
   ||Fan retention |Net followers / total followers |
   ||Average order value \- WeChat Video Channel |Transaction amount / number of transactions |
   ||Average unit price |Order amount / order quantity |
   ||Number of playbacks |Within a period of time, count the number of times this item number appears in each playback time slot; count of time slots. |
   ||On\-air quantity / amount / profit (average) |Total quantity (profit or amount) / number of playbacks |
