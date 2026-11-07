---
title: "Supported ECS instances"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/emr_support_ecs_instances"
---

Volcano Engine E\-MapReduce (EMR) provides a variety of ECS compute specifications for you to choose from. Different compute specifications offer varying virtualization capabilities, supporting a wide range of business applications and service scenarios.

<span id="_1-emr支持的ecs实例类型"></span>
## **ECS instance types supported by EMR**

<span id="_1-1-通用型"></span>
### General purpose

vCPU:Memory=1:4.For example,8 cores and 32 GiB,using cloud disks for storage.


|Specification type |Description |
|---|---|
|[General-purpose g4i](https://docs.byteplus.com/en/docs/ecs/General-purpose#ZHRHYffU) |The latest generation of general\-purpose instances offers superior computing performance and enhanced I/O capabilities. |
|[General-purpose g3il](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNpbA==) |The third generation of general\-purpose instances provides balanced vCPU, memory, and network capabilities, meeting service requirements for most use cases. |
|[General-purpose g3i](https://docs.byteplus.com/en/docs/ecs/General-purpose?_vtm_=a78999.b69280.0_0.0_0.0.51_undefined#.6YCa55So5Z6LZzNp) |The third generation of general\-purpose instances integrates the latest proprietary unified virtualization architecture, delivering significant improvements in network and storage I/O performance compared to the second generation. The new generation of general\-purpose instances integrates Volcengine's latest proprietary DPU architecture, delivering significant improvements in network and storage I/O performance compared to the second generation. |
|[General-purpose g3a](https://docs.byteplus.com/en/docs/ecs/General-purpose?_vtm_=a78999.b69280.0_0.0_0.0.53_7638477131018044933#.6YCa55So5Z6LZzNh) ||


<span id="_1-2-计算型"></span>
### Compute type

vCPU:Memory=1:2. For example,8 cores and 16 GiB,using cloud disks for storage,providing more compute resources.


|Specification type |Description |
|---|---|
|[Compute-optimized c4i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#DvtwPnpi) |The latest generation of compute\-optimized instances offers superior computing performance and broader use cases. |
| ||
|[Compute-optimized c3al](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNhbA==) |The third generation of compute\-optimized instances is suitable for compute\-intensive applications such as batch workloads and distributed analytics. |
|[Compute-optimized c3il](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNpbA==) ||
|[i](https://www.volcengine.com/docs/6396/68528#%E8%AE%A1%E7%AE%97%E5%9E%8Bc3i)[Compute-optimized c3i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized?_vtm_=a78999.b69280.0_0.0_0.0.77_7638477131018044933#.6K6h566X5Z6LYzNp) |The third generation of compute\-optimized instances integrates proprietary unified virtualization architecture, delivering significant improvements in network and storage I/O performance compared to the second generation. |
|[Compute-optimized c3a](https://docs.byteplus.com/en/docs/ecs/Computing-optimized?_vtm_=a78999.b69280.0_0.0_0.0.78_undefined#.6K6h566X5Z6LYzNh) ||


<span id="_1-3-内存型"></span>
### Memory type

vCPU:Memory=1:8.For example,8 cores and 64 GiB,using cloud disks for storage,providing more memory resources. Suitable for scenarios with high memory requirements, large data access volumes, and large data sets, meeting service needs for demanding data storage, analysis, and search.


|Specification type |Description |
|---|---|
|[Memory-optimized r4i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#mgMpZfw5) |The latest generation of memory\-optimized instances provides greater memory capacity and superior computing and I/O capabilities. |
|[Memory-optimized r3il](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#JirQoNCM) |The third generation of memory\-optimized instances is suitable for memory\-intensive applications with high memory requirements and large data access volumes. |
|[Memory-optimized r3al](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#zOMddgDz) ||
|[Memory-optimized r3i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized?_vtm_=a78999.b69280.0_0.0_0.0.80_7638477131018044933#uvEC2ygI) |The third generation of memory\-optimized instances integrates proprietary unified virtualization architecture, delivering significant improvements in network and storage I/O performance compared to the second generation. |
|[Memory-optimized r3a](https://docs.byteplus.com/en/docs/ecs/Memory-optimized?_vtm_=a78999.b69280.0_0.0_0.0.81_undefined#qEWtPNM0) ||


<span id="_1-4-大数据型"></span>
### Big data type

Uses local SATA disks for data storage, offering cost\-effective storage. This is the recommended instance type for scenarios with large data volumes (terabyte\-level data).


* The specifications and lifecycle of HDD local disks follow the instance. Separate purchase is not supported, and disks cannot be separately attached, detached, or expanded.

* When an instance is deleted, data on the local disk will be automatically cleared. Please back up your data in advance.

* If the physical machine fails or the local disk is damaged, there is a risk of data loss on the local disk. Do not store data that needs to be stored long\-term on the local disk, and back up your data promptly.

   * It is recommended to adopt a high\-availability architecture, distribute your business across multiple instances, or use cloud disk backups to ensure high availability and data reliability.

   * If your application cannot ensure data reliability, we strongly recommend choosing cloud disk backups for your data.



|Specification type |Description |
|---|---|
|[Big data type d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based?_vtm_=a78999.b69280.0_0.0_0.0.84_undefined#sRuv8d0D) |The new generation of big data type instances, equipped with high\-throughput, large\-capacity HDD local disks, is suitable for big data computing, massive data storage, and similar business scenarios. |


<span id="_1-5-本地ssd型"></span>
### Local SSD type


* Uses local SSD disks, featuring high random IOPS (Input/Output Operations Per Second) and high throughput capability.

* The specifications and lifecycle of SSD local disks follow the instance. Separate purchase is not supported, and disks cannot be separately attached, detached, or expanded.

* When an instance is deleted, data on the local disk will be automatically cleared. Please back up your data in advance.

* Caution: There is a risk of data loss if the physical machine fails or the local disk is damaged. Do not save data that needs to be saved for the long term on the local disk, and make sure to back up your data promptly.

   * It is strongly recommended to adopt a high availability architecture, distribute workloads across multiple instances, or use cloud disk backups to ensure high availability and data reliability.

   * It is strongly recommended to save data that needs to be saved for the long term on cloud disks.



|Specification type |Description |
|---|---|
|[Local SSD i4ag](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#UtdiwP1E) |The fourth\-generation Local SSD instance is equipped with the latest Gen5 SSD drives, delivering a significant improvement in storage I/O and network performance compared to third\-generation instances. |
|[Local SSD i3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based?_vtm_=a78999.b69280.0_0.0_0.0.93_7638477131018044933#8IH6RHiz) |The third\-generation Local SSD instance, combined with Volcengine's proprietary integrated hardware\-software virtualization architecture, meets service requirements for most scenarios. |


<span id="_2-已停售的实例规格"></span>
## Discontinued instance types

The following instance types have been discontinued. You can purchase the recommended instances listed below to create your E\-MapReduce cluster.

For the impact of discontinuation, see:


* [[Discontinuation of sale] Announcement on the discontinuation of i2, and d2 of ECS](https://docs.byteplus.com/en/docs/ecs/discontinuation-of-i2-and-d2)

* [[Discontinuation of sale] Announcement on the discontinuation of g2i, c2i, and r2i of ECS](https://docs.byteplus.com/en/docs/ecs/Announcement-on-Discontinuation-of-Sales)



|Discontinuation date |Discontinued instances |Recommended |
|---|---|---|
|2025\-02\-28 |[Big data d2](https://docs.byteplus.com/en/docs/ecs/Instance-types-that-will-stop-selling#big-data-d2) |[Big data d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based?_vtm_=a78999.b69280.0_0.0_0.0.84_undefined#sRuv8d0D) |
||[Local SSD i2](https://docs.byteplus.com/en/docs/ecs/Instance-types-that-will-stop-selling#local-ssd-i2) |[Local SSD i3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based?_vtm_=a78999.b69280.0_0.0_0.0.93_7638477131018044933#8IH6RHiz) |
|2024\-7\-31 |[General-purpose g2i](https://docs.byteplus.com/en/docs/ecs/Instance-types-that-will-stop-selling#general-purpose-g2i) |[General purpose g3i](https://docs.byteplus.com/en/docs/ecs/General-purpose?_vtm_=a78999.b69280.0_0.0_0.0.51_undefined#.6YCa55So5Z6LZzNp) |
||[Compute c2i](https://docs.byteplus.com/en/docs/ecs/Instance-types-that-will-stop-selling#compute-optimized-c2i) |[Compute c3i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized?_vtm_=a78999.b69280.0_0.0_0.0.77_7638477131018044933#.6K6h566X5Z6LYzNp) |
||[Memory r2i](https://docs.byteplus.com/en/docs/ecs/Instance-types-that-will-stop-selling#memory-optimized-r2i) |[Memory r3i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized?_vtm_=a78999.b69280.0_0.0_0.0.80_7638477131018044933#uvEC2ygI) |
