---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/materialized-view-overview"
---

<span id="1e580cfd"></span>
# Definition of materialized view features

In the ByteHouse database, in addition to **Normal Views**, there is also **Materialized Views.** 


* **Normal Views** do not actually store data and **do not occupy storage space.**  They are just data retrieval operations and can be seen as a saved SQL query statement.

* **Materialized Views** store the data included in the SQL query statements and **provide an update mechanism.**  Using materialized views to replace direct queries on data tables can avoid re\-computation and aggregation of data, saving query time and simplifying query logic by trading space for time.


The working principle of materialized views is based on query rewrite mechanisms and data updates. The query rewrite mechanism is transparent to applications, with the database engine optimizer automatically selecting appropriate materialized views for query rewriting without modifying the original query statements. Additionally, materialized views offer an automatic refresh mechanism to ensure data timeliness and accuracy.

In big data environments, materialized views are particularly suited for data warehouses and query engines where complex queries are frequently performed. They improve query efficiency by trading space for time, simplify the query logic, and significantly reduce the resource consumption of complex queries on large tables. As an accelerator for data queries, materialized views greatly enhance data analysis efficiency while maintaining data real\-time. They optimize the processing of large\-scale complex queries in data warehouses, enhancing the overall data analysis experience.

In summary, materialized views enhance database query performance by pre\-computing and storing query results, combined with automatic query rewriting and data update mechanisms, providing strong support for complex query scenarios in big data environments without altering original query statements.

<span id="450fc160"></span>
## Basic concepts


* **Base Table** \- The driving table for materialized views, supports joins and subquery for multi\-table association queries in asynchronous materialized views.

* **Target Table** \- The actual storage table for materialized views, generally AggregateMergeTree or MergeTree.

* **Materialized View** \- The logical concept defining the mapping relationship from base table to target table.

* **Refresh** \- After creating a materialized view, the data it contains only reflects the state of the base table at the moment of creation. When the data in the base table changes, it is necessary to refresh and map the queries from the base table through the view to the destination table.

* **Query Rewrite \-**  Query rewrite refers to the automatic determination by the system to reuse precomputed results from materialized views when querying the base table that has been built with materialized views. If reuse is possible, the system will directly read precomputed results from the relevant materialized views to avoid redundant computations that consume system resources and time.


<span id="81ed91ce"></span>
## Types of materialized views


|View type |Single\-table aggregation |Multi\-table association |Query rewriting |Refresh strategy |Data import impact |
|---|---|---|---|---|---|
|Asynchronous materialized view |Yes |Yes |Yes |Asynchronous Refresh<br><br>Manual Refresh |None |
|Sync Materialized View |Yes |No |Yes |Import Sync Refresh<br><br>Manual Refresh |Yes |


<span id="27efc31d"></span>
### Synchronous materialized view

Characteristics:


* High data timeliness: When the source table data changes, the materialized view is immediately updated.

* Strong consistency: Ensures consistency between the source table data and the materialized view data.

* Write latency: May increase the write latency of the source table.


Advantages:


* Data is always kept up\-to\-date, suitable for scenarios requiring real\-time accuracy.

* When querying, you can ensure access to the latest data.

* Suitable for situations with relatively small amounts of data and not very high update frequencies.


<span id="6db6bf9b"></span>
### Asynchronous materialized view

Characteristics:


* Asynchronous updates: Changes in source table data and materialized view updates are separated.

* Low latency: There is almost no impact on the writing to the source table.

* Eventual consistency: Materialized view data may experience brief delays.


Advantages:


* Minimal impact on write performance to the source table, suitable for high\-concurrency write scenarios.

* Supports more complex view query formations; query rewrite matching supports more scenarios.

* Allows better control over resource usage to avoid performance issues during peak periods.

* Suitable for large\-scale data processing, especially in data warehouses and analytical systems.

* Flexible adjustment of refresh strategies through configuration parameters, balancing timeliness and system load.


Overall, synchronized views and asynchronous views each have their advantages and applicable scenarios. Choosing the type of materialized view depends on specific business needs, data characteristics, and system resource situations. In practical applications, both types of views may be used simultaneously to meet different requirements.
