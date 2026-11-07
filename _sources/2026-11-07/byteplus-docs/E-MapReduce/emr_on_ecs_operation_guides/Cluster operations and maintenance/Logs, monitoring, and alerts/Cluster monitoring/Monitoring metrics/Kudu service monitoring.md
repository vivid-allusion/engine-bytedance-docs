---
title: "Kudu service monitoring"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_kudu_service_monitoring"
---

This article provides detailed information about Kudu metrics. Kudu metrics include the following sections:


* [Node information](https://docs.byteplus.com/docs/E-MapReduce/105455#_1-%E8%8A%82%E7%82%B9%E4%BF%A1%E6%81%AF)

* [Kudu information](https://docs.byteplus.com/docs/E-MapReduce/105455#_2-kudu-%E4%BF%A1%E6%81%AF)


<span id="_1-节点信息"></span>
## **Node information**


* Total number of healthy master nodes

* Total number of healthy tserver nodes


<span id="_2-kudu-信息"></span>
## **Kudu information**


* 99th percentile queue length of master

* 75th percentile queue length of master

* Average queue length of master

* 99th percentile queue length of tserver

* 75th percentile queue length of tserver

* Average queue length of tserver

* 99th percentile operation execution time of master, Unit: μs

* 75th percentile operation execution time of master, Unit: μs

* Average operation execution time of master, Unit: μs

* 99th percentile operation execution time of tserver, Unit: μs

* 75th percentile operation execution time of tserver, Unit: μs

* Average operation execution time of tserver, Unit: μs

* Block cache usage of master, Unit: Byte

* Block cache usage of tserver, Unit: Byte

* Number of data directories in full state of master

* Number of data directories in full state of tserver

* Number of failed data directories of master

* Number of failed data directories of tserver

* Number of running tablets on tserver

* Number of scanners in active state on tserver
