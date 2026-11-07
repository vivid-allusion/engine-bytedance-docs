---
title: "Explanation of observed metrics for the StarRocks engine"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Explanation_of_observed_metrics_for_the_StarRocks_engine"
---

<span id="a5b16a60"></span>
## Overview

EMR StarRocks provides a comprehensive set of monitoring metrics and alert metrics, which are essential for ensuring stable database operations and optimizing business decision\-making. These metrics offer a real\-time view of StarRocks performance, availability, and resource utilization, enabling database administrators to promptly identify and resolve potential performance bottlenecks or failures. They help maintain efficient system operation and ensure that data query and analysis tasks are completed quickly and reliably. In addition, by monitoring these metrics, enterprises can optimize resource allocation, improve operational efficiency, enhance cluster stability, and increase cluster resource utilization.

<span id="d027952d"></span>
## Explanation of observed metrics

<span id="556dc289"></span>
### Basic health check metrics


* Cluster availability: Check whether all nodes (including FE and BE nodes) are online and responding normally. The number of FE and BE/CN nodes and the number of active nodes can be viewed through the health status. If the number of active nodes is less than the total number of nodes, it indicates that some nodes are abnormal.

* Capacity information: Used to describe the total storage size of the cluster and information related to the total available memory of FE.


<span id="b95b6ebf"></span>
### Performance and load\-related metrics


* **Query latency (Query Latency)** : The average query time and the maximum query time can help assess the response speed of the cluster. If a sudden increase in query latency is observed, this may indicate excessive load or a resource bottleneck.

* **QPS (Queries Per Second)** : The number of queries processed per second. A high QPS may indicate that the system is under significant pressure.

* **FE connection count**: The status of clients that have established connections to FE. The average number of established connections per FE in the cluster represents the average connections across multiple FEs.

* **FE heap memory usage**: Represents the memory usage rate of the FE JVM. A high memory usage rate (80%) indicates a high load on FE, and FE memory expansion is required.

* **BE Fragment request response time**: Represents the response time for BE executing fragments. A sudden increase in this time indicates that the cluster is overloaded and may result in task accumulation.

* **CPU usage**: Monitor the CPU usage of each node. Consistently high CPU usage (such as above 80%) may indicate that computing resources are under strain.

* **Memory usage**: Check the memory usage of BE nodes, especially the occupancy of caches and buffers. If memory usage approaches the upper limit, it may result in OOM (Out of Memory) errors.

* **Disk usage**: Monitor the disk space used for data storage. When disk usage reaches a high level (for example, above 70%), consider expanding storage or optimizing data management strategies.

* **Network traffic**: Monitor network bandwidth usage. For distributed queries in particular, network latency and bandwidth limitations may become performance bottlenecks.


<span id="05f1a7aa"></span>
### Failure warning indicators


* Node offline: Check the number of faulty nodes in **health status**. Any unplanned offline event of FE or BE nodes should be addressed immediately. This may signal hardware failure, software crash, or network issues.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By observing node CPU and memory utilization, if any node exhibits abnormally low CPU and memory utilization, it suggests that the cluster may be experiencing anomalies. By observing health status, if any FE, BE, or CN node displays an unexpected unhealthy status, it indicates that the cluster is experiencing anomalies.</div>



* Data replica status: In distributed environments, data typically has multiple replicas to improve reliability and fault tolerance. An increase in the cluster's Tablet creation failure rate indicates that the cluster may be experiencing faults.


&nbsp;
