---
title: "Local SSD"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Local-SSD-based"
---

## Overview

Local SSD instances are configured with SSD local volumes, typically with a processor\-to\-memory ratio of 1:8 or 1:4. This instance type is applicable for OLTP, high\-performance relational databases, NoSQL databases, in\-memory databases, and analytical workloads. This topic describes the features, metric data, and applicable scenarios of each instance family of Local SSD instances. By referring to this topic, you can select an instance type that meets your business needs. This helps you ensure that the selected type meets the minimum CPU and memory requirements for your business.

> **warning**

* > For information about instance types, estimated instance fees, instance type changes, and instance naming rules, refer to [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* > For the performance of local SSDs attached to Local SSD instances, refer to [Local volumes](https://docs.byteplus.com/en/docs/ecs/Local-volumes).

## Limits

* The specifications and lifecycle of local SSDs depend on the ECS instance type. Local SSDs cannot be separately purchased, mounted, unmounted, or scaled up.

* When you delete an instance, all the data stored in the local volume is automatically cleared. Please [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) before you delete the instance.

* A physical server failure or local volume damage may cause data loss. Do not store data that needs to be retained for a long time on local volumes, and [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) in a timely manner.

   * We strongly recommend that you use a high\-availability architecture, deploy your services across multiple instances, or use cloud volumes for data backup. These measures ensure high availability of your services and data reliability.

   * We strongly recommend that you store data that needs to be retained for a long time on volumes.

## Local SSD i4

> **tip**

> For this instance family, you cannot use Windows images.

**Features**

|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel® Xeon® Scalable processor (Granite Rapids) with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.4 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br>* Max.: 256 vCPUs, 2048 GiB |
|Storage |* You can use ESSD volumes. A maximum of 33 volumes (including 1 system volume) can be mounted.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |

**Applicable scenarios**

* Online Transaction Processing (OLTP) and high\-performance relational databases

* Data processing tasks that require local caching and remote caches

* I/O\-intensive scenarios such as searching with ElasticSearch

**Instance types and metrics**

> **tip**

* > Network inbound and outbound PPS can vary significantly depending on the business scenario. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.

* > Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.

|Instance specification |vCPU |Memory (GiB) |Local storage (GB) |VPC network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Volume IOPS (baseline/burst, unit: 10,000) |Volume bandwidth (baseline/burst, Gbit/s) |
|---|---|---|---|---|---|---|---|
|ecs.i4.4xlarge |16 |128 |3,840 \* 1 |10/max. 20 |220 |8/max. 11 |5/max. 8 |
|ecs.i4.8xlarge |32 |256 |3,840 \* 2 |20/max. 30 |450 |10/\-\- |8/\-\- |
|ecs.i4.16xlarge |64 |512 |3,840 \* 4 |36/\-\- |900 |20/\-\- |16/\-\- |
|ecs.i4.32xlarge |128 |1,024 |3,840 \* 8 |72/\-\- |1,800 |40/\-\- |32/\-\- |
|ecs.i4.64xlarge |256 |2,048 |3,840 \* 16 |96/\-\- |3600 |80/\-\- |64/\-\- |

## Local SSD i4ag

> **tip**

> For information on images that can be used for this instance, please refer to [Instructions on compatibility between AMD instance types and operating systems](https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility).

**Features**

|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC™️ Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is approximately 1:4.<br><br>* Max.: 192 vCPUs, 768 GiB<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes only. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 64 Gbit/s<br><br>* Maximum throughput: 18,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |

**Applicable scenarios**

* Hot\-cold data tiering in big data, storage and computing separation

* Online Transaction Processing (OLTP) and high\-performance relational databases

* Searching with ElasticSearch or similar applications

**Instance types and metrics**

> **tip**

* > Network packet sending and receiving PPS may vary significantly across different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.

* > Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.

|Instance specification |vCPU |Memory (GiB) |Local storage (GB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Volume IOPS (baseline/burst, unit: 10,000) |Volume bandwidth (baseline/burst, Gbit/s) |
|---|---|---|---|---|---|---|---|
|ecs.i4ag.12xlarge |48 |192 |3,840 \* 1 |16/max. 25 |450 |8/\-\- |4/max. 5 |
|ecs.i4ag.16xlarge |64 |256 |3,840 \* 1 |16/max. 25 |450 |8/\-\- |4/max. 5 |
|ecs.i4ag.24xlarge |96 |384 |3,840 \* 2 |32/\-\- |900 |15/\-\- |8/\-\- |
|ecs.i4ag.32xlarge |128 |512 |3,840 \* 2 |32/\-\- |900 |15/\-\- |8/\-\- |
|ecs.i4ag.48xlarge |192 |768 |3,840 \* 4 |64/\-\- |1,800 |30/\-\- |16/\-\- |

## Local SSD i3s

> **tip**

> For this instance family, you cannot use Windows images.

**Features**

|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel® Xeon® Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br>* Max.: 96 vCPUs, 768 GiB<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 72 Gbit/s<br><br>* Maximum throughput: 18,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |

**Applicable scenarios**

This instance family is applicable for scenarios such as high\-performance databases with high transaction and low latency workloads, such as:

* Data processing tasks and cache clusters that require local caching

* Small and medium\-sized databases

* Online Transaction Processing (OLTP) and high\-performance relational databases

* Searching with ElasticSearch or similar applications

**Instance types and metrics**

> **tip**

* > Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.

* > Network inbound and outbound PPS can vary significantly depending on the business scenario. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.

|Instance specification |vCPU |Memory (GiB) |Local storage (GB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Volume IOPS (baseline/burst, unit: 10,000) |Volume bandwidth (baseline/burst, Gbit/s) |
|---|---|---|---|---|---|---|---|
|ecs.i3s.3xlarge |12 |96 |3,840 \* 1 |9/max. 20 |220 |5/max. 8 |2/max. 4 |
|ecs.i3s.6xlarge |24 |192 |3,840 \* 2 |18/max. 30 |450 |8/\-\- |4/\-\- |
|ecs.i3s.12xlarge |48 |384 |3,840 \* 4 |36/\-\- |900 |15/\-\- |8/\-\- |
|ecs.i3s.24xlarge |96 |768 |3,840 \* 8 |72/\-\- |1,800 |30/\-\- |16/\-\- |
