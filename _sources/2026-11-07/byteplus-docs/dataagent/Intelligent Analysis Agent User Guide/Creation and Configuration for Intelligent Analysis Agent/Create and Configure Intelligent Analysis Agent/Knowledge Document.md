---
title: "Knowledge Document"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Knowledge_Configuration"
---

Knowledge Documentation is the knowledge management feature of Intelligent Analysis Agent(SaaS version). Agent administrators can upload local files, precipitate business data into agent\-callable knowledge, and maintain knowledge\-enabled status in the list. Knowledge documents are divided into business knowledge, analysis templates, and analysis reports. And the three types of knowledge comparison are described below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Valid scope: Knowledge documents are currently only valid in <strong>deep research mode</strong> and are not applicable to intelligent questions.</div>



|Breakdown comparison |Business knowledge |Analysis template |Analysis Report |
|---|---|---|---|
|Knowledge content |Business background knowledge and definitions are essential to help models interpret data more accurately.<br><br>For example: metric criteria specification, event configuration, business process specification. |A standard analytical approach or procedure for a similar business problem to guide the model on how to disassemble the problem.<br><br>For example: order volume fluctuations → gradually analyze the reasons by channel, user type, and time distribution. |Completed business analysis results, including historical data, conclusions, and insights, for reuse and reference.<br><br>For example, last quarter's marketing impact analysis report. |
|Recall mechanism |Recall at chunk granularity to support efficient vector matching. |Full recall to ensure structural integrity, limit number of templates to 1. |Automatically extract the frame structure and align it logically when recalled. |
|Precautions |Business knowledge recommendations **are structured and chunked** to improve recall granularity and quality. |none |In the privatization scenario, the analysis report knowledge type is turned off by default. If you want to use it, you can contact the BytePlus technical support staff to turn on the function switch. |
|Knowledge example |See below:[ ](https://docs.volcengine.com/docs/86760/1874849#d6ab8376)[Knowledge Example: Business Knowledge](https://docs.byteplus.com/docs/dataagent/Knowledge_Configuration#79e7fc1b). |See below: [Knowledge Example: Analysis Templates](https://docs.byteplus.com/docs/dataagent/Knowledge_Configuration#0b20c2f4). |See below: [Knowledge Example: Analysis Report](https://docs.byteplus.com/docs/dataagent/Knowledge_Configuration#68a2fd7b). |


<span id="46a4fb1f"></span>
# Prerequisite


* Enter the target space and have the configuration permissions of the target agent.

* The local file is ready to be uploaded. The extension of the file to be uploaded belongs to the page support range: txt, md, doc, docx, ppt, pdf, xlsx, xls, csv.

* If the document contains image information that needs to participate in knowledge retrieval, evaluate in advance whether to enable image content analysis; the processing time will be extended accordingly after opening.


<span id="69f613c3"></span>
# Enter the knowledge document

Before configuring the agent's knowledge base, you first need to enter the knowledge document management page. This section will guide you to quickly locate the target agent and reach the knowledge document list for subsequent actions such as uploading, editing, or deleting documents. The following three steps can complete the entrance access.


1. On the Agent List page, locate the target agent from the list and click the **Agent Configuration** button to proceed to its configuration page.

2. In the left navigation bar, expand **Data and Knowledge** , and then click **Knowledge Documents** to go to the Knowledge Documents list page.

3. After entering the page, you can view the knowledge name, source file, knowledge classification, last update time, creator, update status, enabled status, and executable actions. The top of the page provides entry points for searching, adding knowledge, and refreshing lists.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35827586d86b41ef9c147026b8fb9f1b~tplv-goo7wpa0wc-image.image) </span>


<span id="41f37ae5"></span>
# Add knowledge

At the top of the knowledge document list, click the Add Knowledge button, and the system will open the Add Knowledge pop\-up window. According to the content of the pop\-up window, fill in the relevant add knowledge configuration items and confirm that the knowledge addition is completed. The following is the description of the relevant configuration items:


|Configuration item name |Description |
|---|---|
|**Source of knowledge** |Local file. |
|**Knowledge classification** |* **Automatic classification:**  The model automatically parses the knowledge content and classifies it, which is suitable for scenarios without manual classification.<br><br>* **Manual classification:**  The operator selects the knowledge classification by himself; after selection, please complete the configuration according to the fields appearing on the page.<br><br>   * **Business knowledge:**  applicable to business rules, index criteria, industry common sense and other business information;<br><br>   * **Analysis template:**  Standard analysis ideas or steps for similar business problems, used to guide the model on how to disassemble the problem (for example: order volume fluctuations → progressive analysis of causes by channel, user type, and time distribution)<br><br>   * **Analysis report:**  completed business analysis results, including historical data, conclusions and insights, for reuse and reference (example: last quarter marketing performance analysis report) |
|**Upload local file** |Click **Upload File** to select the file locally. The display supports txt, md, doc, docx, ppt, pdf, xlsx, xls, csv formats. |
|**Knowledge name** |Fill in the "Knowledge Name" text box with a name that is easy to search and identify. |
|**Image content analysis** |After opening, the uploaded picture can be automatically recognized as text, and the recognition result can be filled in "knowledge content". |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b31a59678194c9d997a6effbcc707e0~tplv-goo7wpa0wc-image.image) </span>

<span id="e258cd27"></span>
# Manage existing knowledge

The created knowledge is displayed in the knowledge document list, and the knowledge can be edited, enabled, disabled, deleted, and other operations.


1. **Search and browse**

   * Enter the knowledge name keyword in the search box at the top of the list to quickly locate the target knowledge.

   * When there are many knowledge items, use the paging control at the bottom of the page to switch the list page and browse all the content.

2. **Enable/disable state control**

   * In the row where the target knowledge is located, directly operate the "Enabled Status" switch:

      * Open: Knowledge can be used in the context of the current agent.

      * Closed: Knowledge is temporarily disabled, but records are preserved.

3. **Editing or deleting knowledge**

   * **Edit:**  Click the "Edit" button on the right side of the target row, modify the configuration according to the page field, return to the list after saving, and refresh to restore the updated status to "Available".

   * **Delete:**  Click the "Delete" button, confirm the operation after checking the name of the knowledge, and refresh the list to confirm that the knowledge has been removed. Attention: Knowledge cannot be restored after deletion, please proceed with caution.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When all operations are completed, refresh the list to ensure the page shows the latest changes.</div>


<span id="95254d05"></span>
# Reference: Knowledge Examples

<span id="79e7fc1b"></span>
## Knowledge Example: Business Knowledge

Upload the sample knowledge of "Consumer Behavior Analysis 5W2H Model.docx" to the agent. If the user asks "Use Consumer Behavior Analysis 5W2H Model to analyze consumer behavior this year", the agent will automatically identify and use the business knowledge to complete the generation of new reports.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e72b8217a33b45dd9bc6e72dfe1d8552~tplv-goo7wpa0wc-image.image" name="Consumer Behavior Analysis 5W2H Model.docx">Consumer Behavior Analysis 5W2H Model.docx</Attachment>



|Input of business knowledge content |Agent output report content |
|---|---|
|* **5W2H model:** <br><br>   * Who (audience persona): age, gender, region, income level, consumption preferences (such as maternal and infant populations concerned about safety certification);<br><br>   * What (consumer category): high\-frequency rigid demand products (grain and oil) vs low\-frequency durable goods (home appliances);<br><br>   * Why (consumer motivation): functional needs (e.g. mobile phone battery life) vs emotional needs (brand identity);<br><br>   * When (consumption time): seasonal (summer cold drinks), scene\-based (late\-night takeaway);<br><br>   * Where (consumption channel): online platform (Taobao/Douyin) vs offline scene (convenience store/shopping center);<br><br>   * How (consumption mode): impulsive consumption (live broadcast seckill) vs rational decision\-making (price comparison APP use);<br><br>   * How much (consumption amount): customer unit price, repurchase rate, LTV (user life cycle value). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b82684edfc68401190ab6fb4b9eb4e31~tplv-goo7wpa0wc-image.image) </span> |



* Store fragmented content such as rulebooks and scenario guides for daily use.

* The recall strategy of **initial screening → sorting → focusing** is adopted: 30 relevant text fragments are matched first, and only the 3 text fragments with the highest relevance are retained after AI sorting to avoid information dispersion.


<span id="0b20c2f4"></span>
## Knowledge Example: Analysis Templates

<span id="a62727c0"></span>
### Use template

Upload the sample knowledge of "Template for the Review and Analysis Report of All Activities in the First Quarter of This Year.pdf" to the agent. If the user asks "Make review and analysis report of all activities in the first quarter of this year", the agent will automatically generate a new report according to the overall report framework and analysis template requirements of the sample knowledge.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85a5030c79214190b290853e1ca26088~tplv-goo7wpa0wc-image.image" name="Template for the Review and Analysis Report of All Activities in the First Quarter of This Year.pdf">Template for the Review and Analysis Report of All Activities in the First Quarter of This Year.pdf</Attachment>



|Input analysis template requirements |Agent output report content |
|---|---|
|Q1 Overall contributions and trends<br><br><br>* Analysis Purpose: To provide an overview of the overall value and performance cadence generated by all activities in Quarter 1<br><br>* Specify the chart/presentation method:<br><br>   * Use the `metric card`to display the cumulative contribution of all activities during Q1 `sales`, `order volume`, `number of users placing orders`, `new customer ratio`, and `customer unit price`.<br><br>   * Use `line graphs`to show `daily`changes in `sales`and `order volumes`during Q1, reflecting the pull of activity on quarterly results.<br><br>* Module summary: Summarize the overall business scale achieved through activities in Q1, and describe the overall trend of activity effects during the quarter (such as whether there are obvious peaks corresponding to key activity nodes). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9448e017e2d4e0bb4a8b1637be9fba5~tplv-goo7wpa0wc-image.image) </span> |



* Store standardized analysis templates (e.g., industry report structures, research models).

* When the user initiates the report writing task, the system will **call the matching framework content in full** to ensure the systematization of the output content.


<span id="50e98696"></span>
### Template writing

<span id="58d6b0d4"></span>
#### Template structure requirements


|Template structure |Detailed requirements |
|---|---|
|Analysis target |The first step is to clarify what the core problem or goal you want to solve is. It is necessary to explain clearly the analysis scene, the analysis role, and the analysis purpose in one or two sentences. It is usually described in the first part of the template. |
|Analysis object |Refers to the key elements such as metrics and dimensions that need to be further analyzed in order to achieve the analysis objectives. In order to ensure the accuracy and validity of the analysis results, the following core information must be clearly defined when actually handling the analysis task:<br><br><br>* **Metric criteria:**  For DataAgent, the metric criteria points to the information combination of [dataset] + [metric field] + [filter condition];<br><br>   * When there are multiple datasets or datasets containing multiple metric fields with similar names, it is recommended to specify the datasets and metric fields used as much as possible.<br><br>   * Filtering criteria often contain "private domain knowledge" (i.e., domain\-specific professional understanding or rules) of the business domain, which needs to be clearly provided, otherwise it may lead to analytical bias.<br><br>* **Number cycle:**  The time frame of the data is crucial for the interpretation of the analysis results. Different analysis methods may have different requirements for the cycle, which need to be clarified according to specific needs, such as:<br><br>   * Trend analysis: It may be necessary to clarify whether the period of trend analysis is the last 7 days, 30 days, or 3 months.<br><br>   * Attribution analysis: It is necessary to clarify the period of the base period comparison period, whether it is the last 7 days vs last week, or the last month vs last month, etc.<br><br>* **Changes in the analysis object:**  As the analysis advances, the analysis object may advance from the whole to the part, or from the original analysis index to the relevant index, and the change of the analysis object needs to be paid attention to and clarified in the query. |
|Analytical method |When there is a clear analysis expectation, it is necessary to specify which analysis method to use directly in the template. Common analysis methods include descriptive statistics (proportion, median, mean and other statistics), attribution, anomaly detection, prediction, clustering, etc. |
|Output requirement |The quality of output requires both content and form. Arranging insights properly and using the right data lake visualization can make conclusions clearer and easier to understand. Therefore, it is necessary to clarify the requirements for content and form, and to clarify them in the template.<br><br>explain<br><br><br>* **The problem description should be specific:**  Describe the desired analysis in concise language, and be sure to make the requirements clear. For example, analyze the distribution of customers by age stratification, and display it using a pie chart.<br><br>* **Need to refine the problem:**  When the analysis task is more complex, it is recommended to split it into several small steps step by step, it is recommended that each step be a sentence, not written into a group. If each step is related, it needs to be explained and emphasized.<br><br>* **Make good use of Markdown:**  use `#`to indicate the title, `** bold **`to indicate emphasis, and use blank lines, indents, and bullets to distinguish the hierarchy, which is beneficial for the model to understand the intent.<br><br>* **Emphasize when necessary:**  When multiple descriptions fail to return the corresponding field or result, you can write it again separately for emphasis.<br><br>* **Reminder to use tools:**  Currently supports online search, Python, business knowledge base and other tools, you can use tools by requiring models. |


<span id="140508e4"></span>
#### Template structure example

```Bash
# Analysis target  
State what you want to know in one sentence.
# Data range  
Clearly identify which dataset/table to use and whether there are any restrictions (such as time/customer/product)
# Specify method (if necessary)  
Are specific algorithms or tools used? Do you need to draw, predict, etc?
# Output expectation  
The conclusions, charts, attribution structures, etc., that you would like to see
# Role setting (if needed) 
Optional, it can enhance style consistency
```


<span id="68a2fd7b"></span>
## Knowledge Example: Analysis Report

Upload the sample knowledge of "2025 New Product Promotion Theme Activity Review Analysis Report.docx" to the agent. If the user asks "Make a review analysis of last year's New Product Promotion Theme Activity", the agent will automatically extract the analysis template in the sample report, learn its analysis requirements, and complete the generation of a new report.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fd55796997349f1b857767f836a0e45~tplv-goo7wpa0wc-image.image" name="Analysis Report on the 2025 New Product Promotion Themed Campaign Review.docx">Analysis Report on the 2025 New Product Promotion Themed Campaign Review.docx</Attachment>



|Sample analysis report input |Agent output report content |
|---|---|
|In\-depth analysis of the effect of new product promotion<br><br><br>* **Purpose of analysis:**  To focus on evaluating the core performance of "New Product Early Purchase" activities in driving sales and user acceptance of key products.<br><br>* **Content and Presentation:** <br><br>   * **Main product performance:**  Use the bar chart to show the main product sales ranking TOP10 product names and categories. From the results, the running shoes category performed well, accounting for 6 of the TOP10 products, of which the sales of "cushioning series B" were the highest, reaching 608,295.20 yuan.<br><br>* **Module summary:**  The "New Product Rush" activity has achieved certain results in promoting the sales of the main products. The running shoes category is the core main product, and the performance is outstanding. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5ecb0dfe8c046c59d7ff1100c33c88a~tplv-goo7wpa0wc-image.image) </span> |



* Store completed business analysis cases (e.g. market research, activity reviews, etc.).

* When users need to refer to historical experience or methodology, the system will **automatically extract the analysis template part of the report** for structured recall to ensure that the output knowledge is complete and logical.


<span id="7759d35e"></span>
# Special Statement


1. The output of this service is generated by artificial intelligence models.

2. This function is applicable to the crowd: only for customers in\-house, own business, own use, customers are not allowed to provide generative artificial intelligence services to the public through DataAgent.

3. This product supports SaaS version and private deployment version products. If you need to buy or try it, please contact the business staff for consultation.
