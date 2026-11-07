---
title: "Troubleshooting Methods for DataWind Product Usage Issues"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Troubleshooting_Methods_for_DataWind_Product_Usage_Issues"
---

<span id="_1-权限逻辑问题"></span>
# 1. Permission logic issues

**How to understand this?** 

For editing and managing permissions of resource objects, there is a dependency on the permissions of upstream resources. Therefore, it is necessary to trace back to upstream objects to confirm whether at least viewing permissions are granted. For example:

User A is the manager of dataset X, as well as the manager of the data connection XLink, which is an upstream dependency of dataset X. When A grants user B the “manage” or “edit” permissions for dataset X, it is also necessary to grant user B at least viewing permissions for the data connection XLink. Otherwise, user B will not be able to access or import XLink when editing the dataset, which is required for adjusting the dataset.

User A is the owner of charts P and M in the dashboard, and is also the manager of dataset X, which charts P and M depend on. When user A not only grants user B viewing permissions for the dashboard, but also allows user B to edit charts P and M, it is also necessary to grant user B at least viewing permissions for dataset X.

In other words, to obtain management or editing permissions for the current resource object, it is necessary to trace back and ensure at least viewing permissions for the upstream objects that the resource object depends on.

**Solution approach**

Permission\-related errors are generally caused by insufficient permissions. According to the principle above, backtracking to obtain the necessary authorizations usually resolves the issue.

Another type of permission issue is: Sometimes, in the visual query interface, you may see **gray capsule fields** in certain charts. This occurs because the chart uses fields that others have saved as personal dataset fields in the dataset.

> For permission issues, see [Permission Operation Manual](https://docs.byteplus.com/docs/DataWind/Permission_Operation_Manual) (reference incomplete).


<span id="_2-数据集管理"></span>
# 2. Dataset management

**How to understand this?** 

A dataset is essentially a business repository that stores required data from upstream business data sources. It serves both as an intermediate transformation and storage tool for synchronizing data to DataWind, and as a business\-customized data warehouse.

The base table storage of the dataset is the storage and computing engine of DataWind. It connects to multiple data sources, masking the specificity of data formats and standards of different source databases. This enables a certain degree of data cleansing and allows downstream visualization query functions to ignore SQL heterogeneity among data sources. As a result, all upstream chart creation and analysis can be performed using a unified data format and function library.

The dataset decouples business intelligence from direct dependency on business source databases. It supports both offline complex analytical queries and fast, direct single\-table ad hoc queries.

The dataset serves as the upstream dependency for BI charts and also acts as the output node (data warehouse) of visual modeling projects.

<span id="_2-1-模型逻辑："></span>
## 2.1 Model logic:

The most critical aspect of maintaining a dataset is model management and editing. The model determines the scope of extracted data and the data cleansing logic.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/748109c7ab64422faf1574f166613412~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-关联（join）"></span>
## 2.2 **Join**

When the data volume is large, duplicate statistics may occur during queries, which often confuses business users and is difficult to understand.

For troubleshooting, check whether the field (dimension or metric) being evaluated within a limited number of rows is from the primary table in the model for (left, inner, or full) joins. In the joined table, according to the join relationship, if the primary table and the joined table have a 1:N relationship, then in the generated dataset base table, each row of the primary table will be duplicated N times as a Cartesian product to connect to the fields of subsequent tables.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36c39a15919b419aa6a67a9ed04886d2~tplv-goo7wpa0wc-image.image" width="1446px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd0d8f9375bb4a0d9752d7bf9dcc35bc~tplv-goo7wpa0wc-image.image" width="801px" /></div>


At this point, directly counting the primary table (such as the Name field in the above figure) in the concatenated dataset base table will yield 10 rows, which is more than the original 7 rows in the A\-Role table's name field. Or, when filtering for the number of roles with the role "Role 1", you will get 2 instead of 1, even though in reality there is only one such role, Character 1.

Solutions for such issues:


* Change count(X) to uniq(X); as shown in the figure above, X can be ID, Name, or Role_ID.

* Check the model relationships, pull out several additional fields from the joined table, and then change the chart type to [Detail Table] to eliminate the interference of aggregated fields or aggregated metrics with the actual row data. This facilitates troubleshooting which fields in the primary table are being split and duplicated due to associations with other fields.

> **For the differences in usage between left join, right join, inner join, and full (outer) join, see** [Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration).


<span id="_2-3-数据集同步失败"></span>
## 2.3 **Dataset synchronization failure**

The dataset frequently fails to synchronize, but there are no errors reported in the model configuration.

The main scenarios and reasons are as follows. Investigate based on the actual circumstances:


* After initially creating the dataset model or modifying the model, an extreme logical model may occur where a small table is nested within a large table, causing the Cartesian product to grow geometrically. This triggers the data expansion detection threshold and the system aborts the process.


Small table nested within a large table means: based on the join field relationship between the left and right tables, the data presents a 1:N mapping, where N \>= 50.

For example, the common Product Type join SKU, or Type join ProductInstance.


* After initially creating the dataset model or modifying the model, an extreme data skew may occur in the logical model, resulting in the distribution of data values in the wide base table being highly skewed. This triggers the threshold during data synchronization and the system aborts the process. For example, in table A, field X has 100 enumeration values numbered 0 to 99, but in the corresponding data, there are 100,000 rows where X = 1 or 2, while other enumeration values have only 1 or 2 rows.

* The business table in the upstream data source has undergone structural changes. The current dataset used to run successfully, but the dataset model was not correspondingly edited, resulting in unsuccessful runs now. The main check is whether the fields in the original dataset have been affected by changes in the source table, such as field type, whether the field exists, field name, and so on. At this point, check the [Log] of the frontend task, which often shows field parsing errors and displays SQL xxxx error log content.

   4. A migration was performed at the source, and the database type of the data source or the connection's IP+port or JDBC was changed; this resulted in dataset synchronization failure. When checking the [Log] of the frontend task, messages such as DataX...Schame.. or Access Deniled are often displayed, indicating errors in obtaining the database connection or a timeout.


<span id="_2-4-数据源字段与数据集字段"></span>
## 2.4 Data source fields and dataset fields

[Data source fields and dataset fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields#d510d1e1)

The name of a data source field must always be the name from the source table and cannot be modified. If duplicate field names appear, the source table name will be automatically appended, in the format: `source field name [source table name]`; \-\-\- Each node in the model retains the data source fields, which are approximately equivalent to the model fields stored in the CK base table.

Dataset fields are derived from data source fields. When a dataset is generated for the first time, fields are automatically generated according to the model, with the name equal to the source field name. However, users are also allowed to add or modify field names and field expressions (that is, to perform YY transformation on the xx source field) in [Field Configuration].

The purpose of dataset fields is to flexibly encapsulate and load the necessary fields into the chart analysis process from the business layer, allowing users to redefine the meaning of data fields or to unify and integrate a set of fields that better align with business BI requirements from the perspective of downstream business BI data warehouses or data marts.

**Due to the above principles, the following situations may occur:** 

A. After the structure of the upstream visual modeling task changes, users may notice that their dataset fields are not automatically updated. This is because the output of visual modeling is linked to the table structure of the downstream direct\-connection dataset in Clickhouse, and does not directly modify the [dataset fields] of the downstream dataset, which are the fields encapsulated and decoupled at the business layer.

B. After the dataset model is updated but before data is resynchronized, existing BI queries based on the dataset can still retrieve consistent data, rather than immediately encountering data unavailability due to the model update.

**Recommendation:** 


* In BI visualization query analysis, use dataset fields whenever possible, and name dataset fields to best reflect their business meaning.

* When adding a new custom field, reference existing dataset fields in the expression to ensure logical consistency and facilitate modification and maintenance. In this way, if the dataset field at the root node changes due to a change in the source table's data source field, you only need to modify the data source field in the first layer of references.


<span id="_2-5-特殊数据格式处理"></span>
## 2.5 Special data format handling

Certain fields with special formats require specific format conversions; otherwise, they cannot be displayed correctly. Common examples include:


* Date\-time values recorded as long integers in Unix16/32 format, which appear as date\-time locally but are displayed as long\-type numbers after being synchronized to DataWind. \-\-\- Use date functions such as toDate, toDateTime, or FromUnix in field editing to handle these cases.

* Time\-type fields in Lark spreadsheets require dedicated format conversion in DataWind:

   toDate((lark_time \* 86400000 \- 2209161600000)/1000

* After dataset field data types are identified directly from the data source, there may be some discrepancies. Manual confirmation and adjustment are required in the dataset's field configuration; otherwise, incorrect aggregation expressions or statistical analyses may occur during chart analysis.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a976f26fe46e424696e3c4ed548a64a4~tplv-goo7wpa0wc-image.image) </span>


* Hive struct\-type fields cannot be directly retrieved and stored as CK fields.


When importing tables with struct\-type fields directly, the common issue is that these fields are identified as unsupported and cannot be stored as CK fields to generate datasets. The solution is as follows: switch to [Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL), and use the select statement to import individual struct elements as separate fields.

As shown in the example below, this approach allows the elements within the struct in the source table that need to be referenced to be converted into independent field columns and stored in the CK dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a78ac0af79d45c69243a3b0fe5f462b~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Compared to the dataset model used by DataWind, there are differences in the functions supported by many databases from different sources. It is necessary to check and confirm in the current standard CK function set; otherwise, errors may occur. For example:

   * For counting unique values, use Uniq() instead of Count Distinct.

   * For date functions such as now() and today(), it is recommended to use now() as a priority. Although ClickHouse syntax supports the today() function, some source databases may only support now(), not today(). Therefore, it is recommended to use now().

   * The dateDiff() function calculates the difference between dates and rounds the result up; this differs from MySQL's timestampDiff, which rounds down.


<span id="_3-可视化建模管理"></span>
# 3. Visual modeling management

**How should this be understood?** 

Visual modeling can be understood as a more advanced and complex data processing capability, providing multidimensional and flexible data preprocessing, cleaning, and aggregation that cannot be achieved in standard datasets. It is essentially a data preprocessing project; once completed, it becomes a pipeline for producing data. After the modeling task completes data synchronization, the raw data is processed through each stage of the project into the final desired dataset, which is a wide table better suited to BI business needs. The output dataset supports both CK and Hive types.

Simply put, the output of visual modeling can be regarded as a lightweight data warehouse. This data can be used directly for BI or as input data for downstream modeling projects.

<span id="_3-1-单元测试法"></span>
## 3.1 Unit testing method

The essence of the unit testing method is to break down large\-scale modeling into unit tests, with each new processing node added only after the previous stage is confirmed to be correct. Try to avoid building all nodes at once and then verifying data synchronization, as this can waste too much time and make troubleshooting difficult. There are two modes for the unit testing method:


* After completing the current node, use preview exploration to analyze the data samples at each stage of the modeling project, determine whether your expectations for data preprocessing are met, and check whether any issues arise at this stage.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/494dbde4fd97499c8ec7cd2b6c5e586d~tplv-goo7wpa0wc-image.image) </span>


* Based on the node at each [connection_xx], after verification, directly link to the output node to construct the output dataset and quickly complete synchronization. Use visual queries of the dataset to verify the data modeling logic. Repeat this process by gradually adding subsequent node steps, adding each new node only after the previous test is completed, until the entire modeling logic is finished. (Note: To avoid excessive synchronization time for single\-step modeling output tests, add certain filtering conditions in the relevant source input nodes, such as region, business date, or category, to restrict the extraction to sample data with specific enumerated values under these conditions. This ensures that a small data volume of fewer than 1,000 records is used for rapid, repeated unit testing, resulting in shorter synchronization times for the required dataset.)


<span id="_3-2-如何避免数据倾斜或数据膨胀"></span>
## 3.2 How to avoid data skew or data inflation

Generally, the more connection nodes there are in a modeling project, the greater the coefficient of data skew or data inflation. This is because the detection mechanism calculates the ratio of data between the source node and the terminal node. When the inflation coefficient exceeds a certain threshold, the system will forcibly terminate the process.

Two optimization strategies:


* Refer to the data processing method for "Logical Issue Two" in the "Dataset Management" section, and avoid data tables or data connection logic with obvious specificity whenever possible.

* Break down complex projects into multiple basic independent modeling projects, first output intermediate datasets separately, then use a new modeling project to combine these intermediate datasets as input nodes to produce the final dataset output.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f3d1c3b47fa4fe69ac423fd83e18d78~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-上游依赖问题"></span>
## 3.3 Upstream dependency issues

Visual modeling allows an existing dataset to be used as an input node, thereby establishing a dependency based on business relationships between two data synchronization tasks. If, during execution, the dataset remains in a waiting state and, after reaching the synchronization start time, its status is found to be 'waiting for upstream readiness', generally, check whether the visual modeling contains the aforementioned dependency.

The most common scenario where a dependency prevents execution is that, within the business date range configured for the current business's dependent upstream task, the upstream task has not completed data synchronization. For example, if the current task depends on the previous day of the upstream task, open the upstream task to check whether the partition data for the previous day has been synchronized.

To have the current modeling data depend on upstream data in a T+0 day (that is, same\-day) mode, a feasible approach is to set both the dependent upstream dataset or modeling and the current modeling as hourly tasks. Otherwise, for daily\-level tasks, the minimum dependency is on T\-1 day (that is, the previous day) data.

<span id="_3-4-自定义-sql-执行报错或者很慢"></span>
## 3.4 Custom SQL execution errors or slow performance

In some scenarios, using custom SQL with complex aggregation logic at the input node can lead to data errors or slow synchronization.

This is because input nodes typically perform local data queries on the source database tables specified via [Data Connection] during data synchronization. For example, a MySQL input node actually executes the engine\-translated MySQL statement on the remote source database, returns the data result to DataWind, and then passes it to downstream nodes for processing until the output dataset is generated.

This process is constrained by the bandwidth of remote communication and the execution efficiency of the source business database. The more complex the processing placed in the synchronization interaction process, the slower the processing speed. (Imagine this: Is it faster to deliver two pounds of raw beef immediately after payment, or to deliver four plates of braised beef after payment?)

Once this point is understood, you can:


* When using custom SQL for input nodes, keep it as simple and efficient as possible. Only query explicit fields, and do not perform aggregation or data cleansing operations. Ensure that the SQL executed at the source is as efficient and straightforward as possible.

* Perform complex aggregation or data cleansing operations in the second layer of modeling or in non\-input node layers.


<span id="_3-5-presto-数据源的建模获取或执行失败"></span>
## 3.5 Modeling acquisition or execution failure for Presto data sources

Data is stored in the enterprise data warehouse, and then integrated using the Presto query engine. When connecting to DataWind, a Presto\-type data connection is configured. Sometimes users may encounter the following issues:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fc10c91c77346d2bc4b870491837f06~tplv-goo7wpa0wc-image.image) </span>

```plain
DataX schema file does not exist or format is incorrect: Failed to retrieve DataX sample: DataX schema file does not exist or format is incorrect: Failed to request DataX service: {"code": 20003, "msg": "[ERR-SQL precompilation exception] Access Denied: Cannot select from columns [banfn] in table or view eban_1d_a","advice":null,"data":null}
```


Generally, the user configured in the current data connection does not have sufficient permissions, and needs to be replaced with a user who has permission to execute SQL. Modify the user and password for the data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1705ba706934d178c5518c1c7288362~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-图表可视化"></span>
# 4. Chart visualization

**How should this be understood?** 

Based on the results of combinations of dimensions, aggregate and calculate all statistical values that satisfy the metric formulas under different conditions, and output them.

<span id="_4-1-维度与指标"></span>
## 4.1 Dimensions and metrics

The fields that affect statistical or computational classification are dimension fields, which correspond to the commonly discussed concept of "what is the statistical dimension". Metrics are scalars, and are always calculated for the range of enumerated values that match the results of dimensions or combinations of dimensions, such as sum, count, and more.

For example: COLOR = red | yellow | blue, SIZE = large | small. If the dimension combination is COLOR + SIZE, and the metric to be calculated is the total number of CarName, that is, sum(CarName), then sum(CarName) will be provided for the following six dimension result distributions:


|COLOR |SIZE |SUM(CarName) |
|---|---|---|
|Red |Large |10 |
|Yellow |Large |20 |
|Blue |Large |14 |
|Red |Small |34 |
|Yellow |Small |11 |
|Blue |Small |8 |


Therefore, when checking whether data statistics are accurate or whether there is duplicate counting, the following points are usually considered:


* Data sampling: Use key classification fields in business data, select one or two enumerated values, and use them to sample and validate the data.

* Fields observed under different conditions must be set as metrics; the system uses different aggregation methods for metrics and dimensions, and numerical calculations apply only to metrics.

* Dimensions directly affect the data distribution of metrics. Metrics are grouped and calculated based on the enumeration values of dimensions, similar to groupby; metrics do not directly affect the distribution of other metrics.

* When there are too many dimensions, data errors or unexpected results may occur. Generally, there are two troubleshooting methods:

   * Using method a, switch the chart to a detail table to check whether metric fields from the primary table are repeatedly calculated after joining with the secondary table. If so, use the key field to remove duplicates.

   * Following the principle of analyzing dimensions from top to bottom and from larger to smaller granularity, gradually add dimensions to analyze the results of metrics step by step, in order to observe at which step the data changes unexpectedly.


<span id="_3-2-函数应用错误怎么办"></span>
## 3.2 What to do when function application errors occur

When a function formula is used to aggregate metric fields for calculation, and no error is reported but the query results do not meet expectations, this is always a logical design error in mathematics, not a function or feature error.

The fastest way to verify in this situation is to write the same processing logic using equivalent formulas in Excel and validate it there. In most cases, if the equivalent logical expression in Excel is consistent with the logic of the CK function, then the results in Excel will be the same as the metric results displayed in the visualization chart. The essence of this approach is to have users return to the data analysis logic to first verify or rule out misunderstandings in data logic or formula usage.

Similarly, solutions can be found in reverse: first identify a formula method in Excel that produces the correct result, then convert this logic into an equivalent DataWind CK function and apply it to the corresponding field.

<span id="_3-3-空值处理"></span>
## 3.3 Null value handling

When handling special null values, sometimes, due to the mechanisms of the source database, certain fields allow null values. Although these fields appear empty when queried in the local database, after synchronization to DataWind, these null values may sometimes appear as "null" and sometimes as empty values when queried. This is due to differences in field formats and data ingestion mechanisms.

Simple detection and preprocessing methods: Use isNull(X) or empty(Y) to test and determine the value. isNull is mainly used to check for NULL values, returning 1 if true, and is often used for counting the number of null rows. The empty function mainly detects empty string values, returning 1 for empty strings and 0 for non\-empty values. It is often used with if statements to handle empty values.

<span id="_3-4-透视表"></span>
## 3.4 **Pivot table**

A pivot table is mainly used for hierarchical or categorical statistics of data with a limited number of dimensions, allowing you to see the proportion or quantity of big data metrics under different levels of classification. It is not intended for presenting the details of row and column dimension combinations.

Many users, upon seeing that a pivot table can display a matrix distribution of row and column dimensions, may find it more visually appealing or layered, and thus use a pivot table to display charts with many dimensions or metric fields similar to a detail table. However, this can lead to very slow data queries. This is because the underlying operation of a pivot table involves aggregation and pivot calculations similar to Order by and Group By. Therefore, when a pivot table is misused to display large volumes of detailed data, the calculation may hang or time out.

Similar to the pivot logic in Excel, only statistical or distribution calculations with fewer than four dimensions are suitable for using a pivot table. For example, when calculating the sales value of products by different cities under each province and by different brand dimensions, a pivot table can be used.

<span id="_3-5-明细表"></span>
## 3.5 **Detail table**

A detail table reflects each specific row of data in the actual wide base table stored in the CK underlying table, eliminating the merging of data rows caused by statistical formulas or metric aggregation. Therefore, in most scenarios, being able to revert to the original data form to examine the structure and characteristics of the synchronized dataset helps us identify our subjective misunderstandings or omissions.

The main purpose is to facilitate reverse analysis of the 'Cartesian product' effect caused by [Join], which leads to the splitting of rows in the original table.

For example: COLOR = red|yellow|blue, SIZE = large|small. If the dimension combination is COLOR + SIZE, and the metric is the total number of CarName, that is, sum(CarName), then the results will be distributed across the following six dimension combinations, providing sum(CarName) for each distribution, as follows:


|COLOR |SIZE |SUM(CarName) |
|---|---|---|
|Red |Large |10 |
|Yellow |Large |20 |
|Blue |Large |14 |
|Red |Small |34 |
|Yellow |Small |11 |
|Blue |Small |8 |


At this point, if you simply count the total number of colors based on column A, you will get a count of 6, whereas in reality, the unique count, which is 3, is more accurate. Alternatively, sometimes the fields split by the Cartesian product include certain numeric metric fields, such as date, money, or score. In such cases, you can use a method combining the detail table and analysis of multiple columns to identify which fields caused the splitting (duplication) of table rows due to multiplication, and then, during metric aggregation, choose to use the average, maximum, minimum, or other methods to avoid the interference of duplicate values.

<span id="_3-6-数据结果空值过多"></span>
## 3.6 Excessive null values in data results

The issue of many rows with null values in data fields generally arises as follows:


* When using an outer join, a large number of rows with null fields are often generated.

* If the source table is a spreadsheet, there may be invisible blank rows, and this issue becomes more pronounced after multiple table aggregations.


<span id="_3-7-筛选与求和逻辑"></span>
## 3.7 Filtering and summing logic

Why do some aggregate metrics or summary statistics change when the filter conditions are modified? Or why do some [analysis] results change and not meet expectations? For example: single product proportion, sales proportion

**Here is an example:** 

This is because, at this point, the logic **is not** to first perform calculations based on the expression logic of dimensions and measures, then filter the results; instead, it first filters the data rows in the dataset according to the fields specified in the filter criteria, and then starts the calculation based on the calculation logic expressed by the dimensions/measures on the page. Therefore, the calculation results for this type of analysis may change.

Similarly, datasets that use row\-level permissions follow the same logic, so special attention must be paid to how you handle aggregation or analysis fields.

One way to handle this is to combine LOD calculations and add a new measure field to store the target calculation result. By using table\-based calculation functions such as Fixed or Exclude, you can generate fixed values, so that this measure field is not affected by filters at the specified field level during queries.

<span id="_4-仪表盘使用"></span>
# 4. Dashboard usage

This section is mainly about graphical design or layout work, which is more about repeated aesthetic adjustments or the accumulation of design experience.

Three aspects need to be specifically clarified:

<span id="_4-1-公共筛选器的理解和运用"></span>
## 4.1 Understanding and applying global filters

The purpose of global filters is to make it easier to apply unified filtering based on a certain field across multiple charts, using a single filter to achieve global filtering. Common issues here include:

Different charts may have fields with the same meaning or name, but their source dataset models are not the same. In this case, global filtering may produce inconsistent results for charts from different datasets. Therefore, it is recommended to group charts from the same dataset together and apply the same global filter.

For chart groups from different datasets, divide them into sections and use different filters for control.

<span id="_4-2-图表联动的运用和配置逻辑"></span>
## 4.2 Application and configuration logic of chart interactivity

In dashboards, a particularly important and unique feature is chart linkage. Common issues include:

a. From a visual perspective, the data linked between the upper and lower charts may appear unrelated, especially when the two charts are based on different datasets. In such cases, it is necessary to carefully analyze the fields used to associate the two charts and check for any data issues (such as consistent formats or whether the data ranges can be matched).

b. It is necessary to analyze whether the data filtering logic between the linked charts is reasonable (this logic is equivalent to formula logic in Excel), such as whether fields need to be combined to obtain correct results, and whether the required fields are included in the current chart; whether the value of a field in the primary chart is used as an index key or a business key in the secondary chart.

c. For the same dataset (especially complex wide\-table datasets), it is necessary to generate charts of different dimensions on this basis, and there should be a causal relationship between the charts, which is suitable for expressing with chart linkage. For charts based on different datasets, since their underlying data models and data content are often inconsistent, chart linkage is of little significance and is not recommended except in special cases.

d. In most scenarios, drill\-down analysis within the same dataset can be implemented using chart linkage. In terms of data representation and repeated analysis scenarios, chart linkage provides a clearer and more explicit expression than drill\-down.

<span id="_4-3-动态参数的使用"></span>
## 4.3 Use of dynamic parameters

Parameters are generally defined at the project level and are divided into public parameters and personal parameters. Common issues include:

When setting parameters, it is necessary to configure the dataset to which they are applied. The principle is that they take effect in the upper\-level chart results of the applied dataset.

Therefore, when referencing parameters in a dashboard and some charts have issues, first check whether the dataset associated with the chart has applied the parameter.

> For construction methods, refer to [Best Practices for Building Dashboards](https://docs.byteplus.com/docs/DataWind/Best_Practices_for_Building_Dashboards).
