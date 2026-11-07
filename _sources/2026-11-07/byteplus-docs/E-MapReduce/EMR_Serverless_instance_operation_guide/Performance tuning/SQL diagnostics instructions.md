---
title: "SQL diagnostics instructions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/SQL_diagnostics_instructions"
---

The SQL diagnostics feature automatically collects and stores the Query Profiles of all slow queries and failed queries, and supports retrieving historical query records through the frontend interface using multiple criteria. After selecting a specific query, the SQL diagnostics feature provides query details, statistical data for each operator, a visualized query plan, and automatically generated query diagnostic and optimization suggestions.

The SQL diagnostics feature automatically records the Query Profiles of all slow queries and failed queries. Records from up to the past 30 days and a maximum of 50,000 queries will be saved.

<span id="d55c3737"></span>
# **Limits**

Only StarRocks instances support the SQL diagnostics feature.

<span id="fcb35e82"></span>
# Access and activation methods

<span id="_1-1-进入sql诊断页面"></span>
## **Access the SQL diagnostics page**


1. Log in to Volcano Engine and go to the EMR Serverless OLAP console.

2. Click the instance list, select the StarRocks instance you want to view, and enter the instance details page.

3. Click the SQL diagnostics tab on the left.


<span id="_1-2-sql诊断自动收集参数"></span>
## **SQL diagnostics automatic collection parameters**

The SQL diagnostics feature automatically records two types of queries:


* Slow queries that take 5 seconds or longer,

* Failed queries.


You can use the Session variable `auto_profile_slow_query_threshold_ms` to:


* Adjust the threshold for slow queries,

* Completely disable automatic collection of slow queries:

   * When `auto_profile_slow_query_threshold_ms` is set to \-1, automatic collection is disabled.

   * When `auto_profile_slow_query_threshold_ms` is set to 0, information for all queries is collected.

   * When `auto_profile_slow_query_threshold_ms` is greater than 0, slow queries with execution time exceeding the configured value are automatically collected.


For example, `set global auto_profile_slow_query_threshold_ms= 10000` changes the setting to automatically record slow queries that take 10 seconds or longer. The `global` keyword applies the setting globally.

You can use the Session variable `enable_profile` together with `auto_profile_slow_query_threshold_ms` to collect the Runtime Profile information of specific queries, store it, and display it in SQL diagnostics. For example, temporarily configure any query and record it in query diagnostics:

```bash
set enable_profile=true;
set auto_profile_slow_query_threshold_ms=0;
```


In this example, auto_profile_slow_query_threshold_ms is set to 0, so all queries in this session are collected, including those that take less than 5 seconds. To readjust the threshold for recording slow queries, simply change `auto_profile_slow_query_threshold_ms` back to its default value.

<span id="_2-sql诊断界面"></span>
# Interface description

<span id="_2-1-查询监控图"></span>
## **Query monitoring chart**

The query monitoring chart displays the distribution of the top 100 queries by execution time, making it easy to quickly identify long\-running queries.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66e23e8b57d77ab8700cf1b3b5064bca.png) </span>

<span id="_2-2-sql列表"></span>
## **SQL list**

The SQL list shows various basic information about queries and allows searching by different criteria. Click the query ID to enter the query details page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d66e59e0fd70b7205d236fc4fb55bc6.png) </span>

<span id="_2-3-查询详情页"></span>
## **Query details page**

<span id="_2-3-1-查询概述"></span>
### **Query overview**

The query overview displays detailed information about the query, such as the start time, executing user, SQL text, and other information.

If the query fails, the reason for the failure is also displayed. Execution time and Profile information for failed queries may be missing or incomplete.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86a9d59a44c6d0917d3fb2d38fdb095d.png) </span>

<span id="_2-3-2-计划可视化"></span>
### Plan visualization

SQL diagnostics can visualize your Query Profile.

The plan visualization page includes a node tree displayed as a tree diagram on the left and a details panel on the right.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a838f58b40ffbf58529169cfa4cbf9fa.png) </span>

<span id="18ae828a"></span>
#### **Node tree**

The query plan consists of multiple Operator nodes, each representing an Operator. Data flows from bottom to top, starting from the data source, processed layer by layer by intermediate operators, and finally returned by the topmost operator to the client or written to another data source.

Each node displays the Operator's name, node ID, brief information, number of rows processed, and CPU time consumed.

By selecting the top right option to sort by row count or time consumed, you can change the percentage display rule for Operators, helping you identify the Operator with the longest execution time or the most data processed and pinpoint the query bottleneck.

Operators are grouped according to their respective Fragments. Data flow between Fragments is accomplished over the network. Different Fragments also mean that these Operators belong to different scheduling tasks and may have different degrees of parallelism.

<span id="ac562357"></span>
#### **Details panel**

When no node is selected, the details panel on the right displays detailed information at the Query level.

When an Operator node is selected, the details panel on the right displays all metrics for that Operator, as well as metrics for the Pipeline to which the operator belongs.

When a Fragment node is selected, the details panel on the right displays all metrics for that Fragment.

<span id="_2-3-3-原始-runtimeprofile"></span>
### **Original RuntimeProfile**

SQL diagnostics collect the RuntimeProfile of StarRocks, analyze and process it, and obtain query information. Finally, a visualization page is generated, providing diagnostic results and recommendations.

The original RuntimeProfile displays the original RuntimeProfile information of StarRocks. If certain information is missing from the Profile visualization interface, you can search for it in the original RuntimeProfile.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cdd067a1750255083afda2a0ba83fe2.png) </span>

**Reference**


* View and analyze [Query Profile](https://docs.starrocks.io/zh/docs/administration/query_profile) in StarRocks.


<span id="_3-查询诊断"></span>
# Query diagnostics

Query diagnostics automatically analyze various query metrics to help you identify common errors in queries, locate potential performance bottlenecks, and provide diagnostic recommendations. Diagnostic recommendations are displayed on the corresponding Node in the Profile visualization page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_75b43730eb9cf5fa9afcbbf1a6c3dd06.png) </span>

<span id="_3-1-tablescan-缺少有效的裁剪"></span>
## TableScan lacks effective pruning

StarRocks can skip unnecessary parts of the table based on query filter conditions, reducing the amount of data scanned. When the amount of data scanned by the table exceeds the actual number of required rows, this is referred to as TableScan lacking effective pruning.

TableScan lacking effective pruning is usually caused by incorrect table structure or the absence of effective indexes, which prevents storage from filtering data using query conditions. It may also occur when query conditions contain complex functions that cannot be used to filter data.

The results of query diagnostics are not always accurate. The pruning and filtering conditions that storage can achieve are different, and only part of the scan volume can be reduced. The effectiveness depends on the amount of data, correct table structure and indexes, as well as the query conditions and actual data. In addition, different conditions have different filtering effects and may be suitable for different table structures and indexes.

**Recommendation**


* Check whether the table structure is correct.

* Check whether the sort key is appropriate.

* Check whether indexes need to be added.

* Check whether query conditions contain functions that prevent data from being filtered.


**Reference**


* Understand StarRocks [table design](https://docs.starrocks.io/zh/docs/table_design/StarRocks_table_design).

* [Sort keys and prefix indexes](https://docs.starrocks.io/zh/docs/table_design/indexes/Prefix_index_sort_key/)


<span id="_3-2-tablescan-扫描数据倾斜"></span>
## TableScan data skew

StarRocks distributes data across different storage nodes. If the distribution field is incorrect, data stored on each node may also be uneven. This ultimately results in some nodes needing to scan more data during data retrieval, causing query tail latency.

**Recommendation**


* Check whether the bucket key is appropriate.


**Reference**


* Select an appropriate [bucket key](https://docs.starrocks.io/zh/docs/table_design/Data_distribution).

* Use the official StarRocks table analysis tool, [download tools-20230413.tar.gz](https://starrocks-public.oss-cn-zhangjiakou.aliyuncs.com/tools-20230413.tar.gz).


<span id="_3-3-tablescan-读取字段个数较多"></span>
## TableScan reads too many fields

StarRocks is a columnar storage engine by default. Reading a large number of fields consumes more IO resources.

**Recommendation**


* Remove unnecessary fields from SQL.

* Consider splitting the query into multiple queries, each handling different columns.


<span id="_3-4-join-结果膨胀"></span>
## Join result expansion

With appropriate Join conditions, the number of output rows from a Join will be less than or equal to the number of input rows. If the number of output rows from a Join exceeds the number of input rows, it will consume more computing and memory resources, resulting in slower queries.

Join result expansion is usually caused by missing Join conditions, resulting in a Cross Join, or incorrect Join conditions that cause one record in a table to match multiple records in another table. In some cases, missing statistics or expired statistics after data changes can cause the optimizer to select an incorrect plan.

**Recommendation**


* Check whether Join conditions are missing, add more query conditions, and avoid Join result expansion.

* The columns used in Join conditions should preferably use simple types such as INT or DATE.

* Check whether statistics have been collected or have expired.

* If performing a multi\-table Join, check whether the Join order is correct. If not, you can set the session parameter `disable_join_reorder` to manually adjust the Join order in the query.


**Reference**


* [Statistics collection task](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/ANALYZE_TABLE/).


<span id="_3-5-join-右表过大"></span>
## Join right table is too large

StarRocks Hash Join builds a hash table in memory using the right table. If the right table is too large, it will consume more memory resources.

A large Join right table may be caused by complex Join conditions or associated queries that prevent the optimizer from optimizing the order, such as FULL OUTER JOIN. It may also be due to missing statistics or expired statistics after data changes, causing the optimizer to select an incorrect plan.

**Recommendation**


* Check whether statistics have been collected or have expired.

* Set the session parameter `disable_join_reorder` to manually adjust the Join order in the query.


<span id="_3-6-join-不应该使用广播"></span>
## Join should not use broadcast

StarRocks is a distributed engine. Join operations require redistributing the data of both tables to the same nodes based on the join conditions. If the right table is much smaller than the left table, Broadcast Join can broadcast the right table to all nodes, avoiding redistribution of the left table. Although some data is duplicated, overall network transmission overhead is reduced.

In certain cases, the lack of statistics or expired statistics after data changes can cause the optimizer to incorrectly estimate the size of the table, resulting in Broadcast Join being used even for large tables, which leads to a large amount of data being broadcast. Broadcasting large amounts of data not only increases network transmission overhead, but also increases the volume of data to be processed.

**Recommendation**


* Add the hint `[shuffle]` after the JOIN keyword to restrict the use of Broadcast Join. For example: `select a.x, b.y from a join [shuffle] b on a.x1 = b.x1`


<span id="_3-7-join-应该使用广播"></span>
## Join should use broadcast

StarRocks is a distributed engine. Join operations require redistributing the data of both tables to the same nodes based on the join conditions. If the right table is much smaller than the left table, Broadcast Join can broadcast the right table to all nodes, avoiding redistribution of the left table. Although some data is duplicated, overall network transmission overhead is reduced.

**Recommendation**


* Add the hint `[broadcast]` after the JOIN keyword to enable Broadcast Join. For example: `select a.x, b.y from a join [broadcast] b on a.x1 = b.x1`


<span id="_3-8-aggreagte-聚合度低"></span>
## Aggregate has low aggregation degree

StarRocks is a distributed execution engine. Aggregation operations are first performed locally to reduce network transmission.

If the aggregation operator is relatively complex, local aggregation may not reduce the data, which not only fails to decrease network data transmission, but also consumes a large amount of computing resources.

**Recommendation**


* Disable two\-stage Aggregate by setting the session parameter `set new_planner_agg_stage = 1`.


<span id="_3-9-fragment-处理数据量倾斜"></span>
## Fragment data processing skew

StarRocks is a distributed execution engine. Each fragment is split into multiple instances that execute on different BE nodes. If the source table data is skewed, or the data itself has a certain distribution, it can cause uneven data processing across nodes, resulting in long\-tail latency and affecting query performance.

**Recommendation**


* Refer to TableScan for data scan skew and check whether the table structure is reasonable.

* Check whether there is a large amount of abnormal data in the business data, such as null values, which can cause uneven distribution. Use filtering conditions to pre\-filter such data.


<span id="_3-10-查询返回客户端的数据量较大"></span>
## The amount of data returned to the client by the query is large

Returning large amounts of data through the client will consume considerable FE resources.

**Recommendation**


* Add LIMIT or more filtering conditions.

* Export data to other systems using a data export tool to avoid querying directly from the client.


**Reference**


* Use [EXPORT](https://docs.starrocks.io/zh/docs/unloading/Export) to export data.


<span id="_3-11-查询生成的fragment个数较多"></span>
## The number of fragments generated by the query is large

Overly complex queries consume significant computing and network resources, which may affect the performance of other queries.

**Recommendation**


* Use ETL tools such as Flink to preprocess data and reduce the number of joins in queries.


<span id="_3-12-查询消耗的内存资源较大"></span>
## The query consumes a large amount of memory resources

The query occupies a large amount of memory, which may affect the performance of other queries.

**Recommendation**


* Reduce the number of Aggregate and Sort operators.

* Use a larger\-scale cluster.


<span id="_3-13-查询读取的数据量较大"></span>
## The query reads a large amount of data

The query occupies a large amount of I/O resources, which may affect the performance of other queries.

**Recommendation**


* Check whether the table structure is correct or if there are missing valid indexes.

* Add more filtering conditions, or check whether the existing query conditions can be used for TableScan pruning.

* Use a larger\-scale cluster.
