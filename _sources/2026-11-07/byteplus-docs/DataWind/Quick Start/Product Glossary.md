---
title: "Product Glossary"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Product_Glossary"
---

<span id="_1-数据集"></span>
# 1. Dataset


|**Term** |**Description** |
|---|---|
|Dataset |A dataset is a data model composed of one or more tables. It serves as the foundation for visual queries, charts, and dashboards. Before using these three modules, it is necessary to establish a data connection in the "Dataset" module to import data into DataWind. |
|Data type |Data types are used to divide data based on the required memory size. Large memory allocation is only necessary when working with large data volumes. This enables efficient and reasonable use of memory. |
|Expression |Expressions can be edited using SQL to obtain the desired data. For example, if there is a timestamp field creat_time: 1522920936 in the original table, but a month field is actually needed, a function can be used to extract a new field creat_month: 2019\-08. The function is toMonth(toDateTime(create_time)). |
|Data lifecycle |The data lifecycle allows for the periodic cleanup of unnecessary data based on dates, thereby freeing up shared resources. |
|Synchronization type |Data from the specified database is periodically transferred to the DataWind database.<br><br>Scheduled: Data output from the upstream database is synchronized according to the specified time.<br><br>Paused: Synchronization stops after the initial synchronization is completed. |
|Primary key |Setting a primary key for a dataset speeds up queries. Generally, the filter field specified in each query is chosen as the primary key. Multiple primary keys can be set. The first primary key field has the greatest effect, with the others decreasing in importance in order. |
|Partition |Datasets use partitions to horizontally distribute load, physically moving data closer to the users who access it most frequently. |
|Shard |Datasets use shard fields to ensure data is evenly distributed across all nodes. Sharding can improve query speed. |
|Sampling field |When querying a dataset, sampling a small amount of data can improve query speed. By default, HASH is performed based on the sampling field. |
|Sampling ratio |When performing visualized queries, sampling is conducted based on the sampling field. The smaller the proportion, the smaller the data volume, and the faster the visualized query speed. |


<span id="_2-可视化建模"></span>
# 2. Visual modeling


|**Noun** |**Description** |
|---|---|
|Data modeling |The process of cleaning, processing, and producing metadata according to a certain data processing logic is called data modeling. |
|Data connection |The ability to configure connections to various data sources, enabling the primary function of data reading. |
|Canvas |A visual representation of a data processing workflow, where functional modules are organized in a directed workflow. |
|Operator |The integrated capability for data reading, processing, algorithms, and data output on the canvas, corresponding to each block on the canvas. |
|Connection |The directed relationship between operators, referring to the channel for data flow between two operators. |
|Dataset |Refer to [Dataset Overview](https://docs.byteplus.com/docs/DataWind/Dataset_Overview). It is the foundational modeling tool for data preparation, providing basic multi\-table association data modeling capabilities. It also serves as a data container that can be used by products, including ClickHouse datasets and Hive datasets. |
|Real\-time task |A visual modeling task where the data source is updated in real time and the data stream is processed in real time. |
|Offline task |A visual modeling task where the data source is updated on a daily or hourly basis (that is, updated once per day or per hour), and the data processing workflow is executed on a schedule or manually. |


<span id="_3-仪表盘"></span>
# 3. Dashboard


|**Noun** |**Description** |
|---|---|
|Tab |A tab is a collection of multiple pages, and different titles can be displayed for different pages. |
|Global filter |A filter that can be applied to multiple charts at the same time; filters are used to narrow the range of data displayed in charts. |
|Layer order |When different elements overlap, they are displayed according to the layer order. |
|Group |Treats different elements as a whole, allowing you to set and move them together. |
|Markdown |Markdown is a plain text markup language. By using simple markup syntax, ordinary text content can be given specific formatting. |
|Undo |Revert to the state before the most recent operation. |
|Redo |Redo. |
|Align left |Align two or more elements to the left edge. |
|Align vertical center |Align the center lines of two or more elements in the vertical direction. |
|Align right |Align two or more elements to the right edge. |
|Align top |Align two or more elements to the top edge. |
|Align horizontal center |Align the center lines of two or more elements in the horizontal direction. |
|Align bottom |Align two or more elements to the bottom edge. |
|Distribute evenly horizontally |Distribute the center points of two or more elements evenly in the horizontal direction. |
|Distribute evenly vertically |Distribute the center points of two or more elements evenly in the vertical direction. |
|Equal spacing line |When changing the position or size of elements, a guide line appears when the spacing between the moved element and the reference element is equal, or when the height and width are the same. |
|Reference line |When changing the position or size of elements, a guide line appears to assist with layout positioning. |
|Zoom |Zoom in or out of the page. |
|Page settings |Select from common page sizes or customize the page width and height. |
|Appearance settings |Set the page background color or add grid lines to the page. |
|Chart settings |Set whether to hide the chart title and the chart title format; for tables, configure display settings and choose between standard or adaptive table width and height. |
|Transformation settings |Set the XY coordinates of elements or set the width and height of elements. |
|Add description |Add explanatory notes to the chart. |


<span id="_4-可视化查询"></span>
# 4. Visual query


|**Term** |**Note** |
|---|---|
|Table |A table is the basic form for displaying data. By simply configuring dimensions and metrics, you can display the corresponding detailed data. Tables also support style configuration, conditional formatting, column sorting, fixed columns, and more. |
|Pivot table |A pivot table summarizes and displays data according to column and row dimensions. A pivot table can be displayed by simply configuring the column dimensions, row dimensions, and metrics. |
|Detail table |A detail table is a table used to display detailed data. |
|Column chart |A column chart is typically used to describe changes in data over a period of time or across different regions. |
|Bar chart |A bar chart can be considered a horizontal column chart and is usually used to represent changes in data at different times or under different conditions. |
|Line chart |A line chart is generally used to observe data trends. |
|Area chart |An area chart is similar to a line chart, but the difference is that an area chart fills the space between the line and the X\-axis with color. It is suitable for describing data trends and the contribution of parts of the data to the whole. |
|Dual\-axis chart |A dual\-axis chart refers to a data chart with two Y\-axes, often combining a column chart and a line chart, making the chart display more intuitive. It is suitable for scenarios such as analyzing two data sets with large differences, different data trends, or comparing data year\-over\-year and month\-over\-month. |
|Pie chart |In a pie chart, the central angle of each sector is determined by the proportion of the quantity it represents to the whole, and it is commonly used to show the proportion of part of the data to the whole. |
|Map |The map feature supports displaying differences in quantities across different regions. |
|Bidirectional bar chart |A bidirectional bar chart uses both forward and reverse bars to display value comparisons between categories. |
|Combo chart |A combo chart is typically used to compare and display multiple metrics and their changes within the same dimension. |
|Scatter plot |A scatter plot, also known as an X\-Y chart, displays all data as points on a Cartesian coordinate system to show the degree of correlation between variables. The position of each point is determined by the values of the variables. |
|Word cloud |A word cloud is a visual representation of text data, forming a colorful cloud\-like graphic composed of words to display large amounts of text data. The importance of each word is shown by its font size. |
|Histogram |Histogram: Its shape is similar to a bar chart, but it has a completely different meaning from a bar chart. A histogram involves statistical concepts. First, the data must be grouped, and then the number of data points in each group is counted. In a Cartesian coordinate system, the horizontal axis marks each group's endpoints, and the vertical axis represents the frequency. The height of each rectangle corresponds to the frequency for that group. Such a statistical chart is called a frequency distribution histogram. |
|Indicator card |An indicator card can be used to visually display the value of a specific indicator and its related indicators or trends. |
|Sorting |The sorting feature automatically sorts indicators according to certain rules. |
|Top N |Only displays the data for the top few or bottom few entries. |
|Total |Performs summary calculations on the data. |
|Percentage |Calculating percentages quickly determines the proportion that each value occupies in a column of data. |
|Comparison |Comparison analysis refers to differences in data caused by other influencing factors (comparison conditions) under the same data standards (same dimension indicators). |
|Year\-over\-year and month\-over\-month |Quickly calculates year\-over\-year and month\-over\-month values for the data. |
|Indicator template |Modify expressions flexibly by entering parameters. |
|Attribution analysis |Analyze significant increases or decreases in indicators, automatically generate reports, and identify influencing factors. |
|Sampling |Perform sampling operations on the dataset. |
|Routine |Based on SQL query results, visualize the data, generate charts and save them, then perform routine data updates. |
|Monitoring |Monitor relevant indicators in the chart. |
|Dynamic dimensions/dynamic indicators |Allows simple and quick switching between multiple dimensions or indicators in the chart. |
|Drill up/drill down |Create a hierarchical structure based on certain fields, enabling quick drill up or drill down between levels within a visualization item. |
|Alias management |Assign new names to dimension fields. |
|Data panel |This area includes dimensions, metrics, and filters. When fields are placed in this area, a query will be performed. |
|Dimension |A dimension is an aspect for analyzing a metric and usually has only a small number of discrete values. |
|Metric |A metric measures data using different aggregation methods, and in most cases is a number. When defining a metric, you need to specify the scope of the data to be calculated and the calculation method, which we refer to as the 'statistical criteria'. |


<span id="_5-项目中心"></span>
# 5. Project center


|**Term** |**Note** |
|---|---|
|Project |A project refers to an independent workspace in the system, which is generally divided based on business or requirements. Resources and permission controls are independent between different projects. You can create analysis projects based on business topics, business departments, and other themes. Within an analysis project, team members can create visual query charts and dashboards. The main product features are all within specific projects. Each project is logically isolated, and operations and settings within one project do not affect other projects. |
|Resource |Refers to dashboards, datasets, charts, and more. |
|User group |A collection of users |
|Row\-level permission control |Permission control for row\-level data in a dataset |
|Column\-level permission control |Permission control for column\-level data in a dataset |


<span id="_6-sql-查询"></span>
# 6. SQL query


|**Term** |**Note** |
|---|---|
|Workbook |A collection of SQL queries created for a specific need, containing multiple SQL query boxes and query tasks |
|Editor or editor box |SQL query code editor |
|Query task |Refers to a single SQL query task |
|Data source |Refers to the source of data for SQL queries. Currently, supported data sources for SQL queries are Hive and Clickhouse. |
|Cluster |A cluster is a group of service entities working together to provide a service platform with greater scalability and availability than a single service entity. It has scalability and high availability. |
|Queue |This refers to the cluster task execution queue. |
|Parsing |Syntax parsing of SQL query statements |
|Ad hoc query |Add a query editing box to [temporary workbook], so a new workbook will not be opened each time. |
|Batch query / batch query |Split SQL tasks into individual subqueries based on the batch query date, execute each subquery, and then merge the results. |


<span id="_7-权限"></span>
# 7. Permissions


|**Noun** |**Description** |**Use cases** |
|---|---|---|
|System |The system refers to the entire DataWind platform. Whenever DataWind system, BI system, or system appears in the documentation, it refers to this platform; typically, multiple projects may be created within your system. | |
|Project |A project is an independent workspace within the system, generally divided according to business or specific requirements. Resource and permission control between different projects is mutually independent. You can create analysis projects based on business topics, business departments, or other themes. Within an analysis project, team members can create visual query charts and dashboards. The main product features are all within specific projects. Each project is logically isolated, and operations and settings within one project do not affect other projects. |Multiple departments or multiple project teams |
