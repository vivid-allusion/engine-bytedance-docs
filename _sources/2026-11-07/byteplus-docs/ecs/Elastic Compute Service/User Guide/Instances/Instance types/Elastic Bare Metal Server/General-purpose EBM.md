---
title: "General-purpose EBM"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM"
---

<span id=".5qaC6L-w"></span>
## Overview

By referring to this topic, you can select an instance type that meets your business needs. This helps you ensure that the selected type meets the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


* <div data-tips="true" data-tips-type="warning">For information on Elastic Bare Metal (EBM) instances, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/EBM-overview">EBM overview</a>.</div>




|Specification/type |Applicable scenarios |
|---|---|
|[General-purpose EBM ebmg3id](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM#.6YCa55So5Z6L5by55oCn6KO46YeR5bGeZWJtZzNpZA==) |General\-purpose dedicated computing: Dedicated physical computing resources are provided, applicable for production environments where dedicated applications or web applications associate with hardware. The workloads include web and application servers, backend servers supporting enterprise applications, game servers, and cache clusters. |
|[General-purpose EBM ebmg3ad](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM#.6YCa55So5Z6L5by55oCn6KO46YeR5bGeZWJtZzNhZA==) ||


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The specifications and lifecycle of local volumes depend on the ECS instance types can not be purchased separately. Local volumes can not be separately mounted, unmounted, or scaled up.

* When you delete an instance, all the data stored in the local volume is automatically cleared. Please [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) before you delete the instance.

* A physical server failure or local volume damage may cause data loss. Therefore, do not store the data for long\-term use on a local volume and [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) timely.

   * We recommend that you use a high\-availability architecture and deploy your services on multiple instances, or enable the cloud volume for data backup. These measures ensure high availability of your services and data reliability.

   * If the data architecture of your application is not reliable, we recommend that you use cloud volumes for data backup.


<span id=".6YCa55So5Z6L5by55oCn6KO46YeR5bGeZWJtZzNpZA=="></span>
## General\-purpose EBM ebmg3id

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently only available for sale in certain regions/availability zones. Please see the console for details. If you need to use this instance, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">Changing instance type is not allowed.</div>


* <div data-tips="true" data-tips-type="tip">Data Streaming Accelerator (DSA), In\-Memory Analytics Accelerator (IAA), and QuickAssist Technology (QAT) are supported, enabling efficient offloading and acceleration of data operations. This helps you optimize the performance of databases, encryption, compression, and queue management workloads.</div>



**Features**


|Type |Performance |
|---|---|
|Compute |* ecs.ebmg3id.48xlarge:<br><br>   * Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>   * The processor\-to\-memory ratio is 1:5.3.<br><br>* ecs.ebmg3id.60xlarge:<br><br>   * Processor: the 5th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Emerald Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.0 GHz.<br><br>   * The processor\-to\-memory ratio is 1:4.2. |
|Storage |* You can use ESSD volumes. A maximum of 8 volumes (including 1 system volume) can be mounted.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36,000,000 PPS |


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |Local storage (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmg3id.48xlarge |192 |1,024 |3,840 \* 2 |96 |3,600 |600 |32 |8 |30 |60 |32 |8 |
|ecs.ebmg3id.60xlarge |240 |1,024 |3,840 \* 2 |96 |3,600 |600 |32 |8 |30 |60 |32 |8 |


<span id=".6YCa55So5Z6L5by55oCn6KO46YeR5bGeZWJtZzNhZA=="></span>
## General\-purpose EBM ebmg3ad

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently only available for sale in certain regions/availability zones. Please see the console for details. If you need to use this instance, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">Changing instance type is not allowed.</div>


* <div data-tips="true" data-tips-type="tip">For information on images that can be used for this instance, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>



**Features**


|Type |Performance |
|---|---|
|Compute |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:4. |
|Storage |* You can use ESSD volumes. A maximum of 8 volumes (including 1 system volume) can be mounted.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 18,000,000 PPS |


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |Local storage (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmg3ad.96xlarge |384 |1,536 |3,840 \* 2 |96 |1,800 |600 |32 |8 |30 |60 |32 |8 |
