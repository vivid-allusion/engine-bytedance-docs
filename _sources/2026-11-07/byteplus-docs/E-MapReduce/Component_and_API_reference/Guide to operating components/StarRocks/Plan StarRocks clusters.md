---
title: "Plan StarRocks clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Plan_StarRocks_clusters"
---

This document describes how to plan resources for a StarRocks production cluster. You need to plan your StarRocks cluster in terms of the number of nodes, number of CPU cores, memory size, and storage size.

<span id="9c26da50"></span>
## Number of nodes

StarRocks mainly consists of two types of components: FE nodes and BE nodes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Each node must be deployed separately on a physical or virtual machine.</div>


<span id="c207e452"></span>
### Number of FE nodes

FE nodes are primarily responsible for metadata management, client connection management, query planning, and query scheduling.

For a StarRocks production cluster, it is recommended to deploy at least three Follower FE nodes to prevent single points of failure. The Leader FE is automatically elected from among the Follower FE nodes.

StarRocks manages metadata across FE nodes using the BDB JE protocol. StarRocks elects one Leader FE node from all Follower FE nodes. Only the Leader FE node can write metadata, while other Follower FE nodes can only update metadata based on the logs of the Leader FE node. If the Leader FE node goes offline, as long as more than half of the Follower FE nodes remain alive, StarRocks will re\-elect a new Leader FE node.

To handle high\-concurrency query requests in your application, you can add Observer FE nodes to the cluster. Observer FE nodes are only responsible for processing query requests and do not participate in the election of the Leader FE node.

<span id="70d02c32"></span>
### Number of BE nodes

BE nodes are responsible for data storage and SQL execution.

For a StarRocks production cluster, it is recommended to deploy at least three BE nodes. These nodes will automatically form a highly available BE cluster to prevent single points of failure from affecting data reliability and service availability.

You can achieve high\-concurrency queries by increasing the number of BE nodes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In a storage\-compute separation cluster, there are no BE nodes; only FE and CN nodes exist.</div>


<span id="0e48aa93"></span>
### Number of CN nodes

CN nodes are optional components in StarRocks and are only responsible for SQL execution.

You can elastically scale computing resources by increasing the number of CN nodes without changing the data distribution in the cluster.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In a storage\-compute separation cluster, only FE and CN nodes exist.</div>


<span id="e4d2fb2f"></span>
## CPU and memory

Typically, FE services do not consume a large amount of CPU or memory resources. It is recommended to allocate at least 8 CPU cores and 16 GB RAM for each FE node.

Unlike FE services, if your application needs to process highly concurrent or complex queries on large datasets, BE services may consume a large amount of CPU and memory resources. Therefore, it is recommended to allocate at least 16 CPU cores and 64 GB RAM for each BE node.

<span id="af2822c5"></span>
## Storage space

<span id="3074705d"></span>
### FE storage

Since FE nodes only maintain StarRocks metadata in their storage, in most scenarios, each FE node requires only 100 GB of cloud storage.

<span id="b6cac6bd"></span>
### Data storage

<span id="40ff7643"></span>
#### Estimate initial BE storage space for integrated compute and storage

The total storage space required by a StarRocks cluster is affected by the size of the raw data, the number of data replicas, and the compression ratio achieved by the data compression algorithm used.

You can estimate the total storage space required for all BE nodes using the following formula:


* Total storage space required for BE nodes = size of raw data \* number of data replicas / compression ratio achieved by the data compression algorithm

* Size of raw data = size of a single row of data \* total number of data rows


In StarRocks, the data in a table is first divided into multiple partitions, and then further divided into multiple Tablets. A Tablet is the basic logical unit of data management in StarRocks. To ensure high data reliability, you can maintain multiple replicas for each Tablet, stored on different BE nodes. By default, StarRocks maintains three replicas.

Currently, StarRocks supports four data compression algorithms: zlib, Zstandard (or zstd), LZ4, and Snappy (listed in order of compression ratio from highest to lowest). These data compression algorithms can provide a compression ratio from 3:1 to 5:1.

After calculating the total storage space, you can simply divide it by the number of BE nodes in the cluster to estimate the average storage space required for each BE node.

<span id="ba53c581"></span>
#### Add extra storage space at any time for integrated compute and storage

If BE storage space is exhausted as the raw data grows, you can supplement storage space by vertically or horizontally scaling the cluster or expanding cloud storage.


* You can add new BE nodes to the StarRocks cluster, thereby redistributing the data across more nodes. After adding new BE nodes, StarRocks will automatically rebalance the distribution of data among all BE nodes. This automatic balancing is supported for all table types.

* You can also expand the storage capacity of existing BE nodes. After adding additional storage volumes, StarRocks will automatically rebalance the data in all tables.


<span id="c5e56726"></span>
#### Storage\-compute separation – unlimited storage space

With storage\-compute separation, all data is stored in object storage (TOS), which can be considered as having unlimited space, so no specific expansion is required. Of course, as your data volume increases, we recommend simultaneously adjusting the disk size used for caching on CN nodes according to your query habits to achieve optimal cluster performance. The recommended cache size is one third of the original data volume, and it can be adjusted based on the query type.
