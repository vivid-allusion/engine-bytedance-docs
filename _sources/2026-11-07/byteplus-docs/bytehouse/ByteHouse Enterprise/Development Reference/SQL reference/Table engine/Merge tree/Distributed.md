---
title: "Distributed"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/distributed"
---

When using the HaMergeTree table engine, ByteHouse’s data shards need to be used in conjunction with the Distributed table engine.
The Distributed table engine itself does not store any data; it acts as a proxy layer for the distributed table, automatically handling writing, distribution, querying, and routing within the cluster.
<span id="架构与原理"></span>
# Architecture and Principles
![Image](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9bd086868b72d41c7c8449923afa6271.png =793x)
As can be seen from the diagram above, a table is divided into two parts:

* Local table: Usually named with an `_local` suffix. The local table serves as the carrier for data and can use any table engine that is not Distributed. We recommend using HaMergeTree or HaUniqueMergeTree.
* Distributed tables: Typically named directly after the business table, distributed tables can only use the Distributed table engine. They form a one-to-many mapping relationship with local tables and are operated through a distributed table proxy to manage multiple local tables.

To make every node in the cluster searchable, it is also necessary to create a distributed table on each node. Therefore, for a business table, it is necessary to create a separate distributed table and a local table on each node. The architecture is as follows:
![Image](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec1700c306040f7f71cfa94d56353d7c.png =764x)
<span id="分布式表的查询"></span>
## Query of distributed tables
When distributed tables perform a query operation, they query each shard sequentially and then consolidate the results before returning.
<span id="分布式表的写入"></span>
## Writing to distributed tables
When writing to distributed tables, data is first written locally, calculated based on the shard key to determine which nodes to send to, establishes remote connections, and then distributes to these nodes.
However, this approach has some drawbacks:

1. Part synchronization issue: After receiving data, distributed tables split the data into multiple parts and forward it to other servers, which increases network traffic between servers, increases server workload due to merging, slows down the writing speed, and increases the likelihood of having too many parts.
2. Data consistency problem: Data is first written to the disk on the machine where the distributed table is located and then sent asynchronously to the machines where the local tables are located for storage, without any consistency checks. Moreover, if the machine with the distributed table crashes, there is a risk of data loss.
3. Data writing is default asynchronous, which may lead to inconsistencies in a short amount of time.

Therefore, ByteHouse recommends: Insert into local tables, read from distributed tables. Do not directly insert into Distributed tables. Of course, this requires the business to split the data according to the Shard Key before writing, so it can be inserted into different Local tables respectively.
<span id="建表"></span>
# Create Table
<span id="通过-sql-建表"></span>
## Create a table using SQL
Examples of create table statements for distributed tables are as follows:
```sql
CREATE TABLE [IF NOT EXISTS] [db_name.]table_name ON CLUSTER clustern(
  name1 [type] [DEFAULT|MATERIALIZED|ALIAS expr],
  name2 [type] [DEFAULT|MATERIALIZED|ALIAS expr],...
) ENGINE = Distributed(cluster,database,table,[sharding_key])
[PARTITION BY expr]
[ORDER BY expr]
[PRIMARY KEY expr]
[SAMPLE BY expr]
[SETTINGS name=value, ...]
```


* Cluster: Cluster name, which corresponds to the custom name in the cluster configuration. During write and query operations on the distributed table, it uses the cluster's configuration information to locate the corresponding nodes.
* Database: Corresponding Database name
* Table: Corresponding Table name,
* sharding_key: Sharding key, an optional parameter. During the data writing process, the distributed table distributes the data across the nodes where the local tables reside, according to the rules of the sharding key. A further description about sharding rules: the sharding key requires returning an integer type value, including series of Int and UInt types.

Sharding key usage example:
```sql
-- The sharding key can be a specific integer field.
-- Divide according to the user ID.
Distributed(cluster, database, table, userid) -- The sharding key can also be an expression that returns an integer value.
-- Divide according to a random number.
Distributed(cluster, database, table, rand())-- Divide according to the hash value of the user ID. 
Distributed(cluster,database,table,intHash64(userid))
```
