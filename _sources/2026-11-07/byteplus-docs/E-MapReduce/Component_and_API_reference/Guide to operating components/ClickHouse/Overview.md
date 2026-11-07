---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/clickhouse_overview"
---

Clickhouse is a distributed, real\-time, analytical columnar database product that can deliver query results with sub\-second response times, enabling efficient real\-time data analysis. It is widely used in business scenarios such as user behavior analysis, traffic and monitoring, user profiling, and real\-time BI reports.

<span id="_1-clickhouse-功能特点"></span>
## **1 Clickhouse feature highlights**


|Features |Note |
|---|---|
|**Columnar storage** |Clickhouse stores data in columnar format both in memory and on disk. Compared to row\-based storage, columnar storage delivers better performance for analytical queries. Additionally, columnar storage achieves higher compression ratios, saving more storage space. |
|**Vectorized execution** |Clickhouse uses a vectorized execution model. All operators are developed in a vectorized manner, enabling the use of the CPU's SIMD instruction set for more efficient CPU utilization. |
|**Multiple table engines** |Clickhouse offers multiple table engines and supports various MergeTree table engines. For example, ReplicatedMergeTree enables highly available MergeTree tables with multiple replicas, AggregatingMergeTree supports MergeTree tables with data pre\-aggregation, and ReplacingMergeTree allows real\-time updates and deduplication for MergeTree tables.<br><br>In addition to the MergeTree series of table engines, Clickhouse also supports engines such as MySQL, Hive, and Kafka. |
|**Materialized view** |Clickhouse supports real\-time materialized view functionality. After creating a materialized view, when new data is inserted into the base table, the materialized view can also be updated in real time.<br><br>This feature is commonly used to pre\-aggregate detail tables and write the data into AggregatingMergeTree. Queries directly read the pre\-aggregated data, accelerating query performance. |
|**Multiple access methods** |Clickhouse supports multiple access methods. Typically, Clickhouse\-Client is used for query operations, and JDBC can be used for remote connections.<br><br>Clickhouse also supports graphical client connections, such as Tableau and Superset. |
|**Multiple indexes** |Clickhouse supports primary key indexes and secondary indexes. When storing data, Clickhouse sorts by primary key and creates a minmax index on the primary key, enabling ClickHouse to search for specific values or ranges within tens of milliseconds. The types of secondary indexes are more diverse, supporting minmax, set, ngrambf_v1, tokenbf_v1, and bloom_filter. |


<span id="_2-架构说明"></span>
## 2 Architecture note

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f979bd8e88a24d109a124e8250cc9598~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, this ClickHouse cluster contains a total of 2\*N Clickhouse nodes, paired as replicas, and divided into N shards. The meaning of N shards is that data is partitioned into N segments based on the function value of the shard key, and the data is distributed relatively evenly across these N shards.

Within the same shard, data is simultaneously stored in Replica0 and Replica1. Newly inserted data is written to only one replica, and the Clickhouse engine automatically synchronizes the data to the other replica.

Clickhouse supports hot and cold data tiering. Hot data can be stored on the local cloud disk of ECS, offering faster query performance, while cold data is stored in remote object storage TOS, providing lower storage costs.

Clickhouse supports Client and JDBC access. You can choose multi\-node access mode, or bind these nodes to ELB and access them by connecting to ELB.

For more information, refer to [Clickhouse official website](https://clickhouse.com/docs/en/intro/).
