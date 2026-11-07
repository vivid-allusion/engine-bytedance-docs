---
title: "Kudu overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Kudu_overview"
---

Kudu is a distributed, scalable columnar database that can simultaneously provide low\-latency random read and write operations as well as efficient data analytics capabilities. Kudu supports horizontal scaling and uses the Raft protocol to ensure consistency.

<span id="_1-使用场景"></span>
## 1 use cases

The common use cases are as follows. Depending on your business scenario, you may consider prioritizing Kudu:


* Millisecond\-level primary key updates and deletions.

* Sub\-second query analytics (requires integration with compute engines such as Impala or Presto).

* Not suitable for high QPS key\-value queries.


<span id="_2-组件"></span>
## 2 components

<span id="_2-1-master-server"></span>
### 2.1 Master Server

The master node of Kudu is responsible for metadata management and service coordination for the entire cluster.

It performs the following functions:


* Manages the schema and other metadata for all tables and tablets in the cluster.

* Tracks the liveness of all server nodes and coordinates data redistribution when a server node fails.

* Tracks the location of each tablet.


<span id="_2-2-tablet-server"></span>
### 2.2 Tablet Server

Used to store tablets. Tablets can be configured with multiple replicas, and the Raft protocol is used to ensure consistency among replicas.

<span id="_3-基本概念"></span>
## 3 basic concepts


|Name |Description |
|---|---|
|Catalog Manager |The master node of Kudu holds a single\-tablet table—the catalog table—which is not directly accessible to you. The master writes internal catalog information to this tablet and caches the entire catalog in memory. |
|Tablet Directory |The client caches the location information of the tablets it needs to access locally, so it does not need to retrieve it from the master for every read or write operation. Since the location of a tablet may change (for example, if a tablet server node crashes), when the location changes, the client receives a notification and then retrieves a new copy of the metadata from the master. |
|Tablet |A tablet consists of adjacent, continuous segments within a table, similar to partitions in other data storage engines or relational databases. A given tablet is replicated across multiple Tablet Server nodes, forming multiple replicas. At any given time, one of these replicas is elected as the leader tablet. |
|Raft |The consistency protocol ensures high availability of the Kudu Master service and data consistency among tablet replicas. |
