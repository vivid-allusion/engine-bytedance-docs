---
title: "EMR on VKE use cases"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_on_VKE_use_cases"
---

<span id="40343da5"></span>
## Data preparation before model training

The following types of issues are frequently encountered during Preparation:


* Strict timeliness requirements, with data required to be completed within the business\-defined timeframe.

* High data processing throughput, resulting in demanding network bandwidth requirements for object storage.

* In scenarios with data skew, shuffle parallelism is high, and it is common for some nodes' disks to be full while others remain idle.

* Distributed computing frameworks are commonly used during computation, but these frameworks often adopt file semantics, which are inconsistent with the object semantics of data storage.

* It is necessary to load a wide range of third\-party processing tools, requiring a flexible runtime environment.


EMR on VKE provides high\-performance computing engines and distributed computing frameworks such as Spark and Ray for Preparation, enabling linear scaling of computing capacity based on data volume.


|**Spark** |**Ray** |
|---|---|
|* The engine is relatively mature; debugging is more complex.<br><br>* Java technology stack<br><br>* Often required for text analysis |* Compared to Spark, it is more lightweight.<br><br>* The shuffle mechanism is relatively simple.<br><br>* Lightweight; C++ has higher execution efficiency compared to Java.<br><br>* Often used for video, image, and text analysis. |


EMR uses Remote Shuffle to address data skew issues, improving task stability and execution efficiency. It is recommended that Remote Shuffle use nvMe SSD local disk instances such as i3s instance types for BytePlus.


|**Areas for improvement** |**Remote Shuffle scenario overview** |
|---|---|
|**Improve performance** |* Remote Shuffle reduces network latency and improves data transfer efficiency by decreasing the number of network requests and optimizing data transmission.<br><br>* By merging multiple small files into large files, it improves sequential read/write performance on disks, reduces random I/O, and thus enhances overall job performance.<br><br>* In scenarios with large volumes of data, Remote Shuffle uses centralized decision\-making capabilities, such as load balancing, to manage physical machine I/O more effectively and improve performance. |
|**Enhance stability** |* Remote Shuffle, through a compute\-storage separation architecture, ensures that the stability of the Shuffle service is not affected by the stability of compute nodes.<br><br>* It introduces flow control mechanisms, such as credit\-based flow control, to prevent downstream consumer nodes from being overwhelmed by excessive data volumes.<br><br>* It provides better fault tolerance and self\-recovery capabilities, maintaining final cluster state consistency through heartbeat and state synchronization mechanisms. |
|**Improve resource utilization** |* Remote Shuffle reduces disk usage on compute nodes, lowers dependence on local disks, and enables Spark jobs to run more efficiently in resource\-constrained environments.<br><br>* By optimizing memory usage, such as using managed memory, the risk of memory overflow is reduced and job stability is improved. |
|**Simple deployment and operations and maintenance** |* Remote Shuffle Service, as an independent service, simplifies the deployment and operations and maintenance of Spark jobs.<br><br>* Provides rich monitoring metrics, making it easier for users to monitor the system's running status and simplifying issue identification and troubleshooting. |


By using the EMR self\-developed data lake acceleration engine[Proton overview](https://docs.byteplus.com/docs/undefined/69a968353f58f805314f0f02), the conversion from file semantics to object semantics is solved. When combined with object storage (TOS) file buckets (HNS), the performance of rename, delete, and list operations is significantly improved. The Proton caching mode can significantly alleviate bandwidth limitations when accessing object storage.

Users can flexibly add custom libraries and Python packages based on the EMR on VKE Spark/Ray base image to create a custom runtime environment.

<span id="1ef70db4"></span>
## Hybrid online and offline deployment

Online business systems and offline big data systems use two sets of infrastructure, with resources isolated from each other, which is common within enterprises. As the Kubernetes architecture becomes increasingly popular and mature, more and more enterprises deploy online business systems based on Kubernetes, while big data systems still use traditional server setups. The existence of two sets of underlying infrastructure for online business systems and big data systems usually leads to the following issues:


* Two sets of underlying infrastructure create resource islands, resulting in low overall resource utilization at the company level.

* Two sets of underlying infrastructure and an O&M system that cannot be unified increase O&M costs.


By using EMR on VKE, users can share a single VKE cluster (K8s) for both online business systems and offline big data, enabling underlying resource sharing through time\-based multiplexing, improving overall resource utilization, and achieving cost reduction. After sharing the VKE cluster, a unified O&M system can be implemented, significantly reducing O&M costs. In addition, leveraging capabilities such as elastic scaling and dynamic oversubscription can further improve resource utilization and reduce permanently allocated resources.
