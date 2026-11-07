---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/clickhouse_basic_usage"
---

This article describes the basic operations for using a ClickHouse cluster.

<span id="_1-前提条件"></span>
## 1. Prerequisites

A Volcano Engine E\-MapReduce (EMR) cluster type that includes **ClickHouse** has been created. See [Quickstart](https://docs.byteplus.com/docs/E-MapReduce/109198) for details.

<span id="_2-环境介绍"></span>
## 2. Environment overview


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. Click the **Cluster List \> Service List \> ClickHouse \> Deployment Topology** tab to access the deployment topology for the ClickHouse component service.

3. Click the ECS ID under the component name (emr\-core\-1 host name) to go to the cloud server instance page, then click the **Remote Connection** button in the upper right corner.

4. Select a remote connection method (ECS Terminal is recommended), enter the relevant cluster authentication information, and log in to the command line environment of the Core instance node in the ClickHouse cluster to perform command line operations.

5. Connect to the ClickHouse cluster using a client

   ```shell
   /usr/lib/emr/current/clickhouse/clickhouse-client
   ```
   


<span id="_2-1-查看集群信息"></span>
### 2.1 View cluster information

```sql
select cluster,shard_num,replica_num,host_address from system.clusters;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_085aa7b261b8cbb121ef9bd68919bbad.png) </span>

As shown in the figure above, the default Cluster name for ClickHouse is **cluster_emr**. This sample cluster has 3 shards, and each shard has only one replica.

<span id="_2-2-查看集群宏信息"></span>
### 2.2 View cluster macro information

```sql
select * from system.macros;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30dcbba5c79e451b94ba096b0c457930.png) </span>

There are three macros in the sample cluster: **cluster**, **replica**, and **shard**. These three macros are automatically added after the EMR cluster is created.

Cluster macros can be considered as variables on the node. For example, the macro **shard** has a value of 1 on this node, while on another node the value may be 2 or 3.

It is important to remember this cluster_name and the names of these three macros, as they will be used in subsequent steps.

<span id="_3-创建数据库"></span>
## 3. Create a database

ClickHouse supports multiple database engines. For specific differences, refer to the [official documentation](https://clickhouse.com/docs/en/engines/database-engines/). The following example uses the default Atomic Engine.

<span id="_3-1-创建单机数据库"></span>
### 3.1 Create a standalone database

Execute the following SQL to create a database named test.

```sql
CREATE DATABASE test ENGINE = Atomic;
```


After creation, run `show databases` to see the test database.

However, note that the above SQL only creates the database on the current node; other shards or replicas will not create the test database.

Therefore, this SQL is a standalone DDL statement.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using ClickHouse, it is important to clearly distinguish whether the SQL being executed is distributed or single\-node. This important note will be repeatedly mentioned in the subsequent procedure.</div>


<span id="_3-2-分布式创建数据库"></span>
### 3.2 Create a distributed database

Distributed SQL requires special table creation statements. To create a database, execute the following SQL:

```sql
CREATE DATABASE test ON CLUSTER cluster_emr  ENGINE = Atomic;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f73776906125aae64bd6f4178142ed9.png) </span>

After executing the SQL, the ClickHouse client will report the execution status for each node. As shown in the figure above, the operation has been completed on all three nodes of the sample cluster.

The syntax for distributed DDL is to append the statement "ON CLUSTER {cluster_name}" after the original single\-node DDL. In an EMR cluster, {cluster_name} is **cluster_emr**

For more information about how to use distributed DDL, refer to the [official documentation](https://clickhouse.com/docs/en/sql-reference/distributed-ddl).

<span id="_4-创建多副本表"></span>
## 4 Create multi\-replica tables

ClickHouse provides multiple table engines, but only the MergeTree series of table engines is recommended for storing data in production environments.

The MergeTree table engine is divided into single\-replica and multi\-replica types:


* Single\-replica engines are named MergeTree, such as MergeTree and ReplacingMergeTree.

* Multi\-replica engines have the Replicated prefix, such as ReplicatedMergeTree and ReplicatedReplacingMergeTree.


Single\-replica engines are not recommended for use in production environments and should only be used for testing.

Therefore, the following usage examples will focus on multi\-replica engines.

In this example, we will create a table named "test_table".

<span id="_4-1-创建本地数据表"></span>
### 4.1 Create a local data table

```sql
CREATE TABLE test.test_table_local  ON CLUSTER  cluster_emr
(
    EventDate DateTime,
    CounterID UInt32,
    UserID UInt32
) ENGINE = ReplicatedMergeTree('/clickhouse/tables/{cluster}/{shard}/test/test_table_local', '{replica}')
PARTITION BY toYYYYMM(EventDate)
ORDER BY (CounterID, EventDate, intHash32(UserID));
```


Note:


1. We create a table with the suffix  **_local**. This table serves as the local table and will actually store ClickHouse data.

2. Use the `on cluster` syntax to execute the DDL in a distributed manner.

3. Specify column information, table engine, partition field, and sorting field.

4. The details of the table engine need to be explained in detail here:

   The syntax for the multi\-replica table engine is as follows: `ReplicatedMergeTree('zookeeper_name_configured_in_auxiliary_zookeepers:path', 'replica_name')`.

   It only requires specifying a ZK path and a replica name, but does not care about their specific values. Therefore, on EMR, we need to standardize the usage of the path and name: The ZK path specification is: /clickhouse/tables/ **{cluster}** / **{shard}** /test/test_table_local:

   Here, /clickhouse/tables/ is a fixed prefix to prevent path conflicts,  **{cluster}** / **{shard}**  are the two macros mentioned above for cluster and shard information, and should be filled in as  **{cluster}/{shard}** . When using macros in the CREATE TABLE statement, curly braces are required. test/test_table_local represents the database and table name, which should be modified as needed according to different databases and tables.

   The replica name specification is:  **{replica}** , simply use the replica macro.

   For more information about table engine usage, refer to the [official documentation](https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/replication).


<span id="_4-2-创建分布式表"></span>
### 4.2 Create a distributed table

Querying a local data table: the query statement will only be executed on the current node, and the data is only a subset. To perform a distributed query, you need to create the corresponding distributed table.

```sql
CREATE TABLE IF NOT EXISTS test.test_table ON CLUSTER cluster_emr
AS test.test_table_local 
ENGINE = Distributed(cluster_emr, test, test_table_local, xxHash32(UserID));
```


Note:


1. Determine the distributed table name and distributed DDL syntax.

2. Specify the distributed table field information. Here, use the AS syntax to directly associate the local data table. CK will automatically read the field information of the data table.

3. Specify the Engine information. The syntax for a distributed table is: Distributed(cluster, database, table, sharding_key)

   * cluster: In this example, it is **cluster_emr**

   * database: Here, it is **test**

   * table: The name of the local data table, that is, **test_table_local**

   * sharding_key: Indicates how the data is distributed. In this example, the hash value of the user ID is used as an example. Users can also use the rand() function for random partitioning.


For more ways to use distributed tables, please refer to [the official documentation](https://clickhouse.com/docs/en/engines/table-engines/special/distributed)

<span id="_5-导入数据"></span>
## 5 Import data

Construct some test data using the Insert statement:

```sql
insert into test.test_table select '2020-02-02 00:00:00', number+1, number from numbers(100);
```


<span id="_6-查询数据"></span>
## 6 Query data

<span id="_6-1-查询行数"></span>
### 6.1 Query row count

```sql
select count(*) from test.test_table;
```


<span id="_6-2-点查询"></span>
### 6.2 Point query

```sql
select * from test.test_table where UserID=10;
```


<span id="_6-3-聚合查询"></span>
### 6.3 Aggregate query

```sql
select UserID, sum(CounterID)  from test.test_table group by UserID ;
```


For more query syntax, see [the official documentation](https://clickhouse.com/docs/en/sql-reference).
