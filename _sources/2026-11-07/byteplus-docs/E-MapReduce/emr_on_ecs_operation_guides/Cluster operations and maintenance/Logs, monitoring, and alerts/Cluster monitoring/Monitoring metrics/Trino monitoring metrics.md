---
title: "Trino monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_trino_monitoring_metrics"
---

This article provides detailed information about Trino metrics.

Trino metrics include the following sections:


* [Overview](https://docs.byteplus.com/docs/E-MapReduce/105452#%E6%A6%82%E8%A7%88)

* [Trino Worke](https://docs.byteplus.com/docs/E-MapReduce/105452#trino-worke)

* [Trino Coordinator](https://docs.byteplus.com/docs/E-MapReduce/105452#trino-coordinator)


<span id="概览"></span>
## Overview


|**Title** |**metric name** |**Unit** |
|---|---|---|
|Number of nodes |Number of active nodes |count |
||Total number of nodes |count |
||Number of failed nodes |count |
|Query |Query |count |
||Query frequency |count |
|Input/output |Data input/output per minute |GB/min |


<span id="trino-worke"></span>
## Trino Worke


|**Title** |**metric name** |**Unit** |
|---|---|---|
|GC |Number of GC |times/min |
||GC time |times/min |
|JVM memory |JVM memory |MB |
|Input/output |Data input/output rate |GiB |
|Process |Number of threads |count |
||Process running duration |h |
|Number of file descriptors |Number of file descriptors |count |


<span id="trino-coordinator"></span>
## Trino Coordinator


|**Title** |**metric name** |**Unit** |
|---|---|---|
|GC |Number of GC |times/min |
||GC time |times/min |
|JVM memory |JVM memory |MB |
|Process |Number of threads |count |
||Process running duration |h |
||Process start time |h |
|Number of file descriptors |Number of file descriptors |count |
