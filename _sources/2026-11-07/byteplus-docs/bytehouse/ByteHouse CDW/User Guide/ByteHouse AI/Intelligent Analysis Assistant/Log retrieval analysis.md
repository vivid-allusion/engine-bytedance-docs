---
title: "Log retrieval analysis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/log-retrieval-analysis"
---

ByteHouse provides log search and analysis functionality, which is similar to the Discover feature in Kibana and offers users the ability to visually analyze log data. The ByteHouse log retrieval and analysis feature supports integration with intelligent assistants and knowledge bases, enabling more efficient identification and analysis of error logs as well as the generation of intelligent analysis recommendations. This feature is suitable for scenarios such as log search and filtering, interactive data exploration, contextual correlation analysis, performance bottleneck identification, and root cause analysis of failures. This article explains how to configure and use the log exploration and analysis feature.

<span id="151adb6e"></span>
# Prerequisites


* Before using the search analysis feature, please enable the full\-text search feature for the virtual warehouse you want to use. For details, refer to [Edit Virtual Warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#48dec0d3).

* Log data has been imported. For operational details, please see [Data Import documents](https://docs.byteplus.com/en/docs/bytehouse/docs-data-import-e8caa19b).

* Please ensure that your log data table has an inverted index set up and includes a Date or DateTime data column.


<span id="88dd0595"></span>
# Usage restrictions

This feature is in Beta. To use it, please submit a ticket or contact the ByteHouse team to request whitelist access.

<span id="6682b027"></span>
# Overview of functions

As a general\-purpose data analytics platform, ByteHouse offers high query performance, low cost, a user\-friendly interface, and full\-text search capabilities, providing systematic support for log search and analysis scenarios. Currently, ByteHouse provides log data ingestion, query, and analysis capabilities, allowing users to visually search and analyze log data. It supports querying log data within specified time ranges and conditions using full\-text search or SQL queries, intuitively presenting trends in the distribution of system anomalies to help users quickly locate issues and improve the efficiency of issue identification and analysis.

At the same time, you can also leverage the AI log insight capabilities of the ByteHouse intelligent assistant to generate SQL queries and log insights using natural language. This enables intelligent log analysis scenarios such as error log identification and analysis, error log correlation and root cause analysis, and repair solution suggestions. These features help you focus on analyzing the root causes of errors and automatically generate repair suggestions, improving the efficiency of troubleshooting and issue resolution.

ByteHouse also supports associating your dedicated [Knowledge base](https://docs.byteplus.com/docs/bytehouse/knowledge-base) when using the intelligent assistant for AI log retrieval. By leveraging the business and industry knowledge you upload, it can analyze log details more accurately, intelligently classify large volumes of logs by fault type, detect abnormal patterns in the logs, and automatically generate repair suggestions based on the content of your knowledge base.

<span id="d5ef8ac5"></span>
# Use log retrieval analysis

<span id="5f03d9f9"></span>
## Step 1: Add and select analysis objects and virtual warehouse


1. Log in to the ByteHouse console, click the \*\*SQL worksheet \*\*tab at the top, and then click the **Log retrieval analysis** icon to access the feature page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee3b023dcb614156a31c3bab41e6ee67~tplv-goo7wpa0wc-image.image) </span>

2. Add data tables as analysis objects. Click the dropdown button for the data table. Click **Table Configuration**. In the pop\-up window, filter and add the databases, data tables, and timestamps to be analyzed. Then click **Save**. Data tables added successfully will be displayed in the dropdown list. You can add multiple tables at once. You can click the **plus sign** to continue adding.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/071db27257a243668aee2425f826a8e2~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, only data tables configured with "inverted index" and "Date/DateTime" columns are supported.   </div>
   

3. Select the object to retrieve and analyze. Click the **Table** dropdown button. Select the target data table from the list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6973848f26f84be9a67e2735747d1b83~tplv-goo7wpa0wc-image.image) </span>

4. Click the virtual warehouse dropdown button and select an available virtual warehouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0bb631fd62e4c9bbcf88fa277134afb~tplv-goo7wpa0wc-image.image) </span>

5. Once the selection is complete, the system will automatically redirect to the search analysis page for the current table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a19a077a5c4d4d868315671a43df0e4f~tplv-goo7wpa0wc-image.image) </span>


<span id="d3dcc181"></span>
## Step 2: Retrieve and analyze

<span id="85b6e9ce"></span>
### Method 1: Use the intelligent assistant and knowledge base to enhance retrieval and analysis

The ByteHouse log exploration and analysis feature can be used in conjunction with the SQL statement generation and log insight features of [Intelligent assistant](https://docs.byteplus.com/docs/bytehouse/intelligent-assistant). You can use the intelligent assistant to generate SQL statements from natural language instructions and view the corresponding logs. When using the intelligent assistant for log insights, ByteHouse allows you to select a knowledge base you have created and, by leveraging your uploaded business and industry knowledge, provides more accurate problem analysis, diagnosis, and recommendations.

**Preparations**:

For better log analysis, it is recommended that you create [Knowledge base](https://docs.byteplus.com/docs/bytehouse/knowledge-base). The intelligent assistant will leverage your knowledge base to enhance retrieval and provide more accurate log analysis.

**Steps**:


1. On the Log retrieval analysis page, click **Intelligent assistant** to open the dialog box.

2. Click the first icon in the lower left corner of the input box, select **Generating SQL Statements**, enter a natural language command, and click the **Send** button. The intelligent assistant will automatically generate the corresponding SQL query statement. You can click **Inquire**, and the system will retrieve and display the corresponding log details for you.

   The following example queries logs that are within a specified time period and contain specified keywords:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00d400d2a76b43f2ac1d03ac1ed8a4e8~tplv-goo7wpa0wc-image.image) </span>

3. After generating log search results, you can use the intelligent assistant’s **log insight** feature and your knowledge base to assist in analyzing log details.

   1. Click the **Knowledge base** button in the Intelligent Assistant input box, and select the required knowledge base.

   2. Click **Log Insight** on the right side of the data details. The system will automatically switch to the intelligent assistant's log insight feature and generate an insight command, automatically analyze the current search results, identify potential issues, and provide optimization suggestions. You can optimize as needed.

      If you need a more detailed analysis, you can also continue entering insight commands in the input box, and the intelligent assistant will continue analyzing them for you.


<span id="4e63c9f9"></span>
### Method 2: Manual retrieval and analysis

ByteHouse also allows you to manually set search criteria and generate corresponding log search results.

**Steps**:


1. In the text box on the retrieval analysis page, enter the search term\*\*.\*\*

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94ed462438f3403a9f760bc66cc6b4d6~tplv-goo7wpa0wc-image.image) </span>

   ByteHouse currently supports two search methods: full\-text search and SQL query.

   * **Full\-text search**: The default search method; only columns with an inverted index configured can be searched. Please enter the content to search for in the text box. If no content is entered, all data will be searched.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9005c76107f4699abc355e6dd27e5bb~tplv-goo7wpa0wc-image.image) </span>

   * **SQL query**: Click the button next to the full\-text search box to switch to SQL query, then enter the SQL query command. For example, the following figure shows the result of querying for data in the log column that contains "down". The command used is `log LIKE '%down%'`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09d63137b1fb495cb5a30f8c7901c690~tplv-goo7wpa0wc-image.image) </span>

2. Set the **time range** for retrieval to **Relative Time** or **Fixed Time**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d232279c4d7c48acb3df42ff2db2bda1~tplv-goo7wpa0wc-image.image) </span>

   * Relative time: Refers to a time range based on the current time, for example, the past hour, the past day, and so on.

   * Fixed time: Refers to the fixed time range you set, such as 2025\-01\-01 00:00:00 to 2025\-01\-02 00:00:00.

3. (Optional) For full\-text search, you can set filter criteria. Click the **Filter** button, select column fields, and set the corresponding filter criteria. After performing a query, you can also click **Filter** the button to continue adding filter conditions based on the query results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60aba98186594baaa8395afa039bc82e~tplv-goo7wpa0wc-image.image) </span>

4. Click **Search**, and the system will automatically retrieve data that meets the criteria, display statistical charts and data details. You can further analyze the data based on log details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca36a502cec4c369201d75d77f92ec3~tplv-goo7wpa0wc-image.image) </span>

   By default, data details display index fields. To view other fields in the data details, go to the optional fields module and click the  **+**  **plus sign** next to the field to add the fields you want to display. To remove, click the  **\-minus sign** to remove the corresponding field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1f44aae21c24f549cf0b800c1360ec2~tplv-goo7wpa0wc-image.image) </span>

   If, after clicking **Search**, the interface indicates that no search results were found, you can try the following actions and then perform the query again.

   * Adjust to a larger time range.

   * Confirm that the search fields are correct;

   * Modify filter criteria.


<span id="c9b4048a"></span>
# Optional operations: Open multiple search analysis pages

ByteHouse supports opening up to 10 retrieval and analysis pages at the same time, allowing you to perform log search and analysis for different targets on each page.

**Steps**:


1. Open a new search page. You can enable: using any of the following methods

   
   |Method |Paths |
   |---|---|
   |Method 1 |Click **New Analysis**, click **OK**, and a new search analysis page is added.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2aff4eef3cd648baa9d4c1430b5094fb~tplv-goo7wpa0wc-image.image) </span> |
   |Method 2 |Click the  **+ plus sign** next to the tab to add a new search analysis page. |
   

2. Select an analysis object and a calculation group from the respective dropdown lists, then start query analysis. For details about the operation, see [Step 2: Retrieve and analyze](https://docs.byteplus.com/docs/bytehouse/log-retrieval-analysis#d3dcc181).
