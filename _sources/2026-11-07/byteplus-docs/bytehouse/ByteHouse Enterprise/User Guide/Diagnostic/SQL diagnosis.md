---
title: "SQL diagnosis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/sql-diagnostic"
---

ByteHouse Enterprise supports SQL diagnostics by collecting slow query logs. It provides multidimensional analyses of performance metrics, trends, and details to help you gain insights into the performance of clusters and instances, accurately identify inefficient queries, and achieve targeted SQL optimization. This function is applicable to database performance bottleneck troubleshooting, periodic system health checks, SQL efficiency analysis for specific business modules, and similar scenarios. This tutorial introduces how to use the SQL diagnosis function.

<span id="23420e0d"></span>
# Feature overview

SQL Diagnosis is a query optimization diagnostic tool provided by ByteHouse. Its main functions include:


* **Slow query collection**: ByteHouse collects all queries, obtains the most time\-consuming queries in the cluster, and generates detailed slow query logs.

* **Diagnostic analysis capability**: Based on data from slow query logs, ByteHouse analyzes trends and detailed data across different dimensions to help you identify inefficient query patterns, optimize resource allocation, and achieve targeted SQL tuning.


The diagnosis items currently supported by ByteHouse include:


|Diagnosis items |Description |
|---|---|
|Insight details ||
|Query Total |Query total for the selected time frame. |
|Number of Successful Queries |Total number of successful queries for the selected time frame. |
|Number of Failed Queries |Total number of failed queries in the selected time frame. |
|Failure Query |It displays the type and quantity of query errors to help you manage them. At the same time, ByteHouse also displays detailed information such as query ID, query content, error logs, CPU usage, memory usage, query duration, the user who submitted the query, and other relevant details, making it easier for you to further understand the specifics of the failed query. |
|Succecc/Failure Query Trend |It displays the proportion of successful and failed queries for the selected time period, making it easier to understand the overall query performance of the current instance. |
|Trends in the Proportion of Time Spent on Queries |It displays the trend of the proportion of total query time accounted for by each query type during the selected time frame. By default, only the proportion of query time for SELECT and INSERT queries is analyzed. |
|DML Analysis ||
|DML Trend |It shows trends in DML query execution counts. By default, only ALTER and INSERT queries are analyzed. |
|DDL Trend |It shows trends in the total number of DDL Query runs |
|Query Analysis ||
|Query Source Ratio&Query Source Trend |It shows the proportion or trends of queries in the `application_name` dimension (the client name from which the query originates). |
|Query Ratio By User&Query Trend By User |It shows the query proportion or trends in the `usename` dimension (the username of the user who runs the query). |
|Loss Top5 ||
|Loss Time Top5 Query |It shows the top 5 queries with the longest execution time. |
|Loss Cpu Top5 Query |It shows the top 5 queries with the highest CPU resource consumption |
|Loss Memory Top5 Query |It shows the top 5 queries with the highest memory resource consumption |
|SQL Fingerprint |For SELECT and INSERT type queries, ByteHouse calculates an MD5 hash value as the SQL fingerprint for each query. You can use this parameter to perform global analysis and identify query modes with significant resource consumption.<br><br>The SQL fingerprint analysis diagnosis displays the top 5 queries by total CPU consumption.<br><br><br>* It queries that differ only in literal values, such as specific numbers or strings, but having the same query structure (template) will have the same hash value (that is, the SQL fingerprint). ByteHouse aggregates the hash values of these query logs and, by calculating their total count as well as total CPU, memory, and usage, identifies from a global perspective types of queries that have a significant impact on system performance.<br><br>* Collection and calculation rules:<br><br>   * By default, only the fingerprints of SELECT and INSERT type queries are collected.<br><br>   * Display indicators include: SQL fingerprint hash value, number of sampled SQL statements, total CPU consumption, total disk read IO (input/output) volume, total disk write IO volume, total memory consumption, total network received IO volume, and total network sent IO volume. |


<span id="9ce0cfa6"></span>
# Caution

Before use, please ensure you have **Cluster Admin** or **System Admin** privileges. If you have not obtained these privileges yet, please contact the administrator for authorization. For details, refer to [Manage user's role privileges](https://docs.byteplus.com/docs/bytehouse/role-management#240df71d).

<span id="502a0e4c"></span>
# Use SQL diagnosis

Log in to the ByteHouse Enterprise Console, click the **Diagnostic** tab at the top, click **SQL diagnostic**, and go to the function page. Select the cluster and time range, click **Diagnosis**, and the system will automatically analyze and display the SQL activity in the current cluster during the specified time range. Various diagnostic items can be used to assist in diagnosing query issues. You can consider your business problems together with diagnostic items to analyze the root cause and take appropriate improvement measures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/926f640f288a4cfb9f924b30776cd4b4~tplv-goo7wpa0wc-image.image) </span>

<span id="7d8a2755"></span>
## **Insight**

**Insight** shows the overall query execution status of the current cluster. You can quickly identify abnormal periods through such diagnostic items, for example,


* If the total number of queries is excessively high, there may be abnormal traffic or a peak business period. Check whether the cluster's load capacity has been exceeded.

* If you notice a sudden increase in the failure rate during a specific period in the Failed Query Trends, you can refer to the details of failed queries to optimize problematic SQL statements in bulk or adjust the cluster resource configuration.

* If you identify long\-running queries within a certain time frame, you can use the Top 5 Query statistics by Time to pinpoint potential slow query bottlenecks.

* ByteHouse also lists the details of failed queries. You can click the Query ID to jump to the query [Query insight](https://docs.byteplus.com/docs/bytehouse/query-insight) page to view the query overview and error details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4b14bc060064b06993fd009eda8f02c~tplv-goo7wpa0wc-image.image) </span>


<span id="73bdadcf"></span>
## DML Analysis

DML Analysis shows the execution trends of DDL and DML in the current cluster, allowing you to monitor operation frequency, identify abnormal fluctuations, and assist in evaluating the impact of metadata changes and data read/write operations on the cluster.


* Monitor DML Trend to understand fluctuations in ALTER/INSERT request pressure.

* You can follow DDL action trends to identify high\-frequency metadata changes (such as a large number of table creations or modifications in a short period), which helps judge the risk of lock contention.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ccf4e08114241e28a652d250b4f8bd2~tplv-goo7wpa0wc-image.image) </span>


<span id="c2529f33"></span>
## Query Analysis

Query AnalysisDisplays the distribution of query sources and users who run queries in the current cluster. You can analyze the sources of query failures by reviewing the trends chart together with the failed query trends.


* By analyzing the distribution of application sources, it is possible to identify the origin of high\-load queries (such as a specific type of connection driver) and determine whether this aligns with business expectations. You can use failed Query trends to analyze the concentration of failures from specific sources.

* If a user is observed to have an excessive number of queries that do not align with actual business requirements, you may investigate whether there is resource abuse or adjust resource quota limits as needed.

* If queries from unexpected sources occur, you can check whether this is due to a configuration error or an abnormal request.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31a151a7abbc4252b8d0049b07a3b6e3~tplv-goo7wpa0wc-image.image) </span>

<span id="2f180459"></span>
## Loss Top5

Consumption analysis provides details on the queries with the longest execution time and those that consume the most CPU and memory resources, and supports SQL fingerprint analysis to help you identify queries that affect system performance.


* Single query diagnosis: Diagnosis items such as time consumption, CPU consumption, memory consumption, and others display the details of the query with the highest consumption for each item. You can click the Query ID to view Query Insights details. Use the Query Insights to optimize this query.

* Aggregate analysis of similar queries: SQL fingerprint analysis summarizes the total consumption of similar queries, enabling the identification of global problems. You can click the Query ID to view Query Insights details. By combining the metrics from SQL fingerprint analysis and Query Insights, you can analyze the behavioral characteristics of such queries. Based on your business needs, conduct targeted problem analysis, identify the cause, and implement targeted optimizations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6551752e70f44ada7704cc5ab91e0d7~tplv-goo7wpa0wc-image.image) </span>
