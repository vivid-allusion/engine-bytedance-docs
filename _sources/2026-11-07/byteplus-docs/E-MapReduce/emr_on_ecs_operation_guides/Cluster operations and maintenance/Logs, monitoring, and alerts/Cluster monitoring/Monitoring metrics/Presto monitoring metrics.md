---
title: "Presto monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_presto_monitoring_metrics"
---

This article provides detailed information about Presto metrics.

Presto metrics include the following sections:


* [Overview](https://docs.byteplus.com/docs/E-MapReduce/105457#%E6%A6%82%E8%A7%88)

* [Presto Worker](https://docs.byteplus.com/docs/E-MapReduce/105457#presto-worker)

* [Presto Coordinator](https://docs.byteplus.com/docs/E-MapReduce/105457#presto-coordinator)


<span id="概览"></span>
## Overview


|**Title** |**Metric name** |**Unit** |
|---|---|---|
|Node information |Number of active nodes |Count |
||Number of failed nodes |Count |
||Number of stopping nodes |Count |
|Query status |Queries |Count |
||Query frequency |Count/min |
|Input and output volume |Data input and output per minute |GB/min |


<span id="presto-worker"></span>
## Presto Worker


|**Title** |**Metric name** |**Unit** |
|---|---|---|
|JVM memory |JVM memory |MB |
|Input and output |Data input and output rate |GiB |
|Process |Number of threads |Count |
||Process running duration |h |
||Process start time |h |
|Number of file descriptors |Number of file descriptors |Count |


<span id="presto-coordinator"></span>
## Presto Coordinator


|**Title** |**Metric name** |**Unit** |
|---|---|---|
|JVM memory |JVM memory |MB |
|Process |Number of threads |Count |
||Process running duration |h |
||Process start time |h |
|Number of file descriptors |Number of file descriptors |Count |
