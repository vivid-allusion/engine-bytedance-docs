---
title: "Data shuffle"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Data_shuffle"
---

<span id="falcon：remote-shuffle-service"></span>
## EMR Serverless Celeborn: enterprise edition Remote Shuffle Service

Shuffle is the process used in Spark jobs to facilitate data exchange between upstream and downstream stages. A service that provides shuffle capabilities is called a Shuffle Service.

Initially, Spark internally implemented a hash\-based Shuffle Service, and later introduced a sort\-based Shuffle Service. Although Spark continuously improves its internal shuffle mechanism, the coupling between storage and computation limits the availability of Spark's internal shuffle mechanism in certain scenarios.

To address this issue, the industry proposed a shuffle design that separates the Shuffle Service from Spark, commonly referred to as Remote Shuffle Service (RSS). RSS allows the Shuffle Service to run outside of Spark, decoupling storage and computation, and providing better availability and performance.

Volcano EMR Serverless Celeborn is a fully managed Remote Shuffle Service launched by Volcano EMR, featuring a highly available architecture with separation of storage and computation. It supports the Spark engine to read and write remote shuffle data, and can be deployed and applied in cloud environments.


|**Features** |**Feature optimization/description** |**Main scenarios** |
|---|---|---|
|Replace Spark native ESS |Shuffle performance and stability improvement |General scenarios |
|Spark supports dynamic resource allocation |Since shuffle data is managed, Executors can be quickly released |General scenarios |
|Support for columnar shuffle |Enhances Native Shuffle performance |Spark on Native scenarios |


<span id="bb75c2a3"></span>
## Shuffle efficiency

In distributed computing engines, data exchange between compute nodes is common but also expensive. In traditional shuffle frameworks, disk and network efficiency is low (M mappers and N reducers result in M \* N), leading to high usage costs.

In addition to low efficiency, traditional shuffle frameworks require significant local storage on compute nodes to store shuffle data, which also hinders the adoption of storage\-computation separation architectures.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29946e700f0e40789f27595b9b23c55c~tplv-goo7wpa0wc-image.image" width="500px" /></div>


EMR Serverless Celeborn reorganizes shuffle data in a more efficient way and stores the data in a separate service to reduce the amount of data stored and transmitted, resulting in lower overall shuffle costs. The architecture is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e44ac430bc94b808bd340b164a19e72~tplv-goo7wpa0wc-image.image" width="554px" /></div>


This service improves disk and network efficiency through data reorganization. It Saves the shuffle data from the mapper side on worker nodes, so the mapper side does not require local disks to store this data. When a reducer needs data from a partition, it only needs a network connection to sequentially read the file. This significantly reduces the Mapper side's reliance on local disks and decouples the upstream and downstream Mapper and Reducer in the shuffle process, allowing the upstream Mapper to promptly release computing resources upon completion.

EMR Serverless Celeborn also provides Tiered Storage capability, which selects different media (memory/SSD/HDD) for storing shuffle data based on the job size, further improving the execution performance of small and medium\-sized jobs.

<span id="e95e3e17"></span>
## Shuffle stability

Since EMR Serverless Celeborn enables data aggregation on the Reducer side, it resolves the issue of fragmented reads during the shuffle phase, greatly reducing reliance on disk IOPS, lowering the risk of OOM (out\-of\-memory) for Spark Executors during runtime, and ensuring the stability of large shuffle jobs. Through the CRC verification scheme, the stability of shuffle data is maximized, preventing execution correctness issues caused by data loss.
