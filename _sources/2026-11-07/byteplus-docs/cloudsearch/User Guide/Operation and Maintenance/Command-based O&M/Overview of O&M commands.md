---
title: "Overview of O&M commands"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/commands"
---

This topic describes commonly used O&M commands. You can run these commands directly in the console of the visualization tool.

<span id="8254dfd2"></span>
## Cluster


|**Command** |**Description** |
|---|---|
|`GET /_cluster/stats` |Query system information about the cluster, including CPU and JVM information. |
|`GET /_cluster/state` |Query detailed information about the cluster, including node and shard information. |
|`GET /_cat/health?v` |Query the health status of the cluster.<br><br>The cluster health status is expressed by three colors: red, yellow, and green. Each color has its unique meaning.<br><br><br>* Red: indicates that the cluster has unavailable primary shards. In this state, some data becomes unavailable, while other data remains available.<br><br>* Yellow: indicates that all primary shards of the cluster are available, but some replica shards are not assigned. Although all data is accessible, the cluster is not highly available due to the unassigned replicas.<br><br>* Green: indicates that all primary shards and replica shards in the cluster are available. In this state, the cluster is healthy and highly available. |
|`GET /_cluster/health?pretty=true` |Query the health status of the cluster.<br><br><br>* `pretty=true`: specifies the output format.<br><br>* `level=indices`: returns the health status of indices at the same time.<br><br>* `level=shards`: returns the health status of shards at the same time. |
|`GET /_cluster/settings` |Query the settings of the cluster. |
|`GET /_cluster/pending_tasks` |Query the pending tasks of the cluster. |


<span id="99d3258c"></span>
## Node


|**Command** |**Description** |
|---|---|
|`GET /_cat/master?v` |Query information about the master node, including the node ID and host. |
|`GET /_cat/nodes?v` |Query information about all the nodes, including the names, roles, CPU usage, HeapMemory usage, and loads of the nodes. |
|`GET /_cat/nodeattrs?v` |Query the custom properties of all the nodes. |
|`GET /_nodes/stats?pretty=true` |Query the status and detailed information of all the nodes. |
|`GET /_nodes/process` |Query information about processes running on all the nodes. |
|`GET /_nodes/hot_threads` |Query information about tasks executed by threads with high resource consumption. |
|`GET /_nodes//jvm,process,os` |Query information about the JVM, processes, and operating system of the specified node. |
|`GET /_cat/plugins?v` |Query information about plug\-ins installed on all the nodes, including the node names, plug\-in names, and plug\-in versions. |
|`GET /_cat/thread_pool?v` |Query information about the thread pools across all the nodes, including the thread pool names, number of active threads, and task queue sizes. |


<span id="c67d440d"></span>
## Shard


|**Command** |**Description** |
|---|---|
|`GET /_cat/shards?v` |Query detailed information about shards in the cluster. It includes the index name, shard number, shard role (whether it is a primary or replica shard), shard status (including reasons for failed shard assignments), document quantity, and disk usage.<br><br>To query the shard information of a specific index, run the `GET _cat/shards/?v` command. |
|`GET /_cat/allocation?v` |Query the shard assignment of each node in the cluster. |
|`GET /_cat/recovery?v` |Query the restoration process of each shard in the cluster. |


<span id="a8ad08f9"></span>
## Index


|**Command** |**Description** |
|---|---|
|`GET /_cat/indices?v` |Query detailed information about indices in the cluster. The information includes the health status, running status, name, UUID, and numbers of shards, replicas, and documents. |
|`GET _cat/indices/?v` |Query detailed information about a specific index. |
|`GET /_cat/aliases?v` |Query detailed information about aliases of all indices in the cluster. The information includes indices associated with aliases, routing configurations, and filters. |
|`GET /_mappings` |Query information about mappings of all indices in the cluster. |
|`GET //_mappings` |Query information about mappings of a specific index. |


<span id="cfbc75d4"></span>
## Document


|**Command** |**Description** |
|---|---|
|`GET /_cat/count?v` |Query the total number of documents in the cluster. |
|`GET /_cat/count/?v` |Query the total number of documents in a specific index. |
|`GET //_doc/` |Query detailed information about a specific document (specified by the document ID) in the index. |
|`GET //_search` |Query information about all documents in the index. You can add query clauses to match relevant documents. |


<span id="060407dc"></span>
## Snapshot


|**Command** |**Description** |
|---|---|
|`GET /_snapshot/_all` |Query all snapshots in all buckets. |
|`GET /_snapshot//_all` |Query all snapshots in a specific bucket. |
|`GET /_snapshot//` |Query a specific snapshot in a bucket. |
