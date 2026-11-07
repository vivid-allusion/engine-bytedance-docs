---
title: "Product restrictions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/restrictions"
---

<span id="4aa8cb7f"></span>
## Scenes where ByteHouse is not recommended

In the following scenarios, ByteHouse may not be suitable, and it is recommended to find an alternative product:


* OLTP scenarios, that is, scenarios that must support updates (UPDATE) and transactions. In this scenario, it is recommended to use traditional transactional databases such as MySQL and SQL Server.

* Key\-Value storage, and scenarios where a large number of single\-row queries are used, such as`select * from table where user_id in (xxx, xxx, xxx, ...)`. In this scenario, it is recommended to use Redis or other KV databases.

* Blob or document storage. Elastic Search is recommended for this scenario.


<span id="09beac9e"></span>
## Ways of Using ByteHouse Not Recommended

<span id="a43c0c5d"></span>
### Create table


* **Dual replica clusters. Do not build MergeTree engine tables. It is recommended to create HaMergeTree by default:**  MergeTree does not have high availability and will not use dual replicas. It is recommended to build ByteHouse self\-developed HaMergeTree tables by default.

* **When creating all local tables, create a** \*\*Distributed table: \*\*For details, please refer to [Distributed](https://docs.byteplus.com/docs/bytehouse/distributed). If the Distributed table is not built, the full data of the cluster cannot be queried.


<span id="3109fbac"></span>
### Data import


* Avoid small batch data import. Small batch data import will form a large number of small Parts, resulting in a large amount of system resources consumed by the background Merge task. When it comes to different import methods, the suggestions are as follows:

   * **Avoid single or several rows of data** **`Insert into`**It is generally recommended to insert 100,000 bars at the same time when inserting, and insert one partition at a time.

   * If using Flink docking, configure flink\-connector's`sink.buffer-flush.interval` to 8000 or more, and configure the partition key.

   * If you use Kafka docking, configure `stream_flush_interval_ms` to 8000 or more.


<span id="3608ba33"></span>
### Query


* **Avoid using** **`Select *`**  ** Make a query**. ByteHouse is a column database, and the efficiency of querying all columns is far worse than that of an ordinary row database. Specify as few rows as possible when querying.

* **Avoid queries without Limits or without Partition Fields**. If this restriction is not applied to the query, it will cause the query to scan all rows, resulting in very slow results and blocking other queries.
