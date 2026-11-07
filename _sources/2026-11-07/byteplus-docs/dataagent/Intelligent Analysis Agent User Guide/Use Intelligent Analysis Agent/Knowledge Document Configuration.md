---
title: "Knowledge Document Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Knowledge_Document_Configuration"
---

In Deep Research Agent usage scenarios, the product also provides features such as online search and knowledge document configuration. This article introduces how to configure the knowledge document feature.

<span id="e71ac478"></span>
# Feature overview

Knowledge document configuration is the dedicated knowledge hub for Deep Research Agent, supporting the upload of enterprise private documents. Through intelligent matching and structured extraction, internal knowledge is accurately injected into the analysis process. This complements online search, ensuring that research conclusions have both timeliness and business depth.

Knowledge documents can be categorized into three types: business knowledge, analysis templates, and analysis reports. The following is a comparative introduction to these three types of knowledge.


|Detailed comparison items |Business knowledge |Analysis template |Analysis report |
|---|---|---|---|
|Knowledge content |Essential background knowledge and definitions required for daily business operations, helping the model interpret data more accurately.<br><br>For example: metric definition explanations, activity event configuration, business process specifications. |Standard analytical approaches or steps for similar business problems, used to guide the model in breaking down issues.<br><br>For example: order volume fluctuations → analyze causes step by step by channel, user type, and time distribution. |Completed business analysis results, including historical data, conclusions, and insights, for reuse and reference.<br><br>For example: analysis report on marketing campaign effectiveness for the previous quarter. |
|Recall mechanism |Recall at the chunk level, supporting efficient vector matching. |Full recall to ensure structural completeness; template quantity is limited to 1. |Automatically extract the framework structure and align by structural logic during recall. |
|Notes |It is recommended to write business knowledge in a **structured and chunked** manner to improve recall granularity and quality. |None |In on\-premises scenarios, the analysis report knowledge type is disabled by default. To enable this feature switch, please contact Volcano Engine technical support. |
|Knowledge examples |See the following section: [Knowledge example: Business knowledge](https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration#d6ab8376). |See the following section: [Knowledge example: analysis template](https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration#828851bb). |See the following section: [Knowledge example: analysis report](https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration#76547ffd). |


<span id="a2037ed9"></span>
# Usage restrictions


* Supported local file types for upload: txt, md, doc, docx, ppt, pdf, xlsx, xls, csv.

* The maximum size for local files is 100 MB.


<span id="d98d9277"></span>
# Applicable scenarios


|Scenario types |Typical use cases |
|---|---|
|**Precise knowledge Q&A** |Consult specific product standards, service processes, or business rules, and directly return knowledge fragments with sources. |
|**Automatic report generation** |Invoke historical analysis frameworks to generate new reports and reuse mature structures. |
|**Scenario\-based research** |Focus on a specific type of issue (such as "customer complaint analysis"), only invoking related documents and filtering out irrelevant information. |


<span id="2ff57454"></span>
# Knowledge configuration

<span id="acdd0f13"></span>
## Upload knowledge


1. Select the Deep Research Agent that requires knowledge document configuration from the agent list, and click "Agent configuration" to enter the agent configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8af1ba58d2247be8d201e0c35710d1d~tplv-goo7wpa0wc-image.image) </span>

2. Click "Knowledge configuration", select "Add knowledge", enter the knowledge name, upload the knowledge file, and then click "Save" to enable the knowledge document feature.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13d658641a014d1e8d64e610f930959f~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration instructions |
   |---|---|
   |Knowledge name |Custom knowledge name. Try to ensure that the knowledge name covers the **core keywords** as much as possible to facilitate subsequent retrieval. At the same time, the agent supports automatic identification of the knowledge type based on the knowledge name. The naming format and the corresponding relationship with the identified knowledge type are as follows.<br><br><br>* `BUSINESS_KNOWLEDGE_knowledge core keywords`: Business knowledge.<br><br>* `ANALYSIS_TEMPLATE_knowledge core keywords`: Analysis template.<br><br>* `ANALYSIS_REPORT_knowledge core keywords`: Analysis report. |
   |Knowledge source & file |Currently, only local file uploads are supported as knowledge sources. You can click the "Upload File" button and select a local file that meets the format requirements following the interface prompts. |
   |Knowledge classification |Select the classification method for the knowledge you are uploading. The following options are supported:<br><br><br>* Automatic classification (default): The agent will automatically parse and categorize the uploaded knowledge.<br><br>* Manual classification: You manually select the type of the current knowledge. This feature is supported starting from version 3.3.0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, three types of knowledge can be selected: business knowledge, analysis templates, and analysis reports (in privatized scenarios, this type is disabled by default and requires enabling the feature switch separately). For more information on the comparison of the three supported types, please refer to the above <a href="https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration#e71ac478">Feature overview</a>section.</div><br> |
   |Image content parsing |Select whether to parse the image content in the uploaded document and extract the image content as knowledge. If you choose to parse images, the time required for knowledge content extraction and processing will be extended. |
   

3. The user can click the dialog box to select a built\-in question to ask, or directly enter a question related to the knowledge document.

   
   |Natural language inquiry |Quickly view recommended questions |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a37ed5bc2e484b449b200a751127bb32~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The main usage of the agent is that users can directly describe their in\-depth research needs to the agent in text. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed2968b046394dcc87682d1225c74981~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Recommended questions are provided below the dialog box. Users can click any recommended question to ask directly.<br><br>* Recommended questions are automatically generated based on users' historical queries and can also be customized. For specific configuration methods, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures). |
   


<span id="869c890a"></span>
## Knowledge reclassification/editing/deletion

After uploading and configuring knowledge, you can click the edit or delete button next to the knowledge to edit or delete it. When editing knowledge, you can reclassify and tag the knowledge, or modify parameters such as the knowledge name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d971f19de39c4c2fa9aa2458bc3556ee~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e98b4e8fd99944c196c27b45f8c59145~tplv-goo7wpa0wc-image.image) </span>

<span id="6c1d1828"></span>
# Reference: Knowledge example

<span id="d6ab8376"></span>
## Knowledge example: Business knowledge

For Deep Research Agent, upload a sample knowledge file "Consumer Behavior Analysis 5W2H Model.docx". If the user asks "Use the Consumer Behavior Analysis 5W2H Model to analyze this year's consumer behavior", Deep Research Agent will automatically identify and utilize this business knowledge to generate a new report.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/907de237435246a0b384fc816265baa8~tplv-goo7wpa0wc-image.image" name="Consumer Behavior Analysis Framework.docx">Consumer Behavior Analysis Framework.docx</Attachment>



|Input business knowledge content |Report content output by the agent |
|---|---|
|* **5W2H model**:<br><br>   * Who (audience profile): age, gender, region, income level, consumption preferences (for example, mothers and infants focus on safety certification);<br><br>   * What (product categories): high\-frequency necessities (grain and oil) versus low\-frequency durable goods (home appliances);<br><br>   * Why (consumption motivation): functional needs (such as mobile phone battery life) versus emotional needs (brand identity);<br><br>   * When (consumption time): seasonality (summer cold drinks), scenario\-based (late\-night food delivery);<br><br>   * Where (consumption channel): online platforms (Taobao / Douyin) vs offline scenarios (convenience stores / shopping centers);<br><br>   * How (consumption method): impulsive consumption (live\-stream flash sales) vs rational decision\-making (using price comparison apps);<br><br>   * How much (consumption amount): average transaction value, repeat purchase rate, LTV (user lifetime value). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5115fcf9d8d844d7843967a27b95e99d~tplv-goo7wpa0wc-image.image) </span> |



* Store fragmented content such as rule manuals and scenario guides for daily use.

* Adopt a **preliminary screening→ranking→focusing** recall strategy: first match 30 relevant text fragments, then use AI to rank them and retain only the content from the top 3 most relevant documents, avoiding information fragmentation.


<span id="828851bb"></span>
## Knowledge example: analysis template

<span id="198f1d97"></span>
### Template usage

To generate an analysis report for all activity reviews in the first quarter of this year, upload sample knowledge of "Analysis report template for all activity reviews in the first quarter of this year.pdf" to the agent. The agent will automatically generate a new report based on the overall report structure and analysis template requirements from the sample knowledge.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85ffbfd92d2f47959346dd2f4f943210~tplv-goo7wpa0wc-image.image" name="Template for the Review and Analysis Report of All Activities in the First Quarter of This Year.pdf">Template for the Review and Analysis Report of All Activities in the First Quarter of This Year.pdf</Attachment>



|Input analysis framework requirements |Report content output by the intelligent agent |
|---|---|
|Overall contribution and trends of Q1 activities<br><br><br>* Analysis objective: overview of the total value and performance rhythm generated by all activities in the first quarter<br><br>* Specified charts/presentation methods:<br><br>   * Use `indicator cards` to display the cumulative contribution of all activities during Q1 for `sales revenue`, `order volume`, `number of users who placed orders`, `proportion of new customers`, and `average transaction value`.<br><br>   * Use `line charts` to show the daily changes in `sales revenue` and `order volume` during Q1, highlighting the impact of activities on quarterly performance.<br><br>* Module summary: summarize the overall business scale achieved through activities in Q1, and describe the overall trend of the effectiveness of activities within the quarter (such as whether there are obvious peaks corresponding to key activity nodes). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e3334cbb4e642c883db1658d40c89aa~tplv-goo7wpa0wc-image.image) </span> |



* Store standardized analysis templates (such as industry report structures and research models).

* When a user initiates a report writing task, the system will **invoke all matched framework content** to ensure the output is systematically structured.


<span id="1f8cd076"></span>
### Template authoring

<span id="f9445174"></span>
#### Template structure requirements


|Template structure |Detailed requirements |
|---|---|
|Analysis objective |First, clarify the core problem to be solved or the goal to be achieved. It is necessary to clearly explain the analysis scenario, analysis role, and analysis objective in one or two sentences. This is usually described in the first part of the template. |
|Object of analysis |Refers to the key elements such as metrics and dimensions that need to be further analyzed to achieve the analysis objective. To ensure the accuracy and effectiveness of the analysis results, the following core information must be clearly defined when handling analysis tasks:<br><br><br>* **Metric definition**: For DataAgent, metric definition refers to the combination of [dataset] + [metric field] + [filter conditions];<br><br>   * When there are multiple datasets or datasets contain multiple metric fields with similar names, it is recommended to specify the dataset and metric field as much as possible;<br><br>   * Filter criteria often contain domain\-specific knowledge from the business domain (that is, specialized understanding or rules specific to the domain). This information must be explicitly provided; otherwise, it may lead to analytical bias.<br><br>* **Data extraction period**: The time range of the data is critical for interpreting analysis results. Different analytical methods may have different requirements for the period, which must be specified according to the specific needs, such as:<br><br>   * Trend analysis: It may be necessary to specify whether the period for trend analysis is the past 7 days, 30 days, 3 months, and so on;<br><br>   * Attribution analysis: It is necessary to specify the periods for the baseline and comparison, such as the past 7 days versus the previous week, or the past month versus the previous month, and so on.<br><br>* **Changes in analysis objects**: As the analysis progresses, the analysis objects may shift from the overall to the specific, or from the original analysis metrics to related metrics. It is important to note and specify changes in the analysis objects in the query. |
|Analytical methods |When there are clear analytical expectations, the specific analytical method to be used should be directly specified in the template. Common analytical methods include: descriptive statistics (calculation and comparison of proportions, medians, means, and other statistics), attribution, anomaly detection, forecasting, clustering, and more. |
|Output requirements |The quality of the output should focus on both content and form. Properly organizing insights and using appropriate data visualizations can make conclusions clearer and easier to understand. Therefore, requirements for both content and form need to be specified and clearly stated in the template.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Problem descriptions must be specific:</strong> Clearly describe the desired analysis in concise language, ensuring that the requirements are fully explained. For example: Analyze customer distribution by segmenting customers according to age and display the results using a pie chart.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Problems need to be refined</strong>: When the analysis task is relatively complex, it is recommended to break it down into several small steps and proceed gradually, with each step described in a single sentence rather than as a block of text. If there are dependencies between steps, this needs to be explained and emphasized.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Make good use of Markdown</strong>: Use <code>#</code> to indicate headings, <code>**bold**</code> for emphasis, and use blank lines, indentation, and bullet points to distinguish hierarchy, which helps the model understand the intent.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Emphasize when necessary</strong>: If the relevant field or result cannot be returned after multiple descriptions, you can write it again separately to emphasize.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Remind to use tools</strong>: Currently, tools such as online search, Python, and business knowledge base are supported. You can require the model to use these tools.</div><br> |


<span id="b2f3c92b"></span>
#### Template structure example

```Bash
# Analysis objectives
 Describe what you want to know in one sentence
# Data scope
Clearly identify which dataset/table to use and whether there are any restrictions (such as time/customer/product)
# Specified methods (if needed)
Are specific algorithms or tools used? Do you need to draw, predict, etc?
# Expected output
The conclusions, charts, attribution structures, etc. that you would like to see
# Role definition (if needed)
Not mandatory, but can enhance style consistency
```


<span id="76547ffd"></span>
## Knowledge example: analysis report

To generate a review analysis of last year's new product promotion campaign, upload sample knowledge of "2025 new product promotion campaign review analysis report.docx" to the agent. The agent will automatically extract the analysis framework from the sample report, learn its analysis requirements, and generate a new report.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f46d310be94763810f05883d0a71e2~tplv-goo7wpa0wc-image.image" name="2025 New Product Promotion Theme Activity Review and Analysis Report.docx">2025 New Product Promotion Theme Activity Review and Analysis Report.docx</Attachment>



|Sample input analysis report |Report content output by the agent |
|---|---|
|In\-depth analysis of new product promotion effectiveness<br><br><br>* **Analysis objective**: Evaluation of the effectiveness of the "New Product Early Access" campaign in driving sales of featured products and user acceptance.<br><br>* **Content and presentation**:<br><br>   * **Main promoted product performance**: A bar chart is used to display the top 10 promoted products by sales revenue, including product names and their respective categories. According to the results, the running shoes category performed exceptionally well, accounting for 6 out of the top 10 products. Among them, “Cushioning Series B” achieved the highest sales revenue, reaching 608,295.20 yuan.<br><br>* **Module summary**: The “New Product Early Purchase” campaign has achieved certain results in driving promoted product sales, with the running shoes category as the core promoted product, showing outstanding performance. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7429c011121047c89b1ba44174610d82~tplv-goo7wpa0wc-image.image) </span> |



* Store completed business analysis cases (such as market research, activity reviews, and more).

* When users need to refer to historical experience or methodologies, the system will **automatically extract the analysis framework section from the report** for structured recall, ensuring the output knowledge has complete logic.


<span id="a9523d18"></span>
# Special statement

(1) All content output by this service is generated by artificial intelligence models.

(2) Applicable users for this feature: limited to customers for internal use, own business, and use by the customer themselves. Customers must not provide generative artificial intelligence services to the public through data agents.

(3) This product supports both SaaS and on\-premises deployment versions. To purchase or request a trial, please contact the business staff for consultation.
