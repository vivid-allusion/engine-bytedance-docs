---
title: "HaMergeTree"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hamergetree"
---

HaMergeTree is a proprietary engine developed by ByteHouse, offering a high\-availability version of the ClickHouse community's MergeTree engine; **it supports master\-slave data synchronization**. **ByteHouse uses the HaMergeTree engine by default.** 

Compared to the community's ReplicatedMergeTree, HaMergeTree reduces the dependency on ZooKeeper while implementing multiple replicas; a single cluster can support more total tables than the community version (over 10,000).

<span id="架构与原理"></span>
## Architecture and Principles

The HaMergeTree data of each shard will be synchronized with each other, maintaining data consistency, so querying any replica of HaMergeTree within the same shard yields consistent results. When any node in the shard fails, as long as there are still live nodes under that shard, the data remains accessible. After a node fails and is replaced, the data on the new node will also be synchronized by the surviving nodes' HaMergeTree tables.

If the current cluster is in a single\-replica mode, HaMergeTree tables can still be created, but by definition, there is only one replica within the shard, so no data synchronization exists, and this HaMergeTree table behaves like a normal MergeTree table.

It's important to note that data in HaMergeTree across different Shards vary. At this time, a distributed table is needed to aggregate data from different nodes and provide unified returns. For details on the distributed table, refer to [Distributed](https://docs.byteplus.com/docs/bytehouse/distributed).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17ea3cd69c471733abae16953f910925.png) </span>

<span id="建表"></span>
## Create table

<span id="sql-建表"></span>
### SQL create table

The example below only describes how to create a HaMergeTree table; if you directly use SQL to create the table, as best practice, you still need to create a new distributed table. For details, refer to [Distributed](https://docs.byteplus.com/docs/bytehouse/distributed).

```sql
CREATE TABLE [db.]table_name [ON CLUSTER cluster]
(
    name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1] [TTL expr1],
    name2 [type2] [DEFAULT|MATERIALIZED|ALIAS expr2] [TTL expr2],
    ...
) ENGINE = HaMergeTree(
 '/clickhouse/21xxxxxxxx/cluster_name/db_name.table_uuid/{shard}',
 '{replica}'
) -- it is recommended to set it to '/clickhouse/byteplusId/clusterName/databasename.tablename_uuid/{shard}','{replica}'
PARTITION BY toYYYYMM(EventDate)
ORDER BY (CounterID, EventDate, intHash32(UserID))
[PRIMARY KEY expr]
[SAMPLE BY expr]
[TTL expr]
[SETTINGS name=value, ...]
```


<span id="关键参数"></span>
#### Key parameters


* Sorting Key (ORDER BY):

   * To improve query performance, ByteHouse stores data according to the order of the sorting index.

   * The sorting key does not have to be unique. But it cannot be Nullable.

   * It is suggested to select 1\-3 fields that are often used as filters as Click sort by ascend keys; the higher the use frequency, the higher the priority order. When priorities are similar, choose Click sort by ascend indexes with smaller cardinalities in higher order.

   * Partition Field does not have to be a Click sort by ascend index.

* Primary Key (PRIMARY KEY):

   * The index file (.idx) records the relationship between rows and the primary key. It is usually consistent with the Click sort by ascend index and normally does not require additional settings.

   * Primary key must not contain Nullable values. Only one primary key can be chosen for a Table.

* Sampling Field (SAMPLE BY):

   * By default, the first primary key field is used for query sampling. Please refer to the community [Sample by](https://clickhouse.com/docs/en/sql-reference/statements/select/sample/) syntax.

   * Must be one of the sorting indexes / primary keys.

* Partition Field (PARTITION BY):

   * Recommended type: Time type (Date/DateTime). Selecting a time type is considered best practice, and it is advised to convert the DateTime type to Date type via toDate() as the partition key.

   * If there is no need for partitioning, a partition key can be omitted.

   * The partition field cannot be Nullable.

* TTL：

   * Set the data life cycle with the granularity effective at the table level.

   * Data retention time is calculated based on the “partition field”; therefore, setting TTL is not possible for tables without a time\-based partition, and the system will forcibly amend it to retain forever.


<span id="settings"></span>
#### Settings

This part is consistent with the Settings of the [community MergeTree engine](https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/mergetree#settings). If a control panel is used to create tables and default values are adopted, further configuration is not needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using HaMergeTree, set internal_replication to True in the remote configuration file, otherwise two sets of data will be queried.</div>
