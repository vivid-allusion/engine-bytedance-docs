---
title: "Advanced Guide for Business Users"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Advanced_Guide_for_Business_Users"
---

<span id="0cf2985f"></span>
## **Preface**

In the "Beginner's guide for business users", we have already learned about the main modules of Intelligent Data Insight and their relationships. Next, we will continue to explore some advanced features to help everyone use it more effectively.

<span id="76e8311b"></span>
## **1. Visualization queries**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Visual query is an important step in turning data into decisions. Users can conduct self\-service visual analysis based on connected data. Users do not need to know SQL syntax; by clicking or dragging, they can generate visual charts and gain data insights.</div>


<span id="3e664be6"></span>
### 1.1 Field configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the Visual Query module of Intelligent Data Insight, <strong>fields are categorized as either "dimension" or "metric"</strong>.\*\*\*\* Text or time data is recognized by default as dimension fields, and numerical data is recognized by default as metric fields. In actual use, dimension and metric fields can also be converted to each other.</div>


<div data-tips="true" data-tips-type="tip">A field is a concept used to describe and store data. After selecting the dimensions and metric fields to query, users can click on a specific field for further configuration. Intelligent Data Insights provides a wide range of field configuration options. For example, you can modify the display name for all fields; set the date type for date fields; change the aggregation method for metric fields; and adjust the data format for numeric fields, and so on.</div>


<span id="09ff04f2"></span>
#### 1.1.1 Add fields \- How to use existing fields to create new fields


* Most field requirements for datasets can be addressed by colleagues from the data warehouse team. However, if you only need a temporary field for your own analysis, you can also try creating a field yourself. Creating a field requires using expressions, which may be challenging for those unfamiliar with SQL. If you have time, you can read this document: [Add or Modify Fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a29e35fa8e643c8b20ece9544503f42~tplv-goo7wpa0wc-image.image) </span>


<span id="d7215ee3"></span>
#### 1.1.2 [Parameter Management](https://docs.byteplus.com/docs/DataWind/109997) \- Define a value that can be modified arbitrarily for expression calculation


* A parameter is a variable that can be flexibly adjusted. This variable can be used in calculated fields to implement dynamic logic for a single calculated field or even an entire chart. When the parameter takes different values, the field expression will correspond to different calculation logic.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7265415e5ee4e96a4a054690f193daa~tplv-goo7wpa0wc-image.image) </span>

<span id="2302db14"></span>
### 1.2 Chart configuration

<span id="60ba85d5"></span>
#### 1.2.1 [Configure Field Grouping](https://docs.byteplus.com/docs/undefined/69c3469a50cba904c1f57b41) \- Group metrics in a chart


* For dimension fields, when there is a large amount of information that can be displayed in groups, you can create groups to enable collapsed display of information.

* For numeric metric fields, creating groups allows you to use the values of expression fields to group data into bins, forming a new field.


**Common application scenarios:** 


* Merging dimension items of text fields: For example, divide the values in the "Country" field into "Europe", "Asia", and so on, generate a new group field "Continent", and then use "Continent" as a dimension for analysis.

* Custom data buckets: For example, segment the sales price into buckets such as 0\-100, 100\-300, and 300\-500, and analyze the performance of data within each range.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b678869036604bf39113c660814c553f~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="3146eed9"></span>
#### 1.2.2 [Dynamic Dimensions and Dynamic Metrics](https://docs.byteplus.com/docs/DataWind/Dynamic_Dimensions_and_Dynamic_Metrics)  **\- Quickly switch dimensions and metrics in a chart**


* Add dynamic dimension/dynamic metric functionality, enabling faster and simpler switching between multiple dimensions or metrics to meet the needs of different users for various dimensions or metrics.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6058b0a76ce40869787cfbaa2b82ec7~tplv-goo7wpa0wc-image.image) </span>

<span id="83904bc7"></span>
#### 1.2.3 [Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down)  **\- Drill down to other dimensions for analysis without modifying the chart**


* Drill up and drill down refers to creating a hierarchical structure based on fields (for example: province \-\> city \-\> channel), allowing users to quickly drill up or down between levels during visual analysis by clicking.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1d5d62462a1469cb9161fc4b72fa0cc~tplv-goo7wpa0wc-image.image) </span>

<span id="2c28e2bc"></span>
#### 1.2.4 **Conditional formatting \- Add single color, icon set, color scale, and data bars to charts**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb7a4e4c23e44c00864c24513f2888d9~tplv-goo7wpa0wc-image.image) </span>

<span id="109acaef"></span>
#### 1.2.5 **Template link \- Insert dimension values into links for web page navigation**

<span id="bb4a0a97"></span>
#### 1.2.6 [Data Annotation](https://docs.byteplus.com/docs/DataWind/Data_Annotation) \- Add text annotations to charts


* The visual query module provides the data annotation feature, which supports annotating a specific data point or time period in a chart.

* **Application scenarios**: When a data point or time period is abnormal for a specific reason, users can add a data annotation at the corresponding position to inform other users of the cause of the data anomaly. This reduces the need for oral or written explanations and improves readability and communication effectiveness.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f841b4e28556484db8b2d09ffbccf93c~tplv-goo7wpa0wc-image.image) </span>

<span id="615d098b"></span>
### 1.3 Filter configuration

<span id="ff3cae5d"></span>
#### 1.3.1 [Combination Filter](https://docs.byteplus.com/docs/DataWind/Combination_Filter)  **\- Perform complex AND/OR conditional filtering**


* The product supports multi\-level OR/AND filtering, enabling filtering under complex conditions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc784b0b75b4009b51f03388c809304~tplv-goo7wpa0wc-image.image) </span>

<span id="74d3a3d3"></span>
#### 1.3.2 [Subquery](https://docs.byteplus.com/docs/DataWind/Dimension_Filtering#9c6b3821) \- Use the query results of other charts as filter options for the current query


* Dimension filtering supports the subquery feature, allowing users to use the query results of other charts as filter options for the current chart.

* **Caution**:


Charts with the following conditions cannot be used as subquery charts:


1. Cannot reference itself

2. Subquery charts included must also have read or higher permissions for the corresponding dataset

3. Cannot contain dynamic dimensions/metrics

4. Cannot use associated datasets

5. Cannot have parameter\-bound fields


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0b3d3dfe24e4a1e9893d2a8092877d2~tplv-goo7wpa0wc-image.image) </span>

<span id="83bf90f8"></span>
#### 1.3.3 [Set sub-filter](https://docs.byteplus.com/docs/DataWind/Dimension_Filtering#_3-8-%E8%AE%BE%E7%BD%AE%E5%AD%90%E7%AD%9B%E9%80%89%E5%99%A8)\- Enable filter cascading


* **Application scenario**: When fields with hierarchical structures are used as filters, the filter options need to display relevant values. To prevent users from selecting distracting items. For example: province, city; primary category, secondary category.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/338de11fca124b79893b6f6b49e4d204~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="cb15bb1e"></span>
#### 1.3.4 Chart option configuration \- Control which enumerated values can be selected in filters

<span id="21424458"></span>
### 1.4 Analysis features

<span id="9cf0d797"></span>
#### 1.4.1 **Analysis features \- sorting, filtering Top N values, aggregation, percentage calculation, comparison calculation, period\-over\-period calculation, reference lines, table calculation**


* Smart Data Insight provides detailed written instructions for each analysis feature. For reference, see Analysis Configuration.


<span id="ff80bd58"></span>
### 1.5 Other

<span id="f2a2656b"></span>
#### 1.5.1 Chart monitoring \- **Detect data in charts and trigger alerts**


* Smart Data Insight supports the monitoring and alerting feature, allowing configuration of metric fluctuation monitoring and dimension enumerated value change monitoring.


<span id="6da741ab"></span>
## 2. Dashboard

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A dashboard is a collection of data charts and related components created during the visual query process. By arranging multiple components, you can present data stories for a specific business topic. You can also refer to this as a data analysis page, data analysis dashboard, and more.</div>


<span id="a7573902"></span>
### 2.1 Dashboard configuration

<span id="1e5d289d"></span>
#### 2.1.1 **Dashboard themes/templates/assets \- How to create more visually appealing dashboards**


* If you do not want to spend time adjusting various color schemes, fonts, or lines, you can try the [Dashboard Theme](https://docs.byteplus.com/docs/DataWind/Dashboard_Theme) feature of Smart Data Insight, which supports using our official themes or customizing themes according to business line design requirements.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0119a08ec59749be88555d21475949da~tplv-goo7wpa0wc-image.image) </span>


* You can also use the dashboard template feature of Smart Data Insight to directly replace charts with existing templates.

* Recently, the assets feature of Smart Data Insight has also been launched, enabling users to quickly add header images, title images, and dividers to dashboards. See [Operations in the Left Widget Area of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Left_Widget_Area_of_the_Dashboard).


<span id="20126f62"></span>
#### 2.1.2 [Multilingual](https://docs.byteplus.com/docs/DataWind/Multilingual) \- Set different language displays for Chinese and English environments


* In the project center, administrators can configure multilingual settings for datasets, charts, and dashboards separately, allowing colleagues working in multiple languages to intuitively understand relevant information.


<span id="d600e631"></span>
### 2.2 Chart interaction

<span id="94a643d5"></span>
#### 2.2.1 [Chart Linkage](https://docs.byteplus.com/docs/DataWind/Chart_Linkage)  **\- Linked analysis between charts**


* The chart linkage feature allows you to use a chart as a filter. By clicking on a data item within the chart, the associated charts will filter and display the data content corresponding to the selected item, providing a fast and intuitive experience.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a999346667e241f1a6699c2d5f1adf53~tplv-goo7wpa0wc-image.image" width="2874px" /></div>


<span id="7f77b22a"></span>
#### 2.2.2 [Chart Redirect](https://docs.byteplus.com/docs/DataWind/Chart_Redirect)  **\- Click a chart field to jump to another dashboard**


* This feature enables users to click a chart field and jump to another dashboard or webpage. When jumping, you can pass the current chart's data to the **global filter of the target dashboard**, or to the **specified location in the corresponding webpage link.** 


<span id="3723a30b"></span>
#### 2.2.3 Navigation anchor \- Quickly locate a specific chart


* The dashboard supports setting anchor points, allowing each chart to have its own anchor. Once set, the anchors will be displayed on the right side of the dashboard viewing page, making it easier to quickly locate a chart when there are many on the dashboard. See [Operations in the Right-Side Page Configuration Area of the dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Right-Side_Page_Configuration_Area_of_the_dashboard).


<span id="93321f5a"></span>
#### 2.2.4 Chart dataset replacement \- **Quickly switch the underlying dataset of a chart**


* Intelligent Data Insight supports the chart dataset replacement feature, allowing you to replace the underlying dataset of a single chart or the datasets used by all charts in the dashboard.


<span id="107f3cdc"></span>
### 2.3 Dashboard applications

<span id="f91f7d91"></span>
#### 2.3.1 [Bookmark](https://docs.byteplus.com/docs/DataWind/Dashboard_Viewing_Operations#_2-2-1-%E4%B9%A6%E7%AD%BE)\- Save the current dashboard filter configuration as a bookmark


* **Usage scenarios**: Users can save frequently used filter conditions as bookmarks for quick access. It also supports publicly displaying commonly used filter criteria within a department for all project users.


<span id="fa2c1134"></span>
#### 2.3.2 Subscribe to dashboard \- **Schedule dashboard content to be pushed to individuals or group chats**


* You can use the subscription feature of Intelligent Data Insight to push dashboard content as screenshots to individuals or to Feishu group chats. Configuration documentation: [Subscribe to dashboard](https://www.volcengine.com/docs/6470/1164059).

* The subscription feature can be used in conjunction with bookmarks, enabling users to push dashboard content based on different filter conditions.


<span id="c825e4bb"></span>
#### 2.3.3 Dashboard/chart embedding \- Embed dashboards or charts into documents or data portals


* This can be achieved through the dashboard and chart embedding feature.



|[Dashboard embedding](https://www.volcengine.com/docs/4726/111475)<br><br>> Dashboards support embedding the entire dashboard or individual charts into other platforms, such as Feishu Docs and more. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6949fe563a774532bfb71fe10b49b46e~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|**Chart embedding** | |


<span id="f5f8fe77"></span>
## 3. Datasets

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A dataset is the foundation for storing and managing data in Intelligent Data Insights, and also serves as the basis for visual queries and analysis. In simple terms, you can think of it as a type of data table. Users need to create datasets from the source tables to be analyzed before proceeding with subsequent modeling, visual chart creation, dashboard creation, and other tasks. In the dataset module, you can create, edit, query, and manage datasets.</div>


<span id="502b219f"></span>
### 3.1 **Public data \- Add Chinese calendar, public opinion data, weather data, and more to datasets**


* Intelligent Data Insights provides public data such as the Chinese calendar, public opinion data, weather data, and more, which can be combined with data in datasets to facilitate analysis.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57f02ae708bc499eaff450b07e8ea4bf~tplv-goo7wpa0wc-image.image) </span>

<span id="b5d42004"></span>
### 3.2 [Synchronization Settings](https://docs.byteplus.com/docs/DataWind/110023)  **\- Synchronize partitions for the current day and also backfill partitions for the past N days**


* Intelligent Data Insights datasets support the synchronize multiple days feature. Synchronizing multiple days means that when synchronizing a specific partition, the partitions for the previous N days will also be synchronized at the same time.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fcb834b8444412bb70b73e899733855~tplv-goo7wpa0wc-image.image) </span>

<span id="c05e3fbd"></span>
### 3.3 Mirrored datasets \- **Enable cross\-project use of datasets**


* Dataset producers can use the mirrored dataset feature to allow multiple projects to use the same dataset (same data source, data model, dimensions, and metrics) for creating charts and dashboards through simple configuration, saving storage resources and reducing operational costs.

* **Common application scenarios:**  The same dataset needs to be reused across multiple business lines, but unified data management and operations standards are required.

* Datasets support cross\-project use, but dataset management permissions are required for configuration. It is possible to make the current project's dataset available to multiple projects without occupying new storage space. The datasets in these projects will remain consistent with the original dataset. For configuration, refer to the documentation: [Mirror Dataset](https://docs.byteplus.com/docs/DataWind/110002).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04f3db36361b4d068cd8766b28450825~tplv-goo7wpa0wc-image.image) </span>

<span id="c3e13c9b"></span>
### 3.4 Related datasets \- Enable direct join queries across multiple datasets


* Intelligent Data Insights supports the [Joined Datasets](https://docs.byteplus.com/docs/DataWind/109996) features, allowing **multiple datasets within the same cluster** to be related.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e86e32405ae44425b861c64fb03431fe~tplv-goo7wpa0wc-image.image) </span>

<span id="4cf6cfc7"></span>
## 4. SQL queries

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using the on\-premises version, Intelligent Data Insights supports temporary SQL queries. Currently, querying internal company data sources such as Hive, ClickHouse, MySQL, and Doris is supported. Query results can be downloaded or imported into the visual query page for analysis. Queries can be saved to folders or the template library for other team members to use.</div>


<span id="f270a8ff"></span>
### 4.1 Save charts \- Save SQL query results to visual queries


* SQL query results can be saved to visual queries, allowing further data analysis through visual queries.


<span id="dca7a8c7"></span>
### 4.2 **Upload a temporary table \- Upload a local file as an online Hive table**


* SQL queries support uploading local CSV files as temporary Hive tables for query participation.


<span id="53230550"></span>
## 5. Attribution decision\-making

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The attribution decision feature of Intelligent Data Insights (on\-premises version) offers automated data attribution and intelligent reporting capabilities. Designed to enhance the efficiency and intelligence of in\-depth business analysis, it can automatically explore metrics based on attribution configurations created by producers, quickly identify abnormal fluctuations, break down the main contributing factors to metric fluctuations, assist business users in completing data attribution analysis, and rapidly gain data insights.</div>


<span id="1dbc57a7"></span>
### 5.1 **Anomaly analysis**


* Anomaly analysis is used to detect abnormal fluctuations in core metrics. Based on user configuration, the system automatically inspects metrics daily or weekly, using intelligent algorithms or configured rules to detect abnormal fluctuations, send alert notifications, and enable further drill\-down by dimension to investigate anomalies in greater depth.

> **Applicable scenarios**:

> Core business metrics fluctuate every day. How can one determine whether yesterday's fluctuation was abnormal?

> If an anomaly occurs in a metric and an alert is needed, but simply relying on a week\-over\-week threshold does not account for the metric's own trends and seasonality, what is a reasonable way to determine anomalies?

> While the overall dashboard metrics may appear stable, could there be hidden anomalies beneath the surface (by drilling down into various dimensions)?


**For information on using the anomaly analysis report, see** [Attribution Report - Anomaly Analysis](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f626bf).

<span id="8c9e1692"></span>
### 5.2 **Dimension attribution**


* Dimension attribution is used to break down metric changes across different dimensions and provide quantitative explanations of each dimension's contribution. Based on user configuration, the system automatically inspects metrics daily or weekly, using scientific attribution algorithms to analyze the factors influencing the overall dashboard metrics.

> Applicable scenarios:

> For example, when performing DAU change attribution, which business sources, scenarios, or cities contributed to the DAU change, and how much did each factor contribute? Business source, scenario, and city are all different dimensions.


**For information on using the dimension attribution report, see** [Attribution Report - Dimension Attribution](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f626c1).

<span id="2e06bac1"></span>
### 5.3 **Metric attribution**


* Metric attribution is used to explore the impact of multiple related metrics on changes in core metrics, including the contribution of multiplicative factors and the contribution of each factor in non\-multiplicative formula relationships. Based on user configuration, the system automatically analyzes the degree to which relevant metrics affect core metrics on a daily or weekly basis.

> Applicable scenarios:

> With sales revenue as the core metric, user coupon redemption, merchant livestreaming, user livestream viewing, and product clicks each contribute to changes in sales revenue to varying degrees.


**For information on using the metric attribution report, see** [Attribution Report - Metric Attribution](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f626c3).

<span id="e391802b"></span>
### 5.4 **Metric analysis tree**


* The three analysis features introduced earlier are independent. However, actual business scenarios can be more complex, and a single analysis scenario may not be sufficient. For example, users may need to attribute multiple dimensional metrics simultaneously or chain multiple attribution capabilities. In such cases, users can try the metric analysis tree.

* The metric analysis tree atomizes attribution capabilities into individual nodes. Users can organize and chain different types of nodes based on their actual business scenarios. For example, users can first perform anomaly attribution for a metric. When a metric anomaly occurs, metric attribution can be performed for that metric, followed by dimensional attribution for these metrics.


**Help documentation: see** [Metric Analysis Tree](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f626c5).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f25cb1cb734439891534000e1156de1~tplv-goo7wpa0wc-image.image" width="2406px" /></div>
