---
title: "Query insight"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/query-insight"
---

Query Insight, based on slow query logs and system table data in ByteHouse Enterprise, provides detailed execution information for the current query, including a query overview, execution plan visualization, resource consumption, data tables, error information, and more, helping you quickly locate and identify abnormal query issues. This function is applicable to troubleshooting slow queries, analyzing resource bottlenecks, optimizing SQL performance, and other scenarios. This tutorial introduces how to use Query insights.

<span id="e8063ea3"></span>
# Feature overview

Query metadata is sourced from ByteHouse slow query logs. By default, all queries are collected to identify the top time\-consuming queries in the cluster. Query insight displays the query execution plan, resource consumption, tables read and written, and other related information.


* **Query overview**: It displays the basic information of the query, collected from the slow Query log, including Query ID, state, SQL, parameter configuration, cluster, submitter, client address, start/end time, elapsed time, SQL type, and other information. You can quickly view the Query execution status through the Query overview.

* **Execution plan visualization**: It displays the logical and physical execution plans, and visualizes the plan field from the slow query log. You can analyze SQL operator costs by analyzing the execution plan for query rewrite optimization. For more information about Run Plans, see [Execution plan EXPLAIN](https://docs.byteplus.com/docs/bytehouse/execution-plan-explain).

   * **Logical execution plan**: This plan is enabled and displayed by default. It shows the abstract execution plan generated during query execution and describes the logical steps and data flow of query execution.

   * **Physical Execution Plan**: The physical execution plan includes real execution\-time statistics; however, enabling it affects query performance, so it is not recommended to set it as enabled by default. If needed, you can enable this by adding the parameter `log_segment_profiles=1` in SQL and rerunning the SQL statement, or refer to adding the `log_segment_profiles=1` parameter in User Parameters as described in [Configure user parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters#a343f25c). Examples of how to add parameters in SQL are as follows:

      ```SQL
      SELECT xxx FROM sample_db.sample_table
      SETTINGS log_segment_profiles=1; 
      ```
      

* **Resource consumption**: Shows the resource consumption during query execution, collected from the slow query log, including the number of bytes and rows for write and write\-back operations, CPU consumption, memory consumption, cache consumption, and so on. You can use this information to determine whether the query is using too many resources, reading too much data, or encountering similar issues.

* **Table**: Shows the tables involved in Query read and write operations. You can use this information to identify table design or index optimization points.

* **Error information**: When the Query Run State is set to Failed, ByteHouse will display error information, including error codes, reason for error, and other information. You can improve the efficiency of troubleshooting and fixing issues by using error information.


<span id="e2450431"></span>
# Caution

Before use, please ensure you have **Cluster Admin** or **System Admin** privileges. If you have not obtained these privileges yet, please contact the administrator for authorization. For details, refer to [Manage user's role privileges](https://docs.byteplus.com/docs/bytehouse/role-management#240df71d).

<span id="5be8dcfb"></span>
# Before you begin

Obtain the Query ID you need to search for. You can log in to the ByteHouse Enterprise Console, select the target cluster, click **Data query**, and view and copy the query ID in **History**. You can also click the **SQL analyze** button in the Query row, and the system will directly jump to the corresponding query insight details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09c09cfe0e9c492297d11d7855e3408b~tplv-goo7wpa0wc-image.image) </span>

<span id="f8fb7962"></span>
# Procedure


1. Log in to the ByteHouse Enterprise Console, click the \*\*\*\* **Diagnostic** tab at the top, click **Query insight**, and go to the feature page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74cf8a0f5c054cd4acc69feb393ead13~tplv-goo7wpa0wc-image.image) </span>

2. Select the cluster, enter the Query ID, and click **Insight**. The system will automatically generate a detailed analysis for the current query, including the SQL statement used, Executions, Resource, Table, and other information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92c2570552e24f0aa80e4c0d1d2153d6~tplv-goo7wpa0wc-image.image) </span>

   If the status of your query is Failed, the system will display an error message. You can use the query and error message together to troubleshoot and resolve the issue.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1365f86d746b45aba415b21bbbcb8c8c~tplv-goo7wpa0wc-image.image) </span>


<span id="c844fd05"></span>
# Related reference: the query_log system table

Query Insights is built based on the query_log System table. For information about the query_log System table, see [query_log](https://docs.byteplus.com/docs/bytehouse/query_log).
