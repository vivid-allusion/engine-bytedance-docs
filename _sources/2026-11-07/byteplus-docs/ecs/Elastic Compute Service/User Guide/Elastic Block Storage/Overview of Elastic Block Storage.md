---
title: "Overview of Elastic Block Storage"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-of-elastic-block-storage"
---

&nbsp;

Elastic Block Storage (EBS) devices offered by BytePlus feature scalability, high availability, high reliability, and high performance. These devices can be used as scalable hard drives for Elastic Compute Service (ECS) and elastic container services.

<span id="types"></span>
## Types

EBS devices are also known as volumes and can be divided into the following types by purpose: system volume and data volume.


|Type |Description |
|---|---|
|System volume |This type of volume is used to store operating systems. Besides, it can be created only when you create an instance. The lifecycle of a system volume is the same as that of the ECS instance on which it is mounted. |
|Data volume |This type of volume is used to store application data. It can be used in scenarios in which I/O\-intensive applications, relational databases, NoSQL databases, or development and testing are involved.<br><br>You can mount a data volume when or after you create an ECS instance. For more information on volume specifications, refer to [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications). |


<span id="benefits"></span>
## Benefits


* **High performance**: All EBS products are built based on NVMe SSDs. A volume offers tens of thousands of input/output operations per second (IOPS) and ensures sub\-millisecond latency, meeting the requirements of high performance for any business.

* **Scalability**: You can expand volume capacity as needed to meet the requirements of rapidly growing businesses.

* **Ease of management**: EBS offers multiple management methods, such as the console and open APIs. You can use and manage volumes with ease, which can save labor costs.

* **Stability and reliability**: EBS supports a multi\-redundancy mechanism, preventing single point of failures (SPOFs) related to data. Besides, EBS offers 99.9999999% reliability and ensures data security.


<span id="limits"></span>
## Limits

For information on limits to volumes, refer to [Limits](https://docs.byteplus.com/en/docs/ecs/Limits).

&nbsp;

<span id="operation-overview"></span>
## Operation overview

For information on the overview of volume operations, refer to [Overview of volume operations](https://docs.byteplus.com/en/docs/ecs/Overview-of-volume-operations).
