---
title: "Intelligent Query Agent"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Query_Agent"
---

**The Intelligent Analysis Agent (hereinafter referred to as the Analysis Agent or the agent) is an expert advisor based on AI deep reasoning and big data analytics**. The Analysis Agent includes the Intelligent Query Agent and the Deep Research Agent. **The Intelligent Query Agent**, as a flexibly configurable intelligent query tool, enables users to query business data more accurately through simple conversations. It supports multi\-dataset queries, semantic model parsing, business knowledge invocation, question recommendation and bookmarking, multi\-turn interactive querying, as well as attribution analysis, fully meeting users' diverse data query needs.

<span id="a34eaccd"></span>
# Feature overview

The Intelligent Query Agent feature of **the Intelligent Analysis Agent** can accurately interpret user intent through natural language conversations, enabling collaborative queries across multiple datasets and in\-depth attribution analysis. Supplemented by personalized recommendations and multi\-turn interactions, it provides users with efficient, accurate, and unified data query services.

<span id="afc1cec0"></span>
## **Detailed features**


* **Recommended questions**: Frequently asked questions by most team members are pre\-configured in the agent, allowing other users to quickly query by clicking the question.

* **Bookmarked questions**: Users can bookmark their frequently asked questions for quick access in future queries.

* **Data query**: Freely query data within the agent through conversations, supporting multi\-turn interactions.

* **Attribution analysis**: The web\-based agent is equipped with attribution analysis capabilities, enabling quick data analysis while querying data.

* **Scheduled push**: Push questions to relevant users at user\-defined intervals.


<span id="eb8588f3"></span>
## **Application scenarios**


* **Business staff in enterprises who currently lack data analysis skills and statistical knowledge** can use the agent to lower the barriers to querying and understanding data.

* **Managers and business personnel in enterprises** may not be familiar with datasets or the underlying data processing logic. When performing data queries and business analysis, they hope to quickly access the data they need. The intelligent agent enables users to obtain answers simply by asking questions, without needing to select a dataset.

* **Data/technical teams in enterprises** can set the data that business users or managers regularly focus on as recommended questions for the intelligent agent. This allows users to quickly view data in IM (Lark) without opening the product.


<span id="e18c6b44"></span>
# Prerequisites


* Project creation and user authorization have been completed. For details, please refer to [Project Information](https://docs.byteplus.com/docs/dataagent/Project_Information) and [User Management](https://docs.byteplus.com/docs/dataagent/User_Management).

* Data preparation has been completed. For details, please refer to [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview).

* Intelligent agent configuration has been completed. For details, please refer to[Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures).


<span id="7ccf4c87"></span>
# Caution

Currently, the **Intelligent Query Agent** supports the following types of datasets:


* Supports extracted datasets

* Supports direct connection to ClickHouse/ByteHouse datasets

* Supports direct connection to Doris/selectdb/starrocks datasets

* Supports direct connection to Postgres/hologres/openguass

* Supports direct connection to mysql


<span id="893c9308"></span>
# Query data

The following describes how to access the Intelligent Analysis Agent to ask data query questions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When asking a question, the description must be clear. High\-quality questions are a key factor affecting data query results. It is recommended that the question description include information such as the metrics, dimensions, and time range to be queried, so that the intelligent agent can perform data queries based on the description. For more suggestions and examples about asking questions, please refer to <a href="https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions">Best Practices: Recommendations and Examples for Intelligent Data Query Questions</a>.</div>



1. After logging in to the BytePlus DataAgent\-Analysis Agent page with your account and password, select the published intelligent agent on the left side of the page to enter the conversation page and use the data query feature.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a9fdcf3510345ffaab31e1c5bd7db2e~tplv-goo7wpa0wc-image.image) </span>


2. After entering the intelligent agent conversation interface, click the switch button in the dialog box to toggle between the "Intelligent Query" and "In\-depth Research" features. The Intelligent Query Agent only provides the "Intelligent Query" feature.

3. Users can click the dialog box to select built\-in questions to ask questions, or directly enter questions to ask.

   
   |Natural language data query |Quickly view recommended questions |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1aed550a96c643bf958eb4fe0e48d68c~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The main usage of the intelligent agent allows users to directly describe their data query requirements in text. After receiving a response, users can click "Follow\-up" to continue interacting with the intelligent agent regarding related questions.<br><br>* The intelligent agent queries data without requiring users to select a dataset; it will automatically query data in the configured datasets. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5786cf597db94768b9f674127b7b23bb~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Recommended questions are provided below the dialog box. Users can click any recommended question to directly query data.<br><br>* Recommended questions are automatically generated based on users' historical queries and can also be customized. For specific configuration methods, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures). |
   


<span id="2742d7dd"></span>
# Query result analysis

<span id="c0c24df5"></span>
## Common chart analysis

You can select visualization chart display methods, including metric cards, line charts, bar charts, pie charts, combination charts, tables, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9133085d12a84f2aa43b91c47b810b89~tplv-goo7wpa0wc-image.image) </span>


|Chart types |Applicable scenarios |Trigger keywords |Example questions |Diagram |
|---|---|---|---|---|
|line (line chart) |Suitable for displaying data trends over time. |Trend, growth, decline, fluctuation, time series. |Display annual sales revenue changes, show user growth trends. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b073bb3f97340b6b60aa740c28efbf9~tplv-goo7wpa0wc-image.image) </span> |
|column_parallel (bar chart) |Suitable for comparing data across different categories. |Comparison, ranking, category, quantity. |Compare sales revenue by region, show product sales ranking. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc35c0edc8454ab39405d7ff7066e9f4~tplv-goo7wpa0wc-image.image) </span> |
|pie (pie chart) |Suitable for displaying the proportion of each part to the whole. |Proportion, share, distribution. |Show market share distribution, display user age proportions. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96ed3d56887045c3870d0fb289292124~tplv-goo7wpa0wc-image.image) </span> |
|measure_card (metric card) |Suitable for displaying a single key metric or value. |Which, key metric, value, summary. |Display current sales revenue, show total number of users. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ec4ddf969be408c89d8310eec3b1165~tplv-goo7wpa0wc-image.image) </span> |
|table (table) |Suitable for displaying detailed data and supports multidimensional viewing. |Details, multidimensional, list. |List sales data for each product and display detailed user information. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ba879031e1e45318389120b3eb56118~tplv-goo7wpa0wc-image.image) </span> |
|scatter (scatter plot) |Suitable for displaying correlations between fields, for use when there are two metrics, and for continuous data. |Impact, performance, correlation, distribution, grouping. |Display the impact of sales amount, and show the distribution of age and income. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76cb336de54d446a8092c099435c9f79~tplv-goo7wpa0wc-image.image) </span> |
|map (China map) |Suitable for displaying the distribution and differences of data among provinces in China. |Regional distribution, geographic differences, regional comparison, geographic trends, heatmap, marker points. |Display the distribution of sales amount by province. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bab65debfb74056ad9635062c6cda7d~tplv-goo7wpa0wc-image.image) </span> |
|double_axis (dual\-axis chart) |Suitable for displaying two sets of data with different units simultaneously. For use when there are two groups of chart fields. |Dual\-axis, different units, comparison. |Display sales amount and profit margin, show temperature and precipitation. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ff65e5b4e6543babc5546bde1d85284~tplv-goo7wpa0wc-image.image) </span> |
|combination (combination chart) |Suitable for displaying multiple groups of different types of data simultaneously or emphasizing relationships between data, applicable to complex scenarios. For use when there are two or more groups of chart fields. |Combination, complex, multidimensional. |Display trends and proportions of sales amount and profit. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b3f70fc1a2940178d02b5dde97f6a4a~tplv-goo7wpa0wc-image.image) </span> |


<span id="646748af"></span>
## Data interpretation


1. Click the "Data Interpretation" button in the upper right corner of the returned results. The Intelligent Analysis Agent will interpret the data based on the query results.

2. After interpretation is complete, the interpretation results will be returned to you. You can also click "View details" to view detailed data from the interpretation.


<span id="a75d2c89"></span>
## Anomaly detection


1. Click the "Anomaly detection" button in the upper right corner of the returned results. The intelligent analysis Agent will perform anomaly detection on the queried results.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9584ae3571be4f418c79cd103473026d~tplv-goo7wpa0wc-image.image) </span>


2. Once detection is complete, the detection results will be returned to you.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52ab0eed14d4c77bcce23ac79885cb6~tplv-goo7wpa0wc-image.image) </span>

<span id="453ecd98"></span>
## Attribution analysis

To analyze abnormal results found in conventional chart analysis, use attribution analysis to determine the cause of the anomalies. The intelligent agent can automatically perform time series analysis on the influencing factors of abnormal metrics, displaying the top three influencing factors with contributions in the same or opposite direction, their corresponding contribution values, contribution rates, comparison differences, and comparison percentages, enabling intelligent attribution analysis.


1. Click the "Attribution analysis" button in the upper right corner of the chart showing the query results. In the pop\-up window, the intelligent analysis Agent pre\-fills the attribution metric, dimension, and baseline/observation date for you. You can also manually adjust the relevant attribution parameters.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e91a561471c04a46a2a45e126e3f7d94~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Note |
|---|---|
|Attribution metric & attribution dimension |The agent will pre\-fill an attribution metric and attribution dimension for you based on the chart, and you can select a different one from the dropdown menu. |
|Reference date |Click to set the 'reference date' for attribution.<br><br><br>* The reference date is a specific date used as a standard for comparison, to measure and compare data changes relative to the observation date.<br><br>* The reference date must be earlier than the observation date. |
|Observation date |Click to set the 'observation date' for attribution.<br><br><br>* The observation date is the specific date for data collection and phenomenon observation.<br><br>* The observation date must not be earlier than the reference date. |



2. After attribution analysis is complete, the intelligent agent will provide the attribution results and display the top three influencing factors with contributions in the same or opposite direction, along with their corresponding contribution values, contribution rates, comparison differences, and comparison percentages.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/408a35d6e58f439498a6abb1535d7600~tplv-goo7wpa0wc-image.image) </span>


* Top 3 contributors in the same direction: Influencing factors that drive the metric change in the same direction, ranked in the top three by contribution.

* Top 3 contributors in the opposite direction: Influencing factors that drive the metric change in the opposite direction, ranked in the top three by contribution.

* For the algorithm of contribution value and contribution rate, refer to: [Dimension attribution - algorithm](https://www.volcengine.com/docs/4726/1217644).


<span id="7594583f"></span>
## View analysis process

You can choose whether to view the reasoning process, analysis parameters, and other content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e20a7f7dc6d641319af54d44bbdb587b~tplv-goo7wpa0wc-image.image) </span>

<span id="33d92093"></span>
## AI follow\-up questions


|Trigger scenarios |Operation entry and effect |
|---|---|
|When your agent is configured with decomposition questions for recommended questions, and the user's query description matches a configured question during data queries.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed373dffba644391bfe0f46091f3b848~tplv-goo7wpa0wc-image.image) </span><br><br>For detailed configuration operations, see [Content Configuration](https://docs.byteplus.com/docs/dataagent/Content_Configuration). |1. When a question matches a recommended question, the agent will break down the question into the configured sub\-questions and perform query analysis for each; you can click "AI Follow\-up" in the lower left corner of each sub\-question result to further follow up on the corresponding query result.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49d12e9c5d1e43429be165982beae52e~tplv-goo7wpa0wc-image.image) </span><br><br><br>2. The result of a follow\-up question will be further analyzed based on your original follow\-up question. |


<span id="b2cc263e"></span>
# Other operations

<span id="84081749"></span>
## Reset conversation

When using the agent, the agent will automatically use historical conversation data as reference input information for intelligent queries. If you do not need to refer to historical conversation records during interaction with the agent, click "Reset conversation" before asking your question again. Subsequent new conversations will no longer be associated with the above historical conversation content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3948296e0d7e4551a04316187090813c~tplv-goo7wpa0wc-image.image) </span>

<span id="9f86044f"></span>
## View conversation records & start a new conversation


* Users can view and delete historical Q&A in recent conversations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/744cdf0ea46c450b9a0d327fcb1da902~tplv-goo7wpa0wc-image.image) </span>


* Users can create a new conversation window.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de91ce2af04448ed92d79efe45ad2ac5~tplv-goo7wpa0wc-image.image) </span>

<span id="15b72f82"></span>
## Download & save questions

The agent allows users to download and save previously asked questions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35639ba7b13146ffa0f4b5787446a23e~tplv-goo7wpa0wc-image.image) </span>


* Download: Currently, query results can be downloaded in xlsx and 飞书 spreadsheet formats.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To download as a Lark spreadsheet, you must first complete the integration configuration on the Lark side.   </div>
   

* Save: Saved questions will be displayed on the agent conversation home page, so when asking the same question later, there is no need to enter it manually again.


<span id="58b8d25b"></span>
## Scheduled push

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The scheduled push feature is only available for Lark\-side agents; please use it in the Lark\-side agent.</div>


The Lark agent supports scheduled push settings, allowing users to configure routine pushes for the agent, such as automatically pushing data users want to see at a scheduled time each day.

<span id="5e25112d"></span>
# Best practices for optimizing query results

When data query results are inaccurate, unstable, or have other quality issues, optimization can be considered from three aspects: the quality of the original dataset, agent configuration, and the quality of the question description.

When optimizing the agent, the recommended priority is: dataset quality (dataset governance) \> dataset\-semantic model definition \> dataset\-knowledge base configuration \> question accuracy. In other words, give priority to optimizing the quality of datasets involved in business scenarios, then optimize the agent's knowledge configuration, and finally optimize based on the configuration or description of the question.


* [Best Practices: Recommendations and Examples for Intelligent Data Query Questions](https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions).


<span id="35071019"></span>
# Special statement

(1) All content output by this service is generated by artificial intelligence models.

(2) Intended users of this feature: Only for customers' internal use, proprietary business, and their own use. Customers must not provide generative artificial intelligence services to the public through the data agent.

(3) This product supports both SaaS and private deployment versions. To purchase or request a trial, please contact a sales representative for consultation.
