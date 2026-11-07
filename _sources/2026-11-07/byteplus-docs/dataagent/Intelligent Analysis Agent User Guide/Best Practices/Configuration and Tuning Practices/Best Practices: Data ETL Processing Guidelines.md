---
title: "Best Practices: Data ETL Processing Guidelines"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Best_Practices_Data_ETL_Processing_Guidelines"
---

This article introduces the operational approaches and practical scenarios for configuring datasets for the intelligent analysis Agent, including preliminary planning, data processing, and dataset configuration.

<span id="0a896ef0"></span>
# General principles


* **Dataset quantity limit**: To ensure performance and accuracy, it is recommended that the number of datasets associated with an Agent does not exceed **5**.

* **Field quantity limit**: The total number of fields associated with an Agent is recommended not to exceed **300**.

* **Field clarity**: The fields and dimension values within the datasets of the Agent should be managed to reduce or eliminate ambiguities or conflicts (such as fields with the same name but different meanings).

* Whenever possible, perform ETL processing in advance to avoid real\-time multi\-table join calculations; if unavoidable, the number of rows in datasets involved in multi\-table joins is recommended not to exceed 10,000.


<span id="39f2e5fd"></span>
# Data planning and preparation

After completing the preliminary planning of the Agent's application scenarios and user roles, you need to analyze and organize the required datasets and business metrics based on typical questions from each user role. The following is a simple example.


1. Based on the preliminary planning of the Agent's application scenarios, organize the involved data sources and metrics.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51fba89e6bfc444984e388ca9a573f60~tplv-goo7wpa0wc-image.image) </span>


2. Sequentially organize the names of each dataset table and any special notes for the corresponding tables.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f44b3d30138494c89d8bf8ebb8793ee~tplv-goo7wpa0wc-image.image) </span>


3. Organize the key fields, field data types, and business meanings of fields (such as whether additional explanation is needed for the field) in each data table under the current Agent's application scenarios.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0afb0a556568477ca982b688633ca001~tplv-goo7wpa0wc-image.image) </span>


4. Organize information such as the dimension values of high\-frequency dimension fields and explanations of dimension fields under the current Agent's application scenarios.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/991c7a9cfd1248a084f553a4a0046131~tplv-goo7wpa0wc-image.image) </span>

<span id="27e7f6b7"></span>
# Data processing

After completing the planning and organization of datasets, you need to process the data in advance as necessary based on the organized business metrics and dimension fields, ensuring that the datasets integrated with the Agent meet the requirements for the number and meaning of datasets and fields as outlined in the general principles.

<span id="0531f743"></span>
## ETL guidelines and restrictions

High\-quality data is the foundation for the success of DataAgent\-AnalysisAgent. The following ETL guidelines are intended to ensure the standardization and usability of input data, which are prerequisites for accurate analysis.

<span id="8fbad03b"></span>
### Key point 1: **Cross\-table filtering logic is not supported**


* **Problem**: It is not possible to, within a single query, first obtain a condition (such as a time range) from table A and then use that condition to filter table B.

* **Solution**: Such complex cross\-table logic should be handled by ETL, which pre\-associates relevant information into a single wide table.


<span id="1f3c105e"></span>
### **Key point 2: Direct concatenation of multiple fact tables is prohibited**


* **Problem**: Directly concatenating multiple fact tables with different granularities results in data duplication (Cartesian product), leading to incorrect results.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1631831b185c4d54ad1368a766c84d19~tplv-goo7wpa0wc-image.image" width="824px" /></div>



* **Solution**: Each fact table should be aggregated by common dimensions, and concatenation should be performed only after unifying the granularity.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4d53af0f8114d7aab5f14841ad03f82~tplv-goo7wpa0wc-image.image" width="1720px" /></div>


<span id="46373b01"></span>
### Key point 3: Do not add aggregate results to detail tables


* **Problem**: Directly adding pre\-calculated aggregate values (such as averages) to detail data rows causes errors during secondary aggregation (such as totals).

* **Solution**: Maintain the originality of the detail table; aggregation calculations should be performed dynamically during queries or handled in a dedicated aggregation layer.


<span id="3858f70d"></span>
### Key point 4: Pivot tables must not be used as base tables


* **Problem**: Pivot tables are artificially defined formats for display purposes; their structure (such as row\-column transformations) cannot be understood by AI models and cannot serve as stable data sources.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beb665ca917644a7a8320b1c45216a97~tplv-goo7wpa0wc-image.image" width="662px" />   </div>
   

* **Solution**: Standard, non\-pivoted two\-dimensional tables should be used as data sources.


<span id="488115a3"></span>
### Key point 5: **The data source should be a BI dataset rather than a visualization chart**


* **Problem**: Customers sometimes provide charts or the data from them that have already been visualized and processed in BI tools. These data are often heavily processed and are not suitable as the original input for the Agent.

* **Solution**: The underlying, raw dataset from the BI system must be used.

* **Example:** 

   * Example table 1: Activity detail table

      
      |**Activity name** |**Start time** |**End time** |**Number of participants** |
      |---|---|---|---|
      |Activity 1 |2025.1 |2025.7 |37 |
      |Activity 2 |2025.3 |2025.8 |43 |
      

   * Example table 2: Marketing summary table

      
      |**Time range** |**Number of participants** |
      |---|---|
      |2025.1 |130 |
      |2025.2 |560 |
      |2025.3 |270 |
      

   * Example scenario description: There are two tables above (activity detail table, marketing summary table). When using the intelligent analysis Agent, if you want to query the time range of Activity 1 from the "activity detail table" and then use this range to query the total number of participants in marketing within this time range from the "marketing summary table", this type of data query is not supported. This is because the intelligent analysis Agent's cross\-table query logic is not ETL table merging, but cross\-table filtering.


<span id="41df8db6"></span>
### Key point 6: Focus on point\-in\-time balance indicators


* **Issue**: For balance\-type "point\-in\-time" indicators, conventional summing and aggregation (SUM) over a time period is meaningless.

* **Solution**: When asking questions, it is necessary to clearly specify that the query is for the balance at a specific point in time, rather than an aggregation over a time period.

* **Example:** 

   
   |**Time** |**Business type** |**Balance** |**Loss amount** |**Profit amount** |
   |---|---|---|---|---|
   |January |Credit card |50000 |400 |100 |
   |February |Credit card |40000 |\-300 |\-200 |
   |January |Wealth management fund |1000000 |600 |300 |
   |February |Wealth management fund |1200000 |200 |\-400 |
   

   In this type of table, the data for each month is already cumulative, so it cannot be merged for calculation. Normally, all indicators require merged calculation, such as calculating the overall balance for January to February.

   
   |**Business type** |**Balance (sum)**  |
   |---|---|
   |Credit card |90000 |
   |Wealth management fund |2200000 |
   

   This type of data is incorrect. The proper question should be for the user to directly ask what the balance is for February. Therefore, this type of table is not suitable for question\-based querying, or in question\-based scenarios, it is necessary to understand the business meaning of the table itself and directly ask for a specific point in time.


<span id="41b65497"></span>
### Other


* For ETL processes that comply with the above specifications, it is recommended to perform table merging as much as possible. Otherwise, having too many datasets within one Agent will affect the performance and accuracy of the intelligent entity.

* All ETL standards should reference BI datasets, not BI visualization charts. Many customers use BI visualization tables as base tables, which is incorrect.


<span id="17a4bbdc"></span>
# Application practice

<span id="33db2f6d"></span>
## Practice 1: Example of using data cleansing operators

The intelligent analysis Agent provides you with visual modeling capabilities and supports various data cleansing operators (field settings, multi\-table joins, row merging, and more). You can flexibly process data by dragging the corresponding operators on the visual modeling page. The following introduces common operators and their applicable scenarios.


|Common operators |Advantages / usage recommendations |
|---|---|
|Calculated column |* Operator definition: The operator with the highest degree of flexibility, equivalent to writing SQL to construct a new field, supports calling various functions.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89a353011ded4ca3aba0512d6123004f~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Applicable scenario: Suitable for data processing scenarios where a new field needs to be added.<br><br>* Usage approach: Determine whether a new field needs to be added \> How to describe the new field in natural language \> How to express the fields and data processing logic contained in the natural language using functions \> Call functions to process the involved fields and generate new field values<br><br>* Basic usage of functions:<br><br>   * Numeric fields: Functions can typically be called to perform addition, subtraction, multiplication, and division calculations on numeric fields.<br><br>   * Text fields:<br><br>      * Typical scenario: Call the case when function to tag text fields.<br><br>      * Example: `case when 'activity'='running' then 'High-value activity' else 'Low-value activity' end`.<br><br>   * Other function usage scenarios: Date format conversion, JSON nesting |
|Row merge operator |* Operator definition: Two sets of data are joined by rows to become a single set of data.<br><br>* Applicable scenario: For example, two tables respectively store consumption behavior data for men and women; the data from both tables needs to be merged into a single table. |
|More operators |Please refer to [Data Cleaning](https://docs.byteplus.com/docs/dataagent/Data_Cleansing). |


<span id="5edd05fc"></span>
## Practice 2: Handling practices for time fields (business date, creation time, and so on)


* **General recommendations for handling time fields**

   * For fields related to "time" and "date", always use the date or datetime type, and avoid using int or string types.

   * It is recommended to present all time dimensions at the finest granularity. For example, if the finest granularity of a metric is at the day level, then there is no need for separate fields for quarter, month, or year; a "date field" is sufficient, and the model will use date functions to implement this. However, if the finest granularity can only reach the month level, then present it at the month level.

* **Example scenario**:

   * The customer's new intelligent agent has a "work order\-node details" dataset. In the work order scenario, there is a business time field: T1. In the node scenario, the business time field T2 is missing and can only use the pdate field instead.

   * When using the intelligent agent, business queries often mix T1 and T2, and frequently lack the specific names of time fields, resulting in low data query accuracy.

* **Incorrect approach**:

   To configure the agent's knowledge so that the model knows:

   * To use knowledge configuration to automatically identify whether the T1 field or T2 field should be used to filter the dataset based on the structure of the question and the metric.

   * To use knowledge configuration to enable the model to automatically identify and handle time fields, so that in the node metric scenario, the pdate field is processed as the T2 field, and metric statistics require additional deduplication.

      This approach places high demands on the model's understanding of dataset fields and business logic, and the results are poor.

* **Correct optimization approach**: ETL processing + elegant querying

   * By leveraging the visual modeling capabilities of the intelligent analysis agent, clean and process the time fields in the incremental table. Processing logic: In the node scenario, write the pdate field into the T2 field.

   * When querying with the intelligent agent, clearly specify the business scenario and metric name in the problem description.


<span id="a0ae4685"></span>
## Practice 3: Handling practices for multiple tables

After completing the planning and sorting of the agent dataset, if the business scenario of the application may involve multiple tables, the possible issues and practical handling experience at each stage are as follows.


|Model process stages |Common issues |Solutions |
|---|---|---|
|Dataset preprocessing |* Multi\-table selection strategy failure: When the historical table and the prediction table are not merged, the table selection strategy performs poorly, because the only difference between the two tables is the statistical granularity of the year, resulting in feature configuration failures.<br><br>* Incompatible time field format: The original time field is a string such as "2021 Q4", which cannot be directly converted to a date format, causing errors when the model extracts the year or quarter.<br><br>* Deviation in understanding fields with multiple enumeration values:<br><br>   * Price range field: Contains more than 40 numerical intervals (such as 0–25 USD, 25–50 USD), and pure numeric symbol descriptions (such as "0<25") lead to inaccurate model recall; when enumeration values are too long, wide\-domain filtering is prone to omissions or errors. |1. Force merging multiple tables: Standardize fields in the historical and prediction tables, resolve differences in statistical granularity through field mapping, simplify table selection logic, and improve model association efficiency.<br><br>2. Standardize time format: Convert "year + quarter" strings to "YYYY\-MM\-DD" format (for example, "2021 Q4" to "2021\-12\-31") to ensure the model reliably recognizes date fields.<br><br>3. Handle fields with multiple enumeration values:<br><br>   * Add business descriptions: Add unit descriptions such as "USD" to price range field values (for example, "0–25 USD") to enhance the model's semantic understanding.<br><br>   * Convert to numeric fields: Calculate the median value of the price range (for example, 0–25 USD takes 12.5), use numeric interval filtering (such as "<100 USD") instead of enumeration value matching to resolve omissions and errors. |
|Table selection and field recall issues |* In multi\-table scenarios, the model's table association logic is unclear, and insufficient synonyms and business descriptions for fields lead to table selection errors or field matching failures. |* Build a semantic model knowledge base: Define table characteristics (for example, label the "historical sales table" as "2021\-2024 data"), field synonyms (for example, "shipment volume" as a synonym for "sales volume"), and business descriptions (for example, "price range" explains "mobile phone price range"), to ensure the model achieves precise recall. |
|SQL generation |* Complex problems (including multi\-field calculations) trigger the model to generate SQL in a probabilistic manner. Syntax errors, anomalies in nested logic, or limitations of the transcription module (such as only supporting single SQL statements) result in an error rate of over 50 percent, with no clear pattern. |1. Establish a knowledge base for the calculation layer: For high\-frequency error metrics (such as "penetration rate"), specify the optimal SQL approach (such as "prefer using window functions for calculation"), and guide the model to generate compliant SQL through affirmative statements, avoiding the propagation of errors caused by negative restrictions (such as "prohibit multi\-level nesting").<br><br>2. Case comparison analysis: Collect both successful and failed SQL cases, compare syntax differences (such as subqueries versus aggregate functions), and supplement business rules as needed (such as "when filtering with multiple conditions, prefer using JOIN associations").<br><br>3. System\-level output specifications: In the prompt, strictly require retention of decimal points and addition of units (such as "USD" and "units"), and standardize the output format. |


<span id="3abe7c02"></span>
## Practice 4: Reference for scenario metric definitions and calculation formulas

<span id="8c9d0ef3"></span>
### Basic metric definitions


|Metric name |English abbreviation |Calculation formula |Explanation |
|---|---|---|---|
|**Impressions** |Impression |Total number of ad impressions |Measures ad reach |
|**Clicks** |Click |Total number of user clicks on the ad |Measures ad attractiveness |
|**Click\-through rate** |CTR |Clicks ÷ Impressions × 100% |Measures creative effectiveness |
|**Installs** |Install |Total number of users who installed the application |Measures conversion effectiveness |
|**Install rate** |IR |Installs ÷ Clicks × 100% |Measures landing page effectiveness |
|**Cost per install** |CPI |Total spend ÷ Installs |Measures customer acquisition cost |
|**Return on investment** |ROI |LTV ÷ CPI × 100% |Measures campaign efficiency |


<span id="c6319dc1"></span>
### Advanced metric definitions


|Metric name |English abbreviation |Calculation formula |Explanation |
|---|---|---|---|
|**User lifetime value** |LTV |ARPU × number of days in user lifetime |Total user value |
|**Average revenue per user** |ARPU |Total revenue ÷ total number of users |User value density |
|**Average revenue per paying user** |ARPPU |Total revenue ÷ number of paying users |Paying user value |
|**Retention rate** |Retention |Number of retained users ÷ number of new users × 100% |User quality metric |
|**Pay rate** |Pay Rate |Number of paying users ÷ total number of users × 100% |Paid conversion efficiency |


<span id="56a248eb"></span>
### Year\-over\-year and month\-over\-month calculation methods

**Month\-over\-month growth rate:**  $$ Month\-over\-month growth rate = \frac{Current period value \- Previous period value}{Previous period value} \times 100% $$

**Year\-over\-year growth rate:**  $$ Year\-over\-year growth rate = \frac{Current period value \- Value in the same period last year}{Value in the same period last year} \times 100% $$

<span id="01575120"></span>
# Common issues and considerations


|Caution |Note |Problem dataset examples |Unaddressed negative impacts |
|---|---|---|---|
|Ensure that table names and field names are unique and unambiguous |* Field aliases in Chinese used in the dataset must be unique<br><br>* Avoid fields with similar or ambiguous meanings; delete redundant fields directly<br><br>* Ensure that each dataset is named completely and can represent the actual meaning of the data<br><br>* If multiple related metrics are distributed across multiple tables, it is recommended to merge the tables<br><br>* Ensure that within the same dataset, as well as across all datasets, the corresponding metric names are not duplicated and are distinguishable |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Order ID/order_id represents the primary key ID of the order table.</div><br><br><br><div data-tips="true" data-tips-type="tip">Order number/order_num is the business document number.</div><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Order table/purchase order table can be rewritten as order statistics table, shipment detail table, and other detail tables.</div><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Order amount, purchase amount, and contract amount exist in multiple tables. The main subject of analysis is the contract, which is summarized in a contract summary table, associating each order and shipment amount data under the contract.</div><br> |The model may use similar field names for understanding and responses, resulting in inaccurate results. |
|Set Chinese aliases for fields |* Fields in the database may be in English. If queries are made in Chinese, it is necessary to maintain the corresponding Chinese field names.<br><br>* For bilingual queries, it is preferable to use two separate datasets for Chinese and English, respectively. If only one dataset must be used, ensure that the Chinese and English translations are accurate and complete, and supplement with descriptive information. |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Expression: order_num</div><br><br><br><div data-tips="true" data-tips-type="tip">Field name: order number</div><br> |The model cannot perfectly map your Chinese natural language queries to English fields, and therefore cannot provide satisfactory answers. |
|Set accurate field types (such as date and time, geographic information, and more). |* Keywords must be identified, matched, and processed based on the field types you set. Therefore, for fields related to date, time, or geographic latitude, you need to perform data type conversion on the dataset page.<br><br>* If there are time fields in the dataset that are not relevant to the business scenario, it is recommended to delete them directly to prevent interference. |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Date and time format configuration</div><br><br><br><div data-tips="true" data-tips-type="tip">Order creation time: text</div><br><br><br><div data-tips="true" data-tips-type="tip">Other time fields: date format</div><br><br><br><div data-tips="true" data-tips-type="tip">The model tends to prioritize date and time fields.</div><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">case2: Statistical reports do not have date and time formats, only statistical period year and month.</div><br><br><br><div data-tips="true" data-tips-type="tip">Method 1: Create a date field, CAST(toString(<code>year</code>)</div><br><br><br><div data-tips="true" data-tips-type="tip">Method 2: Set year and month as numeric types, and provide description accordingly.</div><br> |The model cannot accurately select and recall the required date and time fields.<br><br>The generated SQL uses commands that are not compatible, resulting in output errors. |
|Set clear field descriptions. |* Fields in the dataset can be configured with descriptive information. You can add Chinese descriptions with business significance in the description, and ensure that the description content is unique.<br><br>* The typical structure of a description includes: meaning, alias, scope, example, and special case.<br><br>* After configuring the description, it takes effect T+1; generally, the process completes before 1 AM, and large data volumes may require validation or acceptance testing. |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">case1: Unified manufacturer</div><br><br><br><div data-tips="true" data-tips-type="tip">Automotive OEM name, for example, ByteDance; 'Byte' represents ByteDance.</div><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">case2: Unified new energy type</div><br><br><br><div data-tips="true" data-tips-type="tip">Refers to the energy type of the automobile, including PET for gasoline vehicles, EV for electric vehicles, HEV for hybrid vehicles, and PHEV for plug\-in hybrid vehicles.</div><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">case3: Month</div><br><br><br><div data-tips="true" data-tips-type="tip">Month, including 01–12; 03 represents March.</div><br> |The model cannot accurately select and recall the correct fields. |
|Dataset – add new calculated fields. |* To query fields other than existing dimensions and metrics, click "Add Field" in the dataset according to the calculation logic of the new field, thereby "add a calculated dimension" or "add a calculated metric".<br><br>* The factor fields required for calculated fields must also be present in the dataset.<br><br>* At the same time, certain specific calculation fields related to period\-over\-period comparison, previous period, and dates are best presented in the form of metrics.<br><br>* Finally, if there are complex time aggregation calculation fields, it is best to preprocess them in advance using the dataset. |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The lead conversion rate field requires a calculated field.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Calculation method: converted order leads / number of leads, or converted order leads / number of valid leads</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Cannot be directly aggregated: avg(January conversion rate + February conversion rate) ≠ conversion rate for January to February</div><br><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Achievement rate = sum(output) / sum(target)</div><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Concept fields for period\-over\-period comparison, previous period, and current period are preferably provided directly by the dataset without additional configuration</div><br> |* Unable to directly identify and analyze unknown dimensions or metrics, and cannot return results.<br><br>* Incorrectly handled fields that require real\-time calculation, resulting in inaccurate returned results. |
|Flag\-type fields comply with Boolean value rules. |* Boolean structure content has two possible results: true and false. You can use 0/1, true/false, or yes/no as indicators.<br><br>* If the relevant indicator method cannot be accurately identified, supplementary explanation can be provided in the description.<br><br>* Non\-standard description methods need to be converted in advance. |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Maintenance status: 0/1</div><br><br><br><div data-tips="true" data-tips-type="tip">Description: Indicates whether the factory repair work order is of the maintenance type; 0 means no, 1 means yes</div><br><br><br><div data-tips="true" data-tips-type="tip">Maintenance status description: non\-maintenance return to factory / maintenance return to factory</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to directly delete easily confused fields</div><br> |The model cannot accurately identify certain business condition judgments. |
