---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/yarn_faqs"
---

<span id="集群重启"></span>
## Cluster restart

Cluster restart consists of RM restart and NM restart.


* RM restart:

   During RM operation, key information is stored in Zookeeper. Upon restart, RM reloads key information from Zookeeper to restore in\-memory records and also obtains additional information from NM's re\-registration and heartbeat reporting logic to ensure that no information is lost during the restart process.

* NM restart:

   During NM operation, key information is stored locally in LevelDB. Restarting NM does not affect container processes running locally on the node. After the restart, NM re\-establishes communication with these processes through local storage to enable real\-time updates of task status.


<span id="nodemanager-可管理资源"></span>
## Resources managed by NodeManager

A normal NodeManager starts on Task or Core nodes and can manage all resources on the node. However, since a resource buffer must be reserved for system processes, the calculation rules for resources managed by NodeManager are as follows:


* Number of manageable cores = Total number of cores on the node \- 1

* Manageable memory (MB) = Total memory (MB) on the node \- 20000


<span id="配置yarn队列后，rm启动异常。"></span>
## RM startup exception after configuring YARN queues.


* Phenomenon description: RM reports a "Failed to initialize queues" error.

* Cause analysis: Queue configuration error, for example, queue names do not support "_".

* Solution: Change the queue name to comply with the specification.
