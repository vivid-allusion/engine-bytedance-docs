---
title: "Big Data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Big-data-based"
---

<span id=".5qaC6L-w"></span>
## Overview

Big Data instances are configured with local HDDs, with a processor\-to\-memory ratio of 1:8 or 1:4. This instance type features large capacity, large bandwidth, high IOPS, and high maximum throughput. It is applicable for scenarios such as big data storage, computation, analysis, and processing. This topic describes the features, metrics, and applicable scenarios for each Big Data instance family. You can refer to this topic to select an instance type that meets your business needs and the minimum CPU and memory requirements of your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


<span id="i3vVTk5W"></span>
## Limits


* The specifications and lifecycle of local volumes are tied to the ECS instances and cannot be purchased separately. Local volumes cannot be separately mounted, unmounted, or scaled up.

* When you delete an instance, all the data stored in the local volume is automatically cleared. Please [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) before you delete the instance.

* A physical server failure or local volume damage may cause data loss. Therefore, do not store the data for long\-term use on a local volume and [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) timely.

   * We recommend that you use a high\-availability architecture and deploy your services on multiple instances, or use volumes for data backup. These measures ensure high availability of your services and data reliability.

   * If the data architecture of your application is not reliable, we strongly recommend that you use cloud volumes for data backup.


<span id="jqmxfbz9"></span>
## Big Data Compute\-optimized d4c

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This instance is currently in Beta in the China (Beijing) region. If you need a trial, please contact your account manager to apply.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel® Xeon® Scalable processor (Granite Rapids) with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.4 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 112 vCPUs, 448 GiB |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Local HDDs with high capacity and throughput are configured, providing local storage of up to 8,000 GB \* 24.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 120 Gbit/s<br><br>* Maximum throughput: 16,000,000 PPS<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Big data computing and storage scenarios such as Hadoop MapReduce, HDFS, Hive, and HBase

* Searching and log data processing such as Elasticsearch and Kafka

* Machine learning preprocessing scenarios, such as Spark offline computing and MLlib


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>


* <div data-tips="true" data-tips-type="default">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>




|Instance specification |vCPU<br><br> |Memory (GiB) |Local storage (GB) |VPC network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |
|---|---|---|---|---|---|---|---|
|ecs.d4c.4xlarge |14 |56 |8,000 \* 3 HDD |15 |200 |4/\-\- |4/\-\- |
|ecs.d4c.7xlarge |28 |112 |8,000 \* 6 HDD |30 |400 |8/\-\- |8/\-\- |
|ecs.d4c.14xlarge |56 |224 |8,000 \* 12 HDD |60 |800 |15/\-\- |16/\-\- |
|ecs.d4c.28xlarge |112 |448 |8,000 \* 24 HDD |120 |1,600 |30/\-\- |32/\-\- |
|ecs.d4cd.14xlarge |56 |224 |* 8,000 \* 12 HDD<br><br>* 3,840 \* 1 SSD |60 |800 |15/\-\- |16/\-\- |
|ecs.d4cd.28xlarge |112 |448 |* 8,000 \* 24 HDD<br><br>* 3,840 \* 2 SSD |120 |1,600 |30/\-\- |32/\-\- |


<span id="ypXfbn0a"></span>
## Big Data Storage\-optimized d4s

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This instance is currently in Beta in the China (Beijing) region. If you need a trial, please contact your account manager to apply.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel® Xeon® Scalable processor (Granite Rapids) with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.4 GHz.<br><br>* The processor\-to\-memory ratio is 1:6.<br><br>* Max.: 112 vCPUs, 720 GiB |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Local HDDs with high capacity and throughput are configured, providing local storage of up to 24,000 GB \* 24.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 120 Gbit/s<br><br>* Maximum throughput: 16,000,000 PPS<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Big data computing and storage scenarios such as Hadoop MapReduce, HDFS, Hive, and HBase

* Searching and log data processing such as Elasticsearch and Kafka

* Machine learning preprocessing scenarios, such as Spark offline computing and MLlib


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>


* <div data-tips="true" data-tips-type="default">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>




|Instance specification |vCPU<br><br> |Memory (GiB) |Local storage (GB) |VPC network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |
|---|---|---|---|---|---|---|---|
|ecs.d4s.4xlarge |14 |90 |24,000 \* 3 HDD |15 |200 |4/\-\- |4/\-\- |
|ecs.d4s.7xlarge |28 |180 |24,000 \* 6 HDD |30 |400 |8/\-\- |8/\-\- |
|ecs.d4s.14xlarge |56 |360 |24,000 \* 12 HDD |60 |800 |15/\-\- |16/\-\- |
|ecs.d4s.28xlarge |112 |720 |24,000 \* 24 HDD |120 |1,600 |30/\-\- |32/\-\- |
|ecs.d4sd.14xlarge |56 |360 |* 24,000 \* 12 HDD<br><br>* 3,840 \* 1 SSD |60 |800 |15/\-\- |16/\-\- |
|ecs.d4sd.28xlarge |112 |720 |* 24,000 \* 24 HDD<br><br>* 3,840 \* 2 SSD |120 |1,600 |30/\-\- |32/\-\- |


<span id="sRuv8d0D"></span>
## Big Data d2c

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 3rd\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Ice Lake) with a processor base frequency of 2.3 GHz and an all\-core turbo frequency of 3.0 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 56 vCPUs, 224 GiB<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Local HDDs with high capacity and throughput are configured, providing local storage of up to 8,000 GB \* 12.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 40 Gbit/s<br><br>* Maximum throughput: 5,000,000 PPS<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Big data computing and storage scenarios such as Hadoop MapReduce, HDFS, Hive, and HBase

* Machine learning scenarios such as Spark in\-memory computing and MLlib

* Searching and log data processing such as Elasticsearch and Kafka


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |Local storage (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.d2c.4xlarge |14 |56 |8,000 \* 3 |10 |150 |50 |8 |8 |30 |4 |4 |16 |
|ecs.d2c.7xlarge |28 |112 |8,000 \* 6 |20 |250 |100 |16 |8 |30 |8 |8 |16 |
|ecs.d2c.14xlarge |56 |224 |8,000 \* 12 |40 |500 |200 |16 |8 |30 |15 |16 |16 |
