---
title: "Doris monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_Doris_monitoring_metrics"
---

This document provides detailed information about Doris metrics.

Doris metrics include the following sections:


* [Node information](https://docs.byteplus.com/docs/E-MapReduce/105470#_1-%E8%8A%82%E7%82%B9%E4%BF%A1%E6%81%AF)

* [Capacity information](https://docs.byteplus.com/docs/E-MapReduce/105470#_2-%E5%AE%B9%E9%87%8F%E4%BF%A1%E6%81%AF)

* [Doris service information](https://docs.byteplus.com/docs/E-MapReduce/105470#_3-doris-%E6%9C%8D%E5%8A%A1%E4%BF%A1%E6%81%AF)


<span id="_1-节点信息"></span>
## Node information


* Number of FE nodes

* Number of active FE nodes

* Number of failed FE nodes

* Number of BE nodes

* Number of active BE nodes

* Number of failed BE nodes


<span id="_2-容量信息"></span>
## Capacity information


* BE storage capacity


<span id="_3-doris-服务信息"></span>
## Doris service information


|Metric name |Metric description |
|---|---|
|FE instance status |Operating status of each FE instance. Code 1 indicates active, code 0 indicates FE instance failure. |
|BE instance status |Operating status of each BE instance. Code 1 indicates active, code 0 indicates BE instance failure. |
|FE node memory usage |Memory usage of each FE node |
|BE node memory usage |Memory usage of each BE node |
|QPS |QPS of the cluster. Includes FE average QPS, FE maximum QPS, and total cluster QPS.<br><br>FE average QPS is the average QPS of all FE instances in the cluster,<br><br>FE maximum QPS is the maximum QPS among all FE instances in the cluster,<br><br>Total cluster QPS is the sum of QPS of all FE instances in the cluster. |
|RPS |RPS of the cluster. Includes FE average RPS, FE maximum RPS, and total cluster RPS.<br><br>FE average RPS is the average RPS of all FE instances in the cluster,<br><br>FE maximum RPS is the maximum RPS among all FE instances in the cluster,<br><br>Total cluster RPS is the sum of RPS of all FE instances in the cluster. |
|Total number of queries |Total number of queries. Includes total number of queries, total number of failed queries, total number of successful queries, and total number of timed\-out queries.<br><br>This metric will be reset after FE restarts. |
|Query response time |Query response time, including P999, P99, P95, and P75 query response times. |
|Number of FE node connections |Number of FE connections. Includes average number of connections, maximum number of connections, and total number of connections in the cluster. |
|FE JVM heap memory usage |Memory usage within the JVM heap of the FE process. |
|BE node CPU usage |CPU usage of BE nodes. |
|BE node disk usage |Disk usage of BE nodes. Includes disk usage for each node, average, and maximum values. |
|BE node disk read/write speed |Disk read/write speed of BE nodes. Includes read/write speed for each node, average, and maximum values. |
|BE node disk I/O latency |Disk I/O latency of BE nodes. Includes IO latency for each node, average, and maximum values. |
|BE node network read/write speed |Network read/write speed of BE nodes. Includes network read/write speed for each node, average, and maximum values. |
