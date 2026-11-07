---
title: "Table creation mode"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/table-creation-mode"
---

ClickHouse was originally a single\-node database, so initially only local tables (usually MergeTree) were needed. As it evolved into a distributed database, the concept of distributed tables and distributed DDL was introduced. To build a table that can be used in a distributed system, it is necessary to create both local and distributed tables and use distributed DDL to build the aforementioned tables.

ByteHouse Enterprise Edition, in historical versions, referred to the original syntax of ClickHouse, requiring the creation of **distributed tables + local tables** using distributed DDL. Starting from version 24.9, ByteHouse Enterprise Edition supports the **Common Table Creation Mode**, allowing the completion of the creation process that historically required two types of tables – distributed and local – through **creating one table**.

Meanwhile, we have retained the **Compatibility Table Creation Mode** for the maintenance of existing databases and tables.

<span id="26ccf225"></span>
## General concepts


* Local Table: A table used for storing local data, typically utilizing the Merge Tree Family engines, like HaMergeTree.

* Distributed Table: A table used for distributing queries and insertion requests, with Distributed as its engine.

* Distributed DDL: Syntax specifying the DDL on each node of the cluster, used by appending `db.table` followed by `on cluster <Cluster Name>` to the DDL. If distributed DDL is not adopted, the DDL can only be effective on the target node of the Query.


<span id="9d464246"></span>
## Differences in table creation modes

<span id="2a4b2a56"></span>
### Conceptual comparison


|Mode |Table creation action |Table status |
|---|---|---|
|Common table creation mode |Create a MergeTree table<br><br>(No distributed DDL required) |A distributed MergeTree table |
|Compatible table creation mode |Create MergeTree table<br><br>Create Distributed table<br><br>(Requires distributed DDL) |Interface:<br><br>A logical distributed table<br><br>Underlying:<br><br><br>* A MergeTree table<br><br>* A Distributed table |


<span id="0bf113d7"></span>
#### Common table creation mode

Like using a MySQL table, add, delete, modify, and query ByteHouse tables, allowing non\-ClickHouse users to quickly start using without changing reliability, supporting:


* No need for on cluster, automatically executes distributed DDL.

* No need to create Distributed tables.


In this mode, the MergeTree table can serve as a complete, distributed\-query\-capable table, which we call **distributed MergeTree table**.

<span id="917cc609"></span>
#### Compatible table creation mode

Compatible with the ClickHouse community version, requires creating both Distributed and Local tables simultaneously.

In this mode, the control plane merges a local table and a distributed table into a Distributed Logical Table, abbreviated as **logical table**; the logical table only exists and is visible on the control service, and does not exist on the engine.

<span id="1f0470f2"></span>
### Basic syntax contrast

Common Table Creation Mode (Supported by New Version)

```SQL
CREATE TABLE db.table (
    id Int8
    ...
) ENGINE = HaUniqueMergeTree()
UNIQUE KEY (id)
ORDER BY id
SETTINGS enable_common_table_mode = 1, // enable_common_table_mode=1 means using common table mode
cluster_name = 'bytehouse_test', // cluster name
sharding_key='cityHash64(id)';
```


Compatible Table Creation Mode (Traditional Method)

```SQL
-- local table
CREATE TABLE db.table_local ON CLUSTER bytehouse_test (
    id Int8
    ...
) ENGINE = HaUniqueMergeTree()
UNIQUE KEY (id)
ORDER BY id;
 
-- distributed table
CREATE TABLE db.table ON CLUSTER bytehouse_test As table_local ENGINE = Distributed(bytehouse_test, db,table_local, cityHash64(id))
```


<span id="a796c1ec"></span>
## Activate common table creation mode

If your account has Administrator permissions, you can activate the "Common Table Creation Mode" in the system backend. After activating this mode:


* The Console can display and use Common table creation SQL statements.

* The command line is still compatible with traditional table creation SQL syntax.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The "Common table creation mode" function cannot be deactivated once activated, please choose carefully based on your business needs.</div>



1. Enter the BytePlus ByteHouse Enterprise Edition Console, click the "Profile" button at the top right corner, and select "System Settings".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82a4ad4c41934a588407616af60d382e~tplv-goo7wpa0wc-image.image) </span>

2. You can:

   1. Click the button on the right side of the cluster to activate "Common Table Creation Mode" for a specific cluster.

   2. Activate "New Cluster Default Common Table Creation", then all newly created clusters will by default use "Common Table Creation Mode".

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddee704bc2ea4ca6b7acbc815e93f1c1~tplv-goo7wpa0wc-image.image) </span>
