---
title: "cluster"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cluster-function"
---

<span id="5015bb5e"></span>
## cluster，clusterAllReplicas
`Cluster` allows access to all shards of the cluster without needing to create distributed tables. Only query one _copy of each shard.
`clusterAllReplicas` function - Similar to `cluster`, but queries all copies. Each _copy in the cluster is used as a separate shard/connection.
:::warning
All available clusters are listed in the system.clusters table.
:::
**Syntax**
```SQL
cluster(['cluster_name', db.table, sharding_key])
cluster(['cluster_name', db, table, sharding_key])
clusterAllReplicas(['cluster_name', db.table, sharding_key])
clusterAllReplicas(['cluster_name', db, table, sharding_key])
```

**Param**

* `Cluster name` – Name of the cluster used to build remote and local server address and connection Param set; if not specified, it is set to `Default`.
* `db.table` or `db`, `table` - Names of the Database and table.
* `sharding_key` - (Optional) Sharding Key. If the cluster contains multiple shards, a specific one needs to be designated.

**Return value**
Data set from the cluster.
**Use of macros**
`cluster_name` can contain macros - replacements within braces. The replacement Values are taken from the macros section of the server configuration file.
Example
```SQL
SELECT * FROM cluster('{cluster}', default.example_table);
```

**Usage and Suggestion**
Using `cluster` and `clusterAllReplicas` table functions is less efficient than creating `Distributed` tables since, in this case, server connections will be re-established for each request. When handling a large number of queries, always create `Distributed` tables in advance and do not use `cluster` and `clusterAllReplicas` table functions.
`cluster` and `clusterAllReplicas` table functions might be useful in the following scenarios

* Accessing specific clusters for data comparison, debugging, and testing.
* For research purposes, querying various ClickHouse clusters and replicas.
* Manual, infrequent distributed queries.
