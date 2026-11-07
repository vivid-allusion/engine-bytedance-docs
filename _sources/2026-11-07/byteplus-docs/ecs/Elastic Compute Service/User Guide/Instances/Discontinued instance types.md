---
title: "Discontinued instance types"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-types-that-will-stop-selling"
---

<span id="overview"></span>
## overview

The instance types listed in this article have been discontinued in all regions. You can then choose to purchase the instances recommended in the table below to deploy your business on the new instances.

Please refer to the following documentation for the specific discontinuation time and impact of the discontinuation.


* [[Discontinuation of sale] Announcement on the discontinuation of i2, and d2 of ECS](https://docs.byteplus.com/en/docs/ecs/discontinuation-of-i2-and-d2)

* [[Discontinuation of sale] Announcement on the discontinuation of g2i, c2i, and r2i of ECS](https://docs.byteplus.com/en/docs/ecs/Announcement-on-Discontinuation-of-Sales)



|Discontinued time |Discontinued instance type |Recommended Use |
|---|---|---|
|February 28, 2025 |[Local-SSD i2](https://docs.byteplus.com/en/docs/49/20522#local-ssd-i2) |[Local-SSD i3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#local-ssd-i3s) |
||[Big Data d2](https://docs.byteplus.com/en/docs/49/20522#big-data-d2) |[Big Data d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based#big-data-d2c) |
|July 31, 2024 |[General-purpose g2i](https://docs.byteplus.com/en/docs/49/20522#general-purpose-g2i) |[General-purpose g3il](https://docs.byteplus.com/en/docs/ecs/General-purpose#general-purpose-g3il) |
||[Compute-optimized c2i](https://docs.byteplus.com/en/docs/49/20522#compute-optimized-c2i) |[Compute-optimized c3il](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#compute-optimized-c3il) |
||[Memory-optimized r2i](https://docs.byteplus.com/en/docs/49/20522#memory-optimized-r2i) |[Memory-optimized r3il](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#memory-optimized-r3il) |


<span id="instance-types-will-discontinue"></span>
## Instance types will discontinue

<span id="local-ssd-i2"></span>
### Local\-SSD i2

**Feature**


|Type |Performance |
|---|---|
|Computing |* Processor: Utilize the third\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Ice Lake) with a processor base frequency of 2.8 GHz and an all cores turbo frequency of 3.5 GHz.<br><br>* Support a processor\-to\-memory ratio of 1:8.<br><br>* Maximum support: 56 vCPUs and 480 GiB.<br><br>> For instance types of higher specifications, contact customer manager for support. |
|Storage |* Support Enhanced SSD volume and allow for a maximum of 16 volumes to be attached (including one system volume).<br><br>* The storage I/O performance is dependent on the instance type, with higher specifications providing stronger performance. |
|Networks |* Maximum network bandwidth: 40 Gbit/s.<br><br>* Maximum throughput: 5 million PPS.<br><br>* Instance types with small configurations have burstable network performance.<br><br>* The network performance is dependent on the instance type, with higher specifications providing stronger performance. |


**Scenario**


* Online Transaction Processing (OLTP) and high\-performance relational databases.

* Small to medium\-sized NoSQL databases, such as Cassandra, MongoDB, and Aerospike.

* In\-memory databases, such as Redis.

* Search scenarios using ElasticSearch, and similar applications.

* Analytical workloads


**Type**


|Instance type |vCPU |Memory (GiB) |Local storage (GB) |Inbound and outbound network bandwidth (basic/burst, Gbit/s) |Inbound and outbound maximum throughput (ten thousand PPS) |Connections (ten thousand) |Maximum queues per network interface |Elastic network interfaces (including one primary network interface) |Private IP address for each network interface |Volume IOPS (ten thousand) |Volume bandwidth (Gbit/s) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.i2.3xlarge |12 |96 |3840 \* 1 |9/up to 14 |120 |40 |8 |4 |15 |3 |3 |
|ecs.i2.4xlarge |16 |128 |3840 \* 1 |12/up to 18 |150 |60 |8 |8 |30 |4 |4 |
|ecs.i2.8xlarge |32 |256 |3840 \* 2 |24/none |250 |120 |16 |8 |30 |8 |8 |
|ecs.i2.14xlarge |56 |480 |3840 \* 4 |40/none |500 |200 |16 |8 |30 |15 |16 |


<span id="big-data-d2"></span>
### Big Data d2

**Feature**


|Type |Performance |
|---|---|
|Computing |* Processor: Utilize the third\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Ice Lake) with a processor base frequency of 2.8 GHz and an all cores turbo frequency of 3.5 GHz.<br><br>* Support a processor\-to\-memory ratio of 1:4.<br><br>* Maximum support: 56 vCPUs and 224 GiB.<br><br>> For instance types of higher specifications, contact customer manager for support. |
|Storage |* Support Enhanced SSD volume and allow for a maximum of 16 volumes to be attached (including one system volume).<br><br>* Maximum support: 8,000 GB x 12 local volumes.<br><br>* The storage I/O performance is dependent on the instance type, with higher specifications providing stronger performance. |
|Networks |* Maximum network bandwidth: 40 Gbit/s.<br><br>* Maximum throughput: 5 million PPS.<br><br>* The network performance is dependent on the instance type, with higher specifications providing stronger performance. |


**Scenario**


* Large\-scale data warehousing and massive data storage.

* Distributed computing and storage scenarios, such as Hadoop MapReduce, HDFS, Hive, and HBase.

* Search and log data processing, such as Elasticsearch.

* Data tiering, storage and computing separation.

* Ideal for industries with high requirements for big data storage and analysis, such as the finance and internet sectors.


**Type**


|Instance type |vCPU |Memory (GiB) |Local storage (GB) |Inbound and outbound network bandwidth (Gbit/s) |Inbound and outbound maximum throughput (ten thousand PPS) |Connections (ten thousand) |Maximum queues per network interface |Elastic network interfaces (including one primary network interface) |Private IP address for each network interface |Volume IOPS (ten thousand) |Volume bandwidth (Gbit/s) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.d2.4xlarge |14 |56 |8000 \* 3 |10 |150 |50 |8 |8 |30 |4 |4 |
|ecs.d2.7xlarge |28 |112 |8000 \* 6 |20 |250 |100 |16 |8 |30 |8 |8 |
|ecs.d2.14xlarge |56 |224 |8000 \* 12 |40 |500 |200 |16 |8 |30 |15 |16 |


<span id="general-purpose-g2i"></span>
### General\-purpose g2i

**Feature**


|Type |Performance |
|---|---|
|Computing |* Processor: Utilize the third\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Ice Lake) with a processor base frequency of 2.3 GHz and an all cores turbo frequency of 3.0 GHz.<br><br>* Support a processor\-to\-memory ratio of 1:4.<br><br>* Maximum support: 112 vCPUs and 448 GiB. |
|Storage |* Support Enhanced SSD volume and allow for a maximum of 16 volumes to be attached (including one system volume).<br><br>* The storage I/O performance is dependent on the instance type, with higher specifications providing stronger performance. |
|Networks |* Maximum network bandwidth: 80 Gbit/s.<br><br>* Maximum throughput: 10 million PPS.<br><br>* Instance types with small configurations have burstable network performance.<br><br>* The network performance is dependent on the instance type, with higher specifications providing stronger performance. |


**Scenario**


* Scenarios with high maximum throughput requirements

* Various types and scales of enterprise applications

* Website and application servers

* Game servers

* Data analysis and computation

* Compute clusters, memory\-based data processing


**Type**


|Instance type |vCPU |Memory (GiB) |Inbound and outbound network bandwidth (basic/burst, Gbit/s) |Inbound and outbound maximum throughput (ten thousand PPS) |Connections (ten thousand) |Maximum queues per network interface |Elastic network interfaces (including one primary network interface) |Private IP address for each network interface |Volume IOPS (ten thousand) |Volume bandwidth (Gbit/s) |
|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g2i.large |2 |8 |2/up to 5 |50 |25 |2 |3 |6 |1 |1.5 |
|ecs.g2i.xlarge |4 |16 |4/up to 8 |80 |25 |4 |4 |15 |2 |2 |
|ecs.g2i.2xlarge |8 |32 |6/up to 10 |100 |25 |8 |4 |15 |3 |3 |
|ecs.g2i.4xlarge |16 |64 |12/up to 18 |150 |60 |8 |8 |30 |4 |4 |
|ecs.g2i.8xlarge |32 |128 |24/none |250 |120 |16 |8 |30 |8 |8 |
|ecs.g2i.12xlarge |48 |192 |36/none |400 |180 |16 |8 |30 |12 |12 |
|ecs.g2i.14xlarge |56 |224 |40/none |500 |200 |16 |8 |30 |15 |16 |
|ecs.g2i.28xlarge |112 |448 |80/none |1000 |400 |32 |15 |30 |30 |32 |


<span id="compute-optimized-c2i"></span>
### Compute\-optimized c2i

**Feature**


|Type |Performance |
|---|---|
|Computing |* Utilize the third\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Ice Lake) with a processor base frequency of 2.3 GHz and an all cores turbo frequency of 3.0 GHz.<br><br>* Support a processor\-to\-memory ratio of 1:2.<br><br>* Maximum support: 48 vCPUs and 96 GiB.<br><br>> For instance types of higher specifications, contact customer manager for support. |
|Storage |* Support Enhanced SSD volume and allow for a maximum of 16 volumes to be attached (including one system volume).<br><br>* The storage I/O performance is dependent on the instance type, with higher specifications providing stronger performance. |
|Networks |* Maximum network bandwidth: 36 Gbit/s.<br><br>* Maximum throughput: 4 million PPS.<br><br>* Instance types with small configurations have burstable network performance.<br><br>* The network performance is dependent on the instance type, with higher specifications providing stronger performance. |


**Scenario**


* Scenarios with high maximum throughput requirements

* Websites or web servers with high computational demands

* MassiveIy multiplayer online games (MMOs)

* Web front\-end servers

* Data analysis, batch processing, video encoding

* High\-performance scientific and engineering applications


**Type**


|Instance type |vCPU |Memory (GiB) |Inbound and outbound network bandwidth (basic/burst, Gbit/s) |Inbound and outbound maximum throughput (ten thousand PPS) |Connections (ten thousand) |Maximum queues per network interface |Elastic network interfaces (including one primary network interface) |Private IP address for each network interface |Volume IOPS (ten thousand) |Volume bandwidth (Gbit/s) |
|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c2i.large |2 |4 |2/up to 5 |50 |25 |2 |3 |6 |1 |1.5 |
|ecs.c2i.xlarge |4 |8 |4/up to 8 |80 |25 |4 |4 |15 |2 |2.0 |
|ecs.c2i.2xlarge |8 |16 |6/up to 10 |100 |25 |8 |4 |15 |3 |3.0 |
|ecs.c2i.4xlarge |16 |32 |12/up to 18 |150 |60 |8 |8 |30 |4 |4.0 |
|ecs.c2i.8xlarge |32 |64 |24/none |250 |120 |16 |8 |30 |8 |8.0 |
|ecs.c2i.12xlarge |48 |96 |36/none |400 |180 |16 |8 |30 |12 |12.0 |


<span id="memory-optimized-r2i"></span>
### Memory\-optimized r2i

**Feature**


|Type |Performance |
|---|---|
|Computing |* Utilize the third\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Ice Lake) with a processor base frequency of 2.3 GHz and an all cores turbo frequency of 3.0 GHz.<br><br>* Support a processor\-to\-memory ratio of 1:8.<br><br>* Maximum support: 48 vCPUs and 384 GiB.<br><br>> For instance types of higher specifications, contact customer manager for support. |
|Storage |* Support Enhanced SSD volume and allow for a maximum of 16 volumes to be attached (including one system volume).<br><br>* The storage I/O performance is dependent on the instance type, with higher specifications providing stronger performance. |
|Networks |* Maximum network bandwidth: 36 Gbit/s.<br><br>* Maximum throughput: 4 million PPS.<br><br>* Instance types with small configurations have burstable network performance.<br><br>* The network performance is dependent on the instance type, with higher specifications providing stronger performance. |


**Scenario**


* Scenarios with high maximum throughput requirements

* High\-performance databases, in\-memory databases

* Data analysis and mining, distributed in\-memory caching

* Hadoop, Spark clusters, and other enterprise applications with large memory requirements.


**Type**


|Instance type |vCPU |Memory (GiB) |Inbound and outbound network bandwidth (basic/burst, Gbit/s) |Inbound and outbound maximum throughput (ten thousand PPS) |Connections (ten thousand) |Maximum queues per network interface |Elastic network interfaces (including one primary network interface) |Private IP address for each network interface |Volume IOPS (ten thousand) |Volume bandwidth (Gbit/s) |
|---|---|---|---|---|---|---|---|---|---|---|
|ecs.r2i.large |2 |16 |2/up to 5 |50 |25 |2 |3 |6 |1 |1.5 |
|ecs.r2i.xlarge |4 |32 |4/up to 8 |80 |25 |4 |4 |15 |2 |2.0 |
|ecs.r2i.2xlarge |8 |64 |6/up to 10 |100 |25 |8 |4 |15 |3 |3.0 |
|ecs.r2i.4xlarge |16 |128 |12/up to 18 |150 |60 |8 |8 |30 |4 |4.0 |
|ecs.r2i.8xlarge |32 |256 |24/none |250 |120 |16 |8 |30 |8 |8.0 |
|ecs.r2i.12xlarge |48 |384 |36/none |400 |180 |16 |8 |30 |12 |12.0 |
