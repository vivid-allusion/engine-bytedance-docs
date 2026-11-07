---
title: "Instance types and specifications"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types"
---

The platform provides various ECS instance types to meet different business needs. Different instances offer different virtualization capabilities, supporting various business applications and service scenarios. Before you purchase an instance, refer to this document for the instance types provided by the platform and the relationship between instance type families and instance types.

## Background information

Before you view the characteristics and metrics of each instance type family, we recommend that you first learn about the following:

### Learn about instance naming and type recommendations

Before purchasing an instance, you can refer to the following documents to learn the instance naming rules and information on how to choose an instance type based on your business scenarios.

* [Instance naming and type recommendations (x86 and Bare Metal)](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice)

* [Instance naming and type recommendations (Heterogeneous Compute-optimized)](https://docs.byteplus.com/en/docs/gpu/Best_practices_for_instance_selection)

### Estimate instance fees

After selecting an instance type, you may want to know the approximate instance fee under each billing method. You can view fees through the [price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2). This price is for reference only. The actual costs are the fee results displayed when you order in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance).

### View regions where instances are available for sale

Instance types available for sale may vary in [different regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones#.5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo). You can refer to [Viewing regions where instances are available for sale](https://docs.byteplus.com/en/docs/ecs/Viewing_regions_where_instances_are_available_for_sale) to check the availability of the target instance in the target region.

### Evaluate resource quota

We recommend that you evaluate the available resource quotas before creating an instance. Make sure that under your account, the total number of existing resources and resources to be created does not exceed the quota limit. Otherwise, the instance creation may fail due to insufficient quota. [Learn more](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management).

### Purchase instances directly

Go to the [instance purchase page](https://console.byteplus.com/ecs/buy?) and complete the purchase as described in [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). In addition, the platform provides [multiple purchasing methods](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances) for you to choose from.

> **tip**

> If you want to purchase Heterogeneous Compute\-optimized instances, please refer to [Purchasing GPU Accelerated instances](https://docs.byteplus.com/en/docs/gpu/Buying-GPU-Accelerated-instances) and [Purchasing HPC\-optimized instances](https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances).

### View information about instance type change

If your instance does not meet, or exceeds, your business requirements, refer to[ Instance types supporting type change](https://docs.byteplus.com/en/docs/ecs/Overview-2) to check whether the current instance type can be changed to other types.

## Instance classification

* Based on system architecture, the current ECS instance offerings are divided into three main categories: x86 Compute, Elastic Bare Metal (EBM), and Heterogeneous Compute\-optimized. Specifically:

   |Specification/type |Description |
   |---|---|
   |[x86](https://docs.byteplus.com/en/docs/ecs/X86_computing) |Based on the x86 architecture, a single physical core can process multiple threads simultaneously by using hyper\-threading technology. This improves resource utilization and processing efficiency of the processor, suitable for running workloads such as enterprise applications, database systems, video encoding/decoding and data analysis jobs. |
   |[EBM](https://docs.byteplus.com/en/docs/ecs/Elastic-Bare-Metal) |EBM instances operate on dedicated physical servers, combining features of ECS and physical machines (full processor characteristics and resource isolation). EBM instances eliminate virtualization overhead and performance loss, utilizing 100% of compute resources. This type is applicable for business scenarios with high requirements for security and compliance. |
   |[Heterogeneous Compute-optimized](https://docs.byteplus.com/en/docs/ecs/Heterogeneous-computing) |* GPU Accelerated: A GPU accelerator card is added to the general ECS instance, combining GPU and CPU computing capacities. While providing super computing capabilities, this instance type also offers the flexibility and on\-demand usage of general ECS instances. This type is applicable for scenarios like AI training, AI inference, scientific computation, and video rendering.<br><br>* HPC\-optimized: Based on the GPU Accelerated type, an RDMA network is added, which significantly enhances network performance and increases the speed\-up ratio of large\-scale clusters. This type is applicable for scenarios like high\-performance computing, artificial intelligence, and machine learning. |

* Based on scenario and performance, ECS instances are divided into General\-purpose, Compute\-optimized, Memory\-optimized, Big Data, etc. For example, some families excel in computing performance, applicable for handling massive computational tasks, and some families excel in storage capability, applicable for data\-intensive applications.

## Instance type families & instance types

An instance type family is a collection of instance types with common characteristics. Instance types within a family typically use the same processor and vCPU/memory ratio and share similar performance characteristics and applicable business scenarios.

An instance type is a specific configuration option under an instance type family. For an instance type, key metrics of an ECS instance are defined, such as the number of vCPUs, memory size, image type, storage type (such as volume type and capacity), and network performance (such as bandwidth, maximum throughput).

An instance type family can have multiple instance types, with higher specifications offering better performance. For information about instance type families provided by the platform, please refer to the [Instance type family list](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types#.5a6e5L6L6KeE5qC85peP5YiX6KGo).

## Instance type family list

> **warning**

* > The maximum number of volumes varies based on instance type (refer to the "Volume Quantity" column in the "Instance types and metrics" table for each instance type). However, if the ECS instance is created based on a CentOS 6.x image, a maximum of 8 volumes can be mounted (including one system volume).

* > The "shared" in "shared instances" refers to the CPU resource sharing mode. Shared instances and burstable instances use this mode. All other instance types adopt a dedicated CPU mode. [Learn more](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#1J0if7MX)

**x86 Compute-optimized Instance Families**

|**Type** |**Instance type family** |
|---|---|
|General\-purpose |[g4i](https://docs.byteplus.com/en/docs/ecs/General-purpose) |
||[g3i](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNp) |
||[g3a](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNh) |
||[g3il](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNpbA==) |
||[g3al](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNhbA==) |
|Compute\-optimized |[c4i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized) |
||[c3i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNp) |
||[c3a](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNh) |
||[c3il](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNpbA==) |
||[c3al](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNhbA==) |
|Memory\-optimized |[r4i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized) |
||[r3i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#uvEC2ygI) |
||[r3a](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#qEWtPNM0) |
||[r3il](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#JirQoNCM) |
||[r3al](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#zOMddgDz) |
|Local SSD |[i3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#8IH6RHiz) |
||[i4](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based?lang=en#8Z8NAkLv) |
||[i4ag](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#UtdiwP1E) |
|Big Data |[d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based#sRuv8d0D) |
||[d4c](https://docs.byteplus.com/en/docs/ecs/Big-data-based#jqmxfbz9) |
||[d4s](https://docs.byteplus.com/en/docs/ecs/Big-data-based#ypXfbn0a) |
|Burstable instance |[t2](https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances#BuPqqP53) |
|Shared |[e](https://docs.byteplus.com/en/docs/ecs/Shared#0C5qnIXc) |

**EBM Instance Families**

|Type |**Instance type family** |
|---|---|
|General\-purpose EBM |[ebmg3id](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM#.6YCa55So5Z6L5by55oCn6KO46YeR5bGeZWJtZzNpZA==) |
||[ebmg3ad](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM#.6YCa55So5Z6L5by55oCn6KO46YeR5bGeZWJtZzNhZA==) |
|Compute\-optimized EBM |[ebmc3id](https://docs.byteplus.com/en/docs/ecs/Compute-optimized-EBM#.6K6h566X5Z6L5by55oCn6KO46YeR5bGeZWJtYzNpZA==) |
|Local SSD EBM |[ebmi3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-EBM#HNkJ3Plb) |

**Heterogeneous Compute-optimized Instance Families**

|**Type** |**Instance type family** |
|---|---|
|GPU Accelerated<br><br> |[pni3l](https://docs.byteplus.com/en/docs/ecs/GPU-Compute#fxeOxsIS) |
||[gni3c](https://docs.byteplus.com/en/docs/ecs/GPU-Compute#AmEoLCBb) |
||[ebmgni3c](https://docs.byteplus.com/en/docs/ecs/GPU-Compute#A4qG3ldp) |
|HPC\-optimized |[gni3cl](https://docs.byteplus.com/en/docs/ecs/GPU-Compute#SBCQw2X5) |
||[hpcpni3ln](https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h#ycaqZd1y) |
||[ebmhpcpni3ln](https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h#NOjpcVyU) |
||[ebmhpcpni3l](https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h#1Tpv4eZe) |
||[hpcpni3h](https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h#8606QuMw) |

**Discontinued Instance Types**

|**Type** |**Instance type family** |
|---|---|
|General\-purpose |g2i |
|Compute\-optimized |c2i |
|Memory\-optimized |r2i |
|Local SSD |i2 |
|Big Data |d2 |
