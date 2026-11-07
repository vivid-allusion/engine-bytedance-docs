---
title: "Best Practices: Recommendations and Examples for Intelligent Data Query Questions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions"
---

<span id="006ab3bd"></span>
# General principles for asking questions

A good question should include the following key elements:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86c36002fd1c453aa58a3760d5427f0a~tplv-goo7wpa0wc-image.image" width="665px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adfaeba273eb478b9fa1d8b0a6417976~tplv-goo7wpa0wc-image.image" width="1707px" /></div>



|Element |Description |
|---|---|
|**Time** |Specify the time point or range for the data, such as "the last 7 days", "Labor Day last year", "within the past 30 days", or "the week of January 18". |
|**Metric** |Specify one or more metrics to query, such as "GMV" or "order volume". |
|**Filter conditions (optional)**  |Specify the statistical dimension of the data, such as "by province" or "by primary and secondary category". |
|**Statistical method (optional)**  |Specify the statistical method for the data, such as "How many XX are there?", "sum", "average", "maximum", "week\-over\-week", or "year\-over\-year". |
|**Presentation method (optional)**  |Supports tables as well as common data visualizations such as line charts, bar charts, and pie charts. |


Structured question descriptions can help obtain higher\-quality answers. You can use the following structured question description template as a starting point and modify or fill it in according to your specific needs.

```Markdown
## Analysis Objectives
(Clearly describe the core issue you want to analyze in one sentence) 

## Data Scope
Dataset: (clearly indicate which dataset or datasets are used)
Filtering criteria: (clearly specify the time range, customer range, product range, etc.) 

## Analysis Requirements
(Step 1: For example, calculate the overall key metrics) 
(Step 2: For example, conduct disaggregated analysis by a certain dimension) 
(Step 3: For example, conduct trend or comparative analysis)

## Output Requirements
(Specify the type of chart, report structure, or key conclusions you wish to see) 
```


<span id="dc3ad500"></span>
# Question description and recommendations for asking questions

<span id="38bb4957"></span>
## Scenario 1: Querying/processing data in a dataset

<span id="a24d90d0"></span>
### case 1: Querying specific data


* Intelligent data analysis capability description: When querying data from a specific table field in a dataset, the question does not need to exactly match the field name in the table. The large model will match the appropriate field based on its own understanding.

* Configuration/question recommendation: When **multiple field names in the dataset are very similar**, it is recommended to:

   * In the agent's dataset configuration: You can use the semantic configuration capability of the dataset to further configure synonyms and characteristics for each field, helping the large model understand the differences between fields and improve the accuracy of field matching.

   * When asking a query: The more detailed the description of the field you want to query in the question, the more accurate the field matching will be.


<span id="da0d9594"></span>
### case 2: Performing calculations on dataset fields


|Sub\-scenarios |Question suggestions |
|---|---|
|Calculations such as maximum, minimum, sorting, and period\-over\-period comparisons |It is best to specify the time granularity for period\-over\-period comparisons. |
|Understanding the calculation formulas for common metrics (such as xxx rate) |The general knowledge of large models can cover the calculation of some metrics in certain scenarios. For example, a large model can understand that "profit margin" = total profit / total sales revenue; however, other xxx rates may not be within the general knowledge of the large model, which may result in a failure to understand.<br><br>Therefore, when dealing with very common calculation metrics, you can ask questions directly. If you find that the AI model misunderstands the metrics in its response, it is recommended to calculate the metrics you want to query directly from the dataset and prepare them in advance. |


<span id="8737b61a"></span>
## Scenario 2: Ambiguous questions


|Segmented scenarios |Question\-asking recommendations |
|---|---|
|Very vague questions |Avoid very vague questions.<br><br>For example: `Check the situation in each region.` The AI model cannot accurately match which metrics you need to analyze. |
|Questions with vague intent |If you find many questions with vague intent while using the intelligent analysis agent, you can try:<br><br><br>* After configuring intent clarification, the intelligent agent will proactively ask follow\-up questions for vague intent issues to obtain clearer questions.<br><br>* If vague intent questions are relatively common and typical, you can configure fuzzy questions to associate vague questions with a clear question, improving the AI model's understanding of similar vague intent questions. |
|Cannot remember specific dimension values |When you cannot remember the dimension values to filter, you can ask questions using "contains".<br><br>For example, "Author nickname: Xiaoming, daily follower count greater than 100,000, what is the xxx tag?" \-\-\-\> "Author nickname**contains**Xiaoming, daily follower count greater than 100,000, what is the xxx tag?". |


<span id="20852db1"></span>
## Scenario 3: Personnel references


* The intelligent analysis Agent currently cannot proactively identify personnel identities. You should avoid questions such as “`What is the sales revenue for the area I am responsible for`” that contain unclear personnel references (“`I`”).

* It is recommended to directly specify the person's name in the question description, for example: “`What is the sales revenue for the area Xiaoming is responsible for`”, “`What is the sales revenue for the area managed by regional manager Xiaoming`”.


<span id="40601918"></span>
## Scenario 4: Multiple intents

When asking questions using the intelligent analysis Agent, do not include multiple intents in a single interaction. That is, each question should query only one piece of data.

**Incorrect example**: `Which are the top 10 products with the highest profit in 2024?` `What are the year-over-year and month-over-month growth rates for the profit and sales revenue of these products, respectively?` `Which product has the largest year-over-year increase?` — In this example, multiple sub\-intents are included within a single question interaction.

<span id="f4748bff"></span>
## Scenario 5: Advanced question description—based on Markdown syntax

Organizing your questions using Markdown syntax (such as headings, lists, and bold text) can effectively enhance the model's ability to recognize the structure and key points of the question, thereby generating reports that better meet expectations.


|**Non\-elegant question** ❌ |**Elegant question** ✅ |
|---|---|
|Analyze the revenue situation of xx brand cars in June and see what changes have occurred. |```Markdown```<br>```## Analysis Objectives```<br>```Analyze the revenue situation and reasons for fluctuations of XX Brand Automobile Technology Co., Ltd. in June 2025.```<br>``````<br>```## Dataset Requirements```<br>```- **Dataset**: Income Wide Table_Billing Granularity```<br>```- **Filter Criteria**: Billing Month is June 2025```<br>```- **Core Fields**: Billing Amount, Product Name, Billing Item```<br>``````<br>```## Analysis Requirements```<br>```1. Summarize the total revenue for June, compare it with that of May, and calculate the Period-on-period Ratio.```<br>```2. Break down and attribute revenue by the dimensions of "Product Name" and "Billing Item".```<br>```3. Draw a revenue trend chart for the past 30 days and analyze whether there are any abnormal fluctuations.```<br>``````<br>```## Output```<br>```- The final report shall include total revenue and month-on-month data, a pie chart of revenue structure, and a line chart of revenue trends.```<br> |


<span id="f818535c"></span>
# Common issues & optimization ideas

<span id="d93026b1"></span>
## Incorrect table selection/incorrect returned results


|Question examples |Problem symptoms & possible causes |Optimization ideas |
|---|---|---|
|How many contracts were signed this year? |* The returned data is incorrect. After checking the intelligent agent's reasoning process and execution script, it was found that the data retrieval logic was wrong and the wrong table was queried.<br><br>* The main reason is that multiple datasets (customer detail table, contract dimension table) added to the intelligent agent contain several contract\-related fields, which caused the agent to select the wrong table. |* When there are similar fields across multiple tables, it is recommended to first analyze the business analysis scenarios to determine whether these datasets require table merging or other ETL processing.<br><br>* If multiple datasets are indeed needed and it is necessary to retain multiple fields with similar names, configure the semantic model for each field in the dataset based on differences in business meaning.<br><br>* In special scenarios where table selection priorities differ, you can emphasize the priority of the business scenario in the 'semantic model name' and 'semantic model description' of the intelligent agent's dataset semantic model. This ensures that the corresponding table will be prioritized for selection in subsequent relevant scenarios. |
|How are the sales of xxx (product name)? |Such ambiguous questions may result in no data being retrieved (SQL execution failure). Possible reasons:<br><br><br>* If fields such as 'order quantity', 'order amount', 'return quantity', and 'return amount' exist in the relevant data tables of the dataset, and no synonyms or semantic settings are configured for these field names, the large model may become confused when interpreting quantity and amount fields.<br><br>* In business scenarios, 'How are the sales?' refers to viewing data for the 'order quantity' and 'order amount' fields, but the large model may misinterpret this. |* Configure the semantic model for fields in the dataset and set up synonyms accordingly.<br><br>* Add knowledge related to 'How are the sales?' in the dataset's knowledge base, and clearly specify the associated dataset fields. |
|How were the sales of Marketing Department 1 in May? |* The returned data is incorrect. After reviewing the intelligent agent's reasoning process and execution script, it was found that the data retrieval logic was incorrect and the time field used for filtering was wrong.<br><br>* The main reason is that there are many date\-type fields in the dataset, and the large model selected the wrong time field for filtering. |* Set semantic models for each date field in the dataset, configure synonyms, and specify in the field description which business scenario each date refers to. |


<span id="6a113078"></span>
## Returned results contain too little content


|Example questions |Observed issues and possible causes |Optimization approach |
|---|---|---|
|What sales contracts did xxx (subsidiary name) have last year? |The returned query results only include a list of contract codes, but in the business scenario, it is expected to return more contract\-related information, such as contract code, Sales representative, contract amount, receivable amount, and more. |* To display more returned information for a single question, directly specify the required data range in the question description.<br><br>* For general business scenarios where all contract\-related queries typically need to return a fixed set of contract\-related fields, this can also be configured in the agent's prompt. |


<span id="8af7c667"></span>
## Incorrect understanding of the question


|Example questions |Observed issues and possible causes |Optimization approach |
|---|---|---|
|Which sales departments are losing money? |Incorrect understanding of the question; the meaning of "losing money" was not correctly interpreted.<br><br>For example, in the business scenario, "losing money" refers to data in the contract dimension table where the sales profit is less than 0. |Add a new entry to the knowledge base to clearly define the meaning of "losing money" in the data. |
|What is the CAC trend for new products in the third quarter? |In this question, "CAC" is a business term in the user operations scenario: Customer Acquisition Cost (CAC), which is not understood by the large model. |Add a new entry to the knowledge base to clarify the calculation formula for "CAC" and the definitions of each data item in the agent dataset used in the formula. |


<span id="18715645"></span>
## Incorrect data units in the query results


|Example questions |Observed issues and possible causes |Optimization approach |
|---|---|---|
|What is the trend of electric power generation capacity in North China in the third quarter? |The data query results return values such as 1,000,1000 W (watts). Since the unit is W (watts), the result values are particularly large. To improve the readability of the data query results, the unit of the query results needs to be standardized to MW (megawatts). |* If only a single question involves unit conversion of this kind, you can directly specify which unit the returned value should use when asking the question.<br><br>* For regular business scenarios, where business data units need to be unified to a fixed unit, you can also set this requirement in the agent's Prompt to enforce unit consistency when returning calculation results. |
