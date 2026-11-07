---
title: "Getting Started Guide for Business User"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Getting_Started_Guide_for_Business_User"
---

<span id="fab62844"></span>
## Preface

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DataWind is a BI (Business Intelligence) platform. Simply put, it allows us to create charts from our data using an intuitive drag\-and\-drop interface, and these charts can be combined into a dashboard.</div>


First, let us introduce the main modules of DataWind and their relationships. Understanding how DataWind transforms data into charts will help you better understand this product.

The overall workflow of DataWind is illustrated in the diagram below, which mainly involves five concepts:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53de50119ae54b22accca74bb14b1ed1~tplv-goo7wpa0wc-image.image) </span>


|Concept |Note |
|---|---|
|* **`Project`**: There are many business lines in a company, and the data and dashboards for different business lines cannot be grouped together. Therefore, it is necessary to distinguish and isolate them. This is the purpose of projects. Each business line can create its own project, which facilitates resource management and access control. |* In general, users do not participate in project management, so there is no need to pay attention to it. The only point to note is that resources from different projects are isolated. If you find that you cannot locate a dashboard you previously created after opening DataWind, first check whether you have entered the correct project. |
|* **`Data source`**: To create a chart, data is required in the chart, and the origin of this data is the data source. Commonly used tables such as Lark tables, Hive tables, and ClickHouse tables are all considered data sources. | |
|* **`Dataset`**: Since there are many types of data sources, some cannot be queried directly, and for some, direct queries may be slow. Therefore, DataWind requires an intermediary to import data from the data source for storage and subsequent querying. This intermediary is called a dataset. |* Tables that users are most familiar with, such as Lark tables and Excel, can all be made into datasets. To upload your own data, refer to this document: [Dataset Overview](https://docs.byteplus.com/docs/DataWind/Dataset_Overview). |
|* **`Visual query`**: Once data is available in the dataset, you can query this data. This is visual query, which is where we query data and create charts. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b84bd007f89740459b0e9ee56320b156~tplv-goo7wpa0wc-image.image) </span> |
|* **`Dashboard`**: After creating charts, you need a place to display these charts. This is the dashboard, which is essentially a blank canvas where you can arrange different charts, text, images, and more. This is what is commonly referred to as a dashboard. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35cde5c8cd7645f986d30ba4857a57f1~tplv-goo7wpa0wc-image.image) </span> |


The above concepts are mainly to help you understand what DataWind does. For most people, **you only need to understand visual queries and dashboards**, because in many organizations, datasets are usually created by data warehouse personnel in the big data team, so you can use them directly.

Next, we will guide you from importing data, to visual queries (the module we use most frequently), and then to dashboards, helping you get started with DataWind from scratch. Get ready to follow along!

<span id="6363363d"></span>
## Step 1: Import data

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To perform queries in DataWind, you first need data. Data is usually stored in data sources, and you need to import data from these sources into DataWind as datasets before you can run queries.</div>



* <div data-tips="true" data-tips-type="tip"><strong>For most users, the data warehouse team will help create datasets, so you can use them directly. If you do not usually need to create datasets, you can skip this section. To create your own datasets, refer to the process below.</strong></div>



<span id="da989eda"></span>
### 1.1 **Supported data sources in DataWind**


|Source name |Supported connection methods |Supported environments |Whether creation is supported [Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL) |Integration guide |
|---|---|---|---|---|
|Excel/CSV file |Offline extraction, direct connection |SaaS, private deployment |Not supported |[Local Excel/CSV Files](https://docs.byteplus.com/docs/DataWind/Local_Excel_CSV_Files) |
|Access |Offline extraction |Private deployment |Not supported |[Access](https://docs.byteplus.com/docs/DataWind/Access) |
|Kafka |Real\-time extraction |Private deployment |Not supported |[Kafka](https://docs.byteplus.com/docs/DataWind/Kafka) |
|Pulsar |Real\-time extraction |Private deployment |Not supported |[Pulsar](https://docs.byteplus.com/docs/DataWind/Pulsar) |
|GreenPlum |Offline extraction |SaaS, private deployment |Supported |[GreenPlum](https://docs.byteplus.com/docs/DataWind/GreenPlum) |
|SAP HANA |Offline extraction |SaaS, private deployment |Supported |[SAP HANA](https://docs.byteplus.com/docs/DataWind/SAP_HANA) |
|Impala |Offline extraction, direct connection |SaaS, private deployment |Supported |[Impala](https://docs.byteplus.com/docs/DataWind/Impala) |
|ClickHouse Community Edition |Offline extraction, direct connection |SaaS, private deployment |Supported |[ClickHouse](https://docs.byteplus.com/docs/DataWind/ClickHouse) |
|HBase Phoenix |Offline extraction |SaaS, private deployment |Supported |[Hbase Phoenix](https://docs.byteplus.com/docs/DataWind/Hbase_Phoenix) |
|HBase |Offline extraction |SaaS, private deployment |Not supported |[HBase](https://docs.byteplus.com/docs/DataWind/HBase) |
|Vertica |Offline extraction |SaaS, private deployment |Not supported |[Vertica](https://docs.byteplus.com/docs/DataWind/Vertica) |
|Amazon Athena |Offline extraction |SaaS, private deployment |Supported |[Amazon Athena](https://docs.byteplus.com/docs/DataWind/Amazon_Athena) |
|Amazon Redshift |Offline extraction |SaaS, private deployment |Supported |[Amazon Redshift](https://docs.byteplus.com/docs/DataWind/Amazon_Redshift) |
|ByteHouse CDW |Offline extraction, direct connection |SaaS, private deployment |Supported |[ByteHouse CDW](https://docs.byteplus.com/docs/DataWind/ByteHouse_CDW) |
|ByteHouse CE |Offline extraction, direct connection |SaaS, private deployment |Supported |[ByteHouse CE](https://docs.byteplus.com/docs/DataWind/ByteHouse_CE) |
|Presto |Offline extraction, direct connection (supported in V2.50.0 and later) |SaaS, private deployment |Supported |[Presto](https://docs.byteplus.com/docs/DataWind/Presto) |
|Databricks |Offline extraction |SaaS, private deployment |Supported |[Databricks](https://docs.byteplus.com/docs/DataWind/Databricks) |
|AnalyticDB for MySQL 2.0 |Offline extraction |SaaS, private deployment |Supported |[AnalyticDB for MySQL 2.0](https://docs.byteplus.com/docs/DataWind/AnalyticDB_for_MySQL_2_0) |
|AnalyticDB for MySQL 3.0 |Offline extraction |SaaS, private deployment |Supported |[AnalyticDB for MySQL 3.0](https://docs.byteplus.com/docs/DataWind/AnalyticDB_for_MySQL_3_0) |
|Hologres |Offline extraction, direct connection |SaaS, private deployment |Supported |[Hologres](https://docs.byteplus.com/docs/DataWind/Hologres) |
|MySQL |Offline extraction, direct connection |SaaS, private deployment |Supported |[MySQL](https://docs.byteplus.com/docs/DataWind/MySQL) |
|IBM DB2 |Offline extraction |SaaS, private deployment |Supported |[IBM DB2](https://docs.byteplus.com/docs/DataWind/IBM_DB2) |
|Oracle |Offline extraction |SaaS, private deployment |Supported |[Oracle](https://docs.byteplus.com/docs/DataWind/Oracle) |
|PostgreSQL |Offline extraction, direct connection |SaaS, private deployment |Supported |[PostgreSQL](https://docs.byteplus.com/docs/DataWind/PostgreSQL) |
|OpenGauss |Offline extraction |SaaS, private deployment |Supported |[OpenGauss](https://docs.byteplus.com/docs/DataWind/OpenGauss) |
|SQL Server |Offline extraction |SaaS, private deployment |Supported |[SQL Server](https://docs.byteplus.com/docs/DataWind/SQL_Server) |
|Teradata |Offline extraction |SaaS, private deployment |Supported |[Teradata](https://docs.byteplus.com/docs/DataWind/Teradata) |
|Doris |Offline extraction, direct connection |SaaS, private deployment |Supported |[Doris](https://docs.byteplus.com/docs/DataWind/Doris) |
|Damon |Offline extraction |SaaS, private deployment |Supported |[Damon](https://docs.byteplus.com/docs/DataWind/Damon) |
|TiDB |Offline extraction |SaaS, private deployment |Supported |[TiDB](https://docs.byteplus.com/docs/DataWind/TiDB) |
|GoldenDB |Offline extraction |SaaS, private deployment |Supported |[GoldenDB](https://docs.byteplus.com/docs/DataWind/GoldenDB) |
|OceanBase MySQL |Offline extraction |SaaS, private deployment |Supported |[OceanBase MySQL](https://docs.byteplus.com/docs/DataWind/OceanBase_MySQL) |
|OceanBase Oracle |Offline extraction |SaaS, private deployment |Supported |[OceanBase Oracle](https://docs.byteplus.com/docs/DataWind/OceanBase_Oracle) |
|Hive |Offline extraction |SaaS, private deployment |Supported |[Hive](https://docs.byteplus.com/docs/DataWind/Hive) |
|MaxCompute |Offline extraction |SaaS, private deployment |Supported |[MaxCompute](https://docs.byteplus.com/docs/DataWind/MaxCompute) |
|Transwarp Inceptor |Offline extraction |SaaS, private deployment |\-\- |[Transwarp Inceptor](https://docs.byteplus.com/docs/DataWind/Transwarp_Inceptor) |
|StarRocks |Offline extraction, direct connection |SaaS, private deployment |Not supported |[StarRocks](https://docs.byteplus.com/docs/DataWind/StarRocks) |
|Huawei FusionInsight |Offline extraction |SaaS, private deployment |Supported |[Huawei FusionInsight](https://docs.byteplus.com/docs/DataWind/Huawei_FusionInsight) |
|Tencent Cloud DLC |Offline extraction |SaaS, private deployment |Supported |[Tencent Cloud DLC](https://docs.byteplus.com/docs/DataWind/Tencent_Cloud_DLC) |
|DataFinder |Direct connection |SaaS, private deployment |Not supported |[DataFinder Data Integration](https://docs.byteplus.com/docs/DataWind/DataFinder_Data_Integration) |
|LAS (public cloud version) |Offline extraction |SaaS, private deployment |Supported |[LAS](https://docs.byteplus.com/docs/DataWind/LAS) |
|Intelligent outbound call |Offline extraction |SaaS, private deployment |\-\- | |
|Metadata connection and application |\-\- |Private deployment |\-\- |[Metadata Connection and Application](https://docs.byteplus.com/docs/DataWind/Metadata_Connection_and_Application) |
|Douyin ecosystem data |Offline extraction |SaaS, private deployment |Not supported |None |
|Ocean Engine/Qianchuan |Offline extraction |SaaS, private deployment |Not supported |Ocean Engine/Qianchuan |
|REST API |Offline extraction |SaaS, private deployment |Not supported |[REST API 2.0](https://docs.byteplus.com/docs/DataWind/REST_API_2_0) |
|Content platform |Offline extraction |SaaS, private deployment |Not supported |Content management platform |
|MongoDB |Offline extraction |SaaS, private deployment |Supported |[MongoDB](https://docs.byteplus.com/docs/DataWind/MongoDB) |
|WeChat Official Account |Offline extraction |SaaS, private deployment |Not supported |WeChat Official Account |
|Constellation data |Direct connection |SaaS, private deployment |Not supported |Constellation data |
|Calendar data |Direct connection |SaaS, private deployment |Not supported |Calendar data |
|Lark Spreadsheet |Offline extraction |SaaS, private deployment |Not supported |[Lark Sheets](https://docs.byteplus.com/docs/DataWind/Lark_Sheets) |
|Lark Multidimensional Table |Offline extraction |SaaS, private deployment |Not supported |[Lark Base Table](https://docs.byteplus.com/docs/DataWind/Lark_Base_Table) |
|Lark Project (Meego) data |Offline extraction |SaaS, on\-premises deployment |Not supported |Lark Project (Meego) data |


<span id="0877c999"></span>
### 1.2 **Configuration process**

For specific configuration steps, refer to the integration help documentation for the supported data sources above.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5eb3cf332134a85a5339d2dfd8c9d42~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


<span id="e8c4d63f"></span>
## Step 2: Using visual queries

<span id="f6b2af7d"></span>
### 2.1 **Page layout of visual queries**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Now we have arrived at the most important module for everyone: visual query, which is where we query data.</div>


**First, the overall layout of the visual query page is divided into four areas**:

A. **Dataset information and field list**: Displays which dataset you are querying, what fields are in this dataset, and allows you to switch datasets here

B. **Chart and analysis features**: Select chart types, configure charts, and choose analysis features (such as sorting, percentage, period\-over\-period comparison, table calculations, and more)

C. **Chart display area**: Place the fields you want to query here. This area displays the final chart style and allows you to adjust the chart's data format and more

D. **Toolbar**: Query history, download data, configure chart data monitoring, and save charts

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/039cab5f584e49f3b33fff78869d2fbb~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="4d2b589f"></span>
### 2.2 Concepts of dimensions and metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before performing queries, there is a small concept that everyone needs to learn, which is the concept of dimensions and metrics. Dimensions and metrics are generally collectively referred to as <strong>fields.</strong></div>


Refer to the two diagrams below. On the left, I have placed all fields from a dataset in Smart Data Insight into a chart, while on the right is the underlying data of this dataset. You will notice that **each field here corresponds to a specific column in the original data**. Additionally, when the chart type selected in Smart Data Insight is a standard table, the queried data is very similar to the original data (it appears identical, but there are differences, which we will discuss later).

**Therefore, when selecting fields in Smart Data Insight, it is essentially equivalent to querying specific columns from the underlying data:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18bd928056ca44fd973295b417cd5e30~tplv-goo7wpa0wc-image.image) </span>

Next is **the difference between dimensions and metrics**, which is relatively straightforward. You can think of a dimension as the granularity at which you view the data, while a metric is a measure. For example, if you want to view the grades of all students in a class, the students' names are dimensions, and the grades are metrics. Dimensions and metrics are not fixed; sometimes a dimension field can also serve as a metric. For instance, if you want to see how many students fall into each grade range, the intervals defined for grades are dimensions, and the count of student names is the metric.

The same applies in Smart Data Insight: **even if a field is classified as a dimension, it can still be placed in the metrics section, and metric fields can also be placed in the dimensions section.** 

<span id="cefc17b7"></span>
### 2.3 Steps for querying data

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Next are the steps for using visual query. Here, we will use a hypothetical requirement as an example to walk everyone through how to use DataWind to fulfill a data query requirement.</div>


<span id="cfc5100c"></span>
#### 2.3.1 Process for completing a query

**Query example 1**


|**Suppose our current data query requirement is**: For Q2 2024, for all secondary subcategories under the primary video category 'Music', show the trend of the number of items submitted for review where the number of followers is greater than 1,000.<br><br><br>* Upon receiving this requirement, it can first be broken down as follows:<br><br>   * Filter conditions: Q2 2024, number of followers greater than 1,000, primary video category is Music<br><br>   * Dimensions: Secondary subcategory, date (although not explicitly stated in the requirement, date is definitely needed to view the trend)<br><br>   * Metric: Number of items submitted for review<br><br>   * Objective: View the trend ||
|---|---|
|Step 1. First, place the required dimensions and metrics into the dimensions and metrics panel. You can either drag them or click the fields on the left. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b9a13ce6f0249bfbd9043b6cd1e1264~tplv-goo7wpa0wc-image.image) </span> |
|Step 2. Then configure the filters. You can also drag the fields to be filtered into the filter panel and then select the appropriate filtering method. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7356f9348fc44dac91ca612f649a7d3f~tplv-goo7wpa0wc-image.image) </span> |
|Step 3. Finally, select a suitable chart.<br><br>> Since we want to view the trend, a line chart is selected. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e42ce9f41814bc2a628754cee714d8e~tplv-goo7wpa0wc-image.image) </span> |


**Query example 2**


|**Suppose our current data query requirement is**: At the granularity of the primary video category, view the proportion of videos sourced from Douyin for this year.<br><br><br>* Upon receiving this requirement, it can first be broken down as follows<br><br>   * Filter conditions: This year, video source is Douyin<br><br>   * Dimension: Primary video category<br><br>   * Metric: Number of videos<br><br>   * Objective: View the proportion ||
|---|---|
|1. First, place the required dimensions and metrics in the dimensions and metrics section.<br><br>> You will notice that this dataset does not have a metric for the number of videos, but it does have a video ID field. If you count the video IDs, that is the number of videos. Therefore, you can drag this field to the metrics section and select count. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b9a13ce6f0249bfbd9043b6cd1e1264~tplv-goo7wpa0wc-image.image) </span> |
|2. You can configure filters. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7356f9348fc44dac91ca612f649a7d3f~tplv-goo7wpa0wc-image.image) </span> |
|3. Finally, select an appropriate chart.<br><br>> Since you want to view proportions, you can choose a pie chart. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43bbe0faec0d4051a02b1d8ca95d663c~tplv-goo7wpa0wc-image.image) </span> |


<span id="0012775e"></span>
#### 2.3.2 Three concepts to learn


|**How to distinguish field types** |The fields in DataWind are categorized just like those in Excel spreadsheets. You can distinguish them by the icon in front of the field name, as shown in the figure below:<br><br><br>* **Red indicates date, green indicates text, and yellow indicates numeric values (including decimals and integers).** <br><br>* The main point to note is that different types of fields require different filtering methods.<br><br>   * For example, date types can be filtered by the most recent N days. However, if the field is named 'date' but is actually a text type, you can only select individual values in the filter. To enable date filtering, contact the dataset owner to make adjustments.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/176dbaf4c96440bfac7403b1b31e1a1c~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|**What does sum above the metrics mean?**  |If you are new to DataWind, you may be confused about why 'sum' appears in front of fields placed in the metrics section, and sometimes 'count' or 'aggregate' is shown.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a34d91b536704355b7f678ae98b785d9~tplv-goo7wpa0wc-image.image) </span><br><br>There is a concept called aggregation here, which is actually easy to understand. **When a set of data is calculated to produce a single value, this calculation process is called aggregation.** <br><br><br>* For example, the commonly used sum operation calculates a single value from a set of numbers; finding the maximum value also produces a single value from a set; counting also results in a single value from a set. This is essentially aggregation.<br><br><br>Since most users rarely view detailed data, DataWind automatically aggregates the metrics you add to charts—except for detail tables—according to your selected dimensions.<br><br>For example:<br><br><br>* The left side below shows a query in DataWind. Here, the dimension is primary business, and the metric is review volume. The system automatically sums the review volume, so what you see is the total review volume under each primary business.<br><br>* The right side displays the underlying raw data, which consists of a large number of records.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6126010c013f4b429315832c8d655747~tplv-goo7wpa0wc-image.image) </span><br><br>Of course, users may not always need summed data. You can click the downward triangle in front of the metric to select the aggregation method—for instance,**choose count to view quantity; choose average to view the mean.** <br><br>As mentioned earlier, fields have different types. Here:<br><br><br>* Numeric types allow you to select mathematical operations such as sum.<br><br>* Text types only allow operations such as count.<br><br>* There is a special case: if the field's expression already uses an aggregation function (such as sum or count), SQL syntax does not permit nested aggregation. Therefore, the system will automatically display "Aggregation" for such fields, and you cannot select other aggregation methods.<br><br>   * Side note:**Fields with aggregation functions in their expressions cannot be placed in the dimension column!** <br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2255d629b3ac4128b0f9aa77bd6d0911~tplv-goo7wpa0wc-image.image) </span> |
|**What is the p_date filter?**  |Attentive users may notice that the filter bar in DataWind visual queries always automatically includes a filter called p_date. This filter cannot be removed from the filter list, meaning it must be applied.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9e60d41954e4212ab615ec6fcb599f3~tplv-goo7wpa0wc-image.image) </span><br><br>Users often wonder what p_date is when using the system.<br><br>In databases, there is a concept called partition, which you can think of as similar to a sheet in a Lark table. Each day, a new sheet is added, and the data for that day is placed inside it. To make it easier to distinguish between these partitions, the partition name is defined as the date of that day. As for p_date, it actually refers to the partition, meaning the date when the data was updated. Filtering by a specific p_date means viewing the data updated on that particular day.<br><br>There is also a related concept here: incremental datasets and full datasets.<br><br><br>* Incremental table: Each partition only updates the data for the current day.<br><br>* Full table: Each partition updates all data from history up to the present.<br><br><br>**When querying a full dataset, filter the partition for the most recent day with data. When querying an incremental dataset, filter the partitions for the entire period you want to query.**  |


<span id="59c774a8"></span>
### 2.4 **Saving, downloading, and sharing**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After completing the query, you can choose to save the current chart, download the data, or share the current query results with other colleagues.</div>



* <div data-tips="true" data-tips-type="tip">When saving, if you have already created a dashboard, you can directly select that dashboard to save to.</div>


* <div data-tips="true" data-tips-type="tip">When downloading, you can choose to download the data. If it is a chart, you can also choose to download the image.</div>


* <div data-tips="true" data-tips-type="tip">Query results in Smart Data Insight can be shared via a browser link.</div>




|**Save chart**<br><br><br>* After the chart is created, you can click Save on the toolbar to save it as a chart.<br><br>* If a dashboard has already been created, you can directly select the dashboard to quickly add the chart to it.<br><br>* If a dashboard has not been created or you do not plan to display it on a dashboard, you can leave it unselected. Later, you can find the chart in [Chart Management](https://docs.byteplus.com/docs/DataWind/Chart_Management). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbc6299f64324e80b8c0f5f657d6dfa9~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|**Download data**<br><br><br>* After creating a chart, if you do not need to save the chart, you can also choose to download the data or import a screenshot of the chart.<br><br>* Caution: Be sure to pay attention when downloading the pivot table. You need to select the pivot table format during download; otherwise, the downloaded file will not be a pivot table. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47f006f463434ddcac883402fdcb46c8~tplv-goo7wpa0wc-image.image) </span> |
|**Share queries**<br><br><br>* In Smart Data Insight, each time you click to run a query, a unique query link is generated. You can directly copy the browser link, and when other users open it, they will enter the same query page as you.<br><br>* If you obtain another user's query link and want to continue querying based on their results,<br><br>   * If the top displays 'Unsaved query', **you can freely modify and save it without affecting other users**.<br><br>   * If the top displays a chart name and the 'Save as' button in the upper right corner is clickable, you **can modify the query conditions as needed; just make sure not to click Save**, or you will overwrite the saved conditions of others. Of course, clicking **Save as to save your own chart is fine**. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/987cc1818f704c41aaaaa006d97bbdaa~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3672d5a80cc4341ab9bb393c26fd5be~tplv-goo7wpa0wc-image.image) </span> |


<span id="57d0cd00"></span>
### 2.5 Common chart configurations

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Here are some commonly used chart configuration options. You can click the blue text to jump to the detailed help documentation.</div>



|Configuration |Description |
|---|---|
|Change [data format](https://www.volcengine.com/docs/4726/1163440#_2-2-%E8%AE%BE%E7%BD%AE%E6%95%B0%E6%8D%AE%E6%A0%BC%E5%BC%8F)<br><br><br>* You can adjust the unit, format, prefix or suffix, number of decimal places, and more for the data in the chart. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e237953ae3e4682bb175f2d3eb2c383~tplv-goo7wpa0wc-image.image) </span> |
|Change [date granularity](https://www.volcengine.com/docs/4726/1163439)<br><br><br>* For date\-type fields, you can quickly change the date granularity in the chart. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe2517972ff44d358c55b31ba3362f41~tplv-goo7wpa0wc-image.image) </span> |
|Change [header name](https://www.volcengine.com/docs/4726/37012#_2-1-%E5%8D%95%E4%B8%AA%E5%AD%97%E6%AE%B5%E4%BF%AE%E6%94%B9)<br><br><br>* You can modify the header names in the chart. This is only a temporary change and does not affect the field's actual name. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a1e62e9c7c4b378d0822fa8ae18918~tplv-goo7wpa0wc-image.image) </span> |
|Quick sort<br><br><br>* Whether in visual queries or dashboards, move the mouse to the right side of the corresponding header and click the icon that appears to open the quick sort popup, where you can quickly sort the data. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19a5724c452a448398d66c7f57505409~tplv-goo7wpa0wc-image.image) </span> |
|Display data on the chart<br><br><br>* This allows each data point on the chart to display its specific value. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/174e4b485d72435cb5c8419c50f22859~tplv-goo7wpa0wc-image.image) </span> |


<span id="6e35765e"></span>
### 2.6 Advanced features for visual queries

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section mainly introduces some advanced features of the visualization query page. These features are not strictly required, but if you have similar scenarios, they can help you.</div>


<span id="4184edc6"></span>
#### 2.6.1 Chart configuration


|Configuration |Description |
|---|---|
|[Dynamic Dimensions and Dynamic Metrics](https://docs.byteplus.com/docs/DataWind/Dynamic_Dimensions_and_Dynamic_Metrics)<br><br><br>* To replace dimensions or metrics in a chart without modifying the chart itself, try this feature.<br><br>* A common scenario is to place dates with different time granularities in dynamic dimensions, so you can quickly switch date granularity on the dashboard.<br><br>* Sample link: [Dynamic Dimensions and Dynamic Metrics](https://docs.byteplus.com/docs/DataWind/Dynamic_Dimensions_and_Dynamic_Metrics) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb8b26a565394b63a8eafc0c1e901a24~tplv-goo7wpa0wc-image.image) </span> |
|[Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down)<br><br><br>* When performing analysis, for example, if you notice a data anomaly in a primary business line and want to examine the secondary business lines under it in detail, you can use this feature.<br><br>* Drill down to other dimensions for analysis without modifying the chart. | |
|[Overview of Field Configuration](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration)<br><br><br>* This feature is relatively simple. It makes the data in the chart easier to distinguish and also improves the appearance of the chart. Currently, it supports adding single color, icon sets, color scales, and data bars to charts.<br><br>* Sample link: [Overview of Field Configuration](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99e7d18b803841389d2ea5339d0040bd~tplv-goo7wpa0wc-image.image) </span> |


<span id="3cd19ef0"></span>
#### 2.6.2 Filter configuration


|Configuration |Description |
|---|---|
|Place filters on the chart<br><br><br>* By selecting "Show as chart filter", you can place the filter box on the chart, making it easier to quickly switch filters. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6866bfbc7847a3af9be1683df7c3da~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5320025fd9bc41eeb0fa7464fa62190e~tplv-goo7wpa0wc-image.image) </span> |
|[Combination Filter](https://docs.byteplus.com/docs/DataWind/Combination_Filter)<br><br><br>* In the filter bar of DataWind, multiple filters are combined with an AND relationship by default. To implement more complex filtering, use the combined filtering feature. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b462b3c24e443b59d9af0ed17c98ec0~tplv-goo7wpa0wc-image.image) </span> |
|[Subfilters](https://docs.byteplus.com/docs/DataWind/Subfilters)<br><br><br>* Sub\-filters enable cascading between filters. For example, if province and city filters are set to cascade, after selecting a province, only the cities under that province will be displayed in the city filter. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77d0a1f0bba9469c950e1dc13db3177e~tplv-goo7wpa0wc-image.image) </span> |


<span id="f01606c2"></span>
#### 2.6.3 **Analysis features**


|Sorting, percentage, period\-over\-period comparison, table calculation, comparison, and more<br><br><br>* DataWind previously recorded dedicated courses for each analysis feature. You can refer to: [DataWind video tutorial - Data Analysis](https://www.volcengine.com/docs/4726/65109) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2251abd231e42468d629f78d59eba64~tplv-goo7wpa0wc-image.image) </span> |
|---|---|


<span id="158b5fa2"></span>
#### 2.6.4 Chart monitoring


|Detect data in charts and trigger alerts<br><br><br>* DataWind supports monitoring and alerting. This feature (dimensions must include a date field) supports configuring metric fluctuation monitoring and dimension enumeration value change monitoring. For example, when a metric fluctuation reaches a certain threshold, it will automatically send alert notifications to users or groups. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/418f6d9967974678bb94c4006f79cd0e~tplv-goo7wpa0wc-image.image) </span> |
|---|---|


<span id="dbd23ba3"></span>
## 3. Step 3: Using dashboards

<span id="706b071c"></span>
### 3.1 Create a blank dashboard

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This chapter introduces the dashboard of DataWind. Previously, we learned how to use visual queries to obtain data, and the charts created can be saved. These charts need a place to be displayed collectively—that is the dashboard. It is essentially a blank canvas, where you can arrange components such as charts, text, and images. For dashboard building techniques and processes, you can also refer to <a href="https://docs.byteplus.com/docs/DataWind/Dashboard_Overview">Dashboard Overview</a>.</div>


<span id="90da4e11"></span>
### 3.2 **Personal dashboards and public dashboards**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since creating a dashboard is equivalent to adding a resource under a project, project edit permissions are required. However, some users may only want to create a dashboard for personal viewing and do not wish to bother others by requesting permissions. Therefore, DataWind provides both personal dashboards and public dashboards. Please note:</div>


<div data-tips="true" data-tips-type="tip">A personal dashboard can grant others view permissions at most. To allow other users to collaboratively edit and maintain the dashboard, a public dashboard must be created.</div>



| |**Personal dashboard** |**Public dashboard** |
|---|---|---|
|Permissions required for creation |Project view permissions |Project edit permissions |
|Maximum permissions that can be granted to others |View permissions |Manage permissions |


As for how to choose between creating a personal dashboard or a public dashboard, you will be prompted to select the save path for the dashboard during creation. If you choose the personal dashboard path, the dashboard created will be a personal dashboard; otherwise, it will be a public dashboard.


* If you later move a dashboard from the personal dashboard path to the public dashboard path, it will become a public dashboard, and vice versa.


<span id="36e5ffbd"></span>
### 3.3 Edit dashboard

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After creating a blank dashboard, you can start editing it. Editing a dashboard is actually quite simple. If you have ever worked with PowerPoint, adding elements here is just like adding them in PowerPoint.</div>


<span id="6e2054d7"></span>
#### Step 1: Enter the edit page


|1. Click Edit in the upper right corner of the blank dashboard to enter the editing page. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4352faa62a4e4e1595a42a8c7a5649d7~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64b5cda54b374a3baaa6b0c07e8636f9~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|2. Let us first get familiar with the layout of the page.<br><br>* The left side is the component bar, which shows what can be added to the dashboard, such as charts, images, text, web pages, and more.<br><br>* The area below is where you can add Sheet pages. For example, to divide a dashboard into multiple pages, you can use this feature.<br><br>* The top is the toolbar, which allows you to adjust layers and similar settings.<br><br>* The right side is where you configure the page, such as layout style, background color, and other options. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e964d77a7cb4c3c94255f2533934ed1~tplv-goo7wpa0wc-image.image) </span> |


<span id="bc9b77a2"></span>
#### Step 2: Add charts and other components


|(1) Click Add Chart on the left, or drag it directly onto the central canvas with your mouse, and a chart component will be added to the canvas. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1da82f4aa4dd47808312ef6879774de9~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|(2) Once you have a chart component, you can configure the corresponding chart for it. There are two ways to do this. |* The first way is to search for charts previously saved in history on the right and add them directly.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e925767d6d14407ca9925e5211f8ada5~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae6c4466b0c44d4cad60544707c512e7~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The second way is to click Add Chart in the center of the component to enter the query page and create a chart on the spot.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f61311e5736d46fca17b2f6194cdca97~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/424c90f879f9438c826cb5347213d549~tplv-goo7wpa0wc-image.image) </span> |
|(3) After adding charts to the dashboard, if you need to add explanations or make the structure clearer, you can also add other components, such as titles, images, explanations, and so on. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0556f37c9bd4d8eaa167ef8d179f67d~tplv-goo7wpa0wc-image.image) </span> |
|(4) Once the dashboard is finished, click Save in the upper right corner. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51e31d7f33b74b77a01b4dab51b32a7b~tplv-goo7wpa0wc-image.image) </span> |


<span id="76e69e1d"></span>
#### Step 3: Configure some minor dashboard settings


|**Add Sheet pages**<br><br><br>* You can add multiple Sheet pages to a dashboard, placing different charts on each page. This is suitable for scenarios where a core dashboard displays multiple categories of data. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edb14a3ad84a4eabb7d6856ba6376205~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|[Dashboard Theme](https://docs.byteplus.com/docs/DataWind/Dashboard_Theme)<br><br><br>* To make the dashboard more visually appealing, you can use the theme feature of DataWind, which allows you to configure the color scheme, fonts, data formats, and more for all charts with one click. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fcf9365e1f54633a1d770ba5e477b8a~tplv-goo7wpa0wc-image.image) </span> |
|**Layout style**<br><br><br>* DataWind supports two layout modes<br><br>   * Tile layout: When dashboard components are dragged, the layout automatically adjusts, making it easy to quickly arrange them.<br><br>   * Free layout: As the name suggests, all components can be freely moved to any position, which is suitable for scenarios with special layout requirements. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c98d152ee6074b828c4b15618a62ab50~tplv-goo7wpa0wc-image.image) </span> |
|[Global Filter](https://docs.byteplus.com/docs/DataWind/Global_Filter)<br><br><br>* Sometimes, there are many charts on the dashboard, and when viewing data, users may want to change the filter criteria for all charts with a single action. This can be achieved using the global filter. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0d08d76d6db4f9c8a20f492e6e6883e~tplv-goo7wpa0wc-image.image) </span> |


<span id="49b3f538"></span>
### 3.4 Several common uses of dashboards

In addition to providing a unified view of chart data, dashboards also have several other uses:


|**Copy dashboards or charts**<br><br><br>* In many cases, dashboards or charts can be reused. For example, if another user's chart is well made and you want to reuse it, DataWind provides several copy features.<br><br>* These copy features require certain permissions, such as for datasets or dashboards. **If you find that this option is not available when you click, it means you do not have permission.**  |* The first method allows you to copy a chart from the current dashboard to another dashboard (the copied chart is a duplicate).<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/986f34e6f15249a1b42b52d0c04b117b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The second method allows you to copy the entire dashboard directly (you can choose whether to create chart duplicates; if you do not create duplicates, modifying a chart in one dashboard will synchronize the changes to the corresponding chart in both dashboards).<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7127bb80cc2e4795afef96b2684f86bb~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The third method allows you to copy a sheet page to another dashboard (you can choose whether to create chart duplicates; if you do not create duplicates, modifying a chart in one dashboard will synchronize the changes to the corresponding chart in both dashboards).<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99e9e6e792c345609afe1b6f2874f814~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|**Configure dashboard**<br><br><br>* The product allows users to configure subscriptions for dashboards. Once configured, the dashboard will automatically send its content as screenshots every day via Lark, email, or other office software to a specific user or group chat, making it easier for everyone to view the data daily. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db7900833db440f8bb0053fc1e9711f9~tplv-goo7wpa0wc-image.image) </span> |
|**Embed the** [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding)<br><br><br>* The charts placed on the dashboard can be embedded. For example, when writing a weekly report, you can insert them into a Lark document and view the data just as you would on the dashboard. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/560593b6cec54e3bb46aff43bd0f1df3~tplv-goo7wpa0wc-image.image) </span> |


<span id="28f2de5b"></span>
## 4. Get familiar with the permission system

<span id="95cbb2bb"></span>
### 4.1 **Permission description**


* The product has two types of permissions:

   * The first type is resource permissions. For example, dashboards and datasets are referred to as resources in DataWind, and actions such as viewing, editing, and managing them are considered resource permissions.

   * The second type is row and column permissions, which apply only to datasets. Row and column permissions determine which rows of data users can view in a dataset.

   * Normally, if a user has dashboard permissions, they can view chart data even without dataset permissions for the charts. However, if the dataset is configured with row and column permissions, the user must also have row and column permissions for the dataset to view the data.


<span id="f53e623e"></span>
### 4.2 **How to grant permissions to others**


* Caution: Only dashboard or dataset administrators can proactively grant permissions to others.

* Normally, the creator of a resource becomes the owner of that resource and has management permissions. However, the owner does not necessarily have management permissions. For example, if the project is under moderate or higher control, the resource creator will have at most editing permissions.



|**Dashboard** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5acd166ad51d477ebbf5332b85c549ee~tplv-goo7wpa0wc-image.image) </span> |
|---|---|
|**Dataset** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4a6efbe83d04eaba154576749c5eb70~tplv-goo7wpa0wc-image.image) </span> |


<span id="55ad589e"></span>
### 4.3 **How to request permissions**


|**Project center \- permission application** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98e2714d760c4d299e820942900c646e~tplv-goo7wpa0wc-image.image) </span> |
|---|---|


<span id="d7f8d963"></span>
## 5. How to seek help when encountering problems

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">During usage, users may encounter various issues. Since DataWind primarily serves as a platform for querying data and gaining business insights, the data available for querying may be maintained by the business teams within the enterprise. Therefore, some issues encountered are related to product functionality, while others are business\-related. How can users seek help correctly when encountering issues to improve efficiency?</div>



|**DataWind product usage issues**<br><br><br>* This includes problems such as not knowing how to use certain features, feature malfunctions, feature consultations, submitting requirements, and other product\-related issues. |* DataWind provides a help documentation center, where you can search for keywords to find solutions: User Guide.<br><br>* If the issue still cannot be resolved, you can seek after\-sales support in the lower right corner of the DataWind product page. |
|---|---|
|**Business issues**<br><br><br>* This includes cases where dataset data does not match online data, unclear field definitions, or not knowing what certain fields mean. |If such issues arise while viewing a dashboard, you can consult the dashboard owner.<br><br>If such issues arise during a query, you can consult the dataset owner.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3160f376f4794f48a5c9d7f5f403159d~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fadc2af30a0b4c27b70bf4f43ad17a4c~tplv-goo7wpa0wc-image.image) </span> |
