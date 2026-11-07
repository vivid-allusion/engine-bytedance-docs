---
title: "ZooKeeper monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_ZooKeeper_monitoring_metrics"
---

This article provides detailed information about ZooKeeper metrics.

ZooKeeper metrics include the following sections:


* [OverView](https://docs.byteplus.com/docs/E-MapReduce/105465#overview)

* [Zookeeper Sever](https://docs.byteplus.com/docs/E-MapReduce/105465#zookeeper-sever)


<span id="overview"></span>
## OverView


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|Overview |Number of live ZK Server instances |number |
||Number of ZNodes |number |


<span id="zookeeper-sever"></span>
## Zookeeper Sever


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|Running status |Maximum number of file descriptors |number |
||Number of open file descriptors |number |
||Current number of connections |number |
|Latency |Average ZK processing latency |ms |
||Maximum ZK processing latency |ms |
||Minimum ZK processing latency |ms |
|Node status |Number of ZK Watches |number |
||Number of ZNodes |number |
||Number of ZK ephemeral nodes |number |
|Data size |Amount of data stored in ZK |Byte |
|Packet sending and receiving |ZK packet receiving rate |packets per second |
||ZK packet sending rate |packets per second |
