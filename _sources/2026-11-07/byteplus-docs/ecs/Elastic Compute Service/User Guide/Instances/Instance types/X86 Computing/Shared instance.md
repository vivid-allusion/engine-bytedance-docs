---
title: "Shared instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Shared"
---

<span id=".5qaC6L-w"></span>
## Overview

Shared instances use an unbound CPU scheduling mode, where each vCPU is randomly assigned to any idle CPU hyperthread. vCPUs from different instances compete for physical CPU resources, which can result in unstable and fluctuating computing performance under high load. An availability SLA is provided, but there is no performance SLA guarantee, meaning that performance cannot be ensured under all circumstances. Compared with other instance types, such as general\-purpose and compute\-optimized instances, shared instances are designed to share compute resources. As a result, the compute performance of an instance cannot be guaranteed to remain stable, but the cost is lower. If your business has specific requirements for performance, please choose instances with dedicated CPUs. This article introduces the features, metrics, and usage scenarios of Shared Instance Families.

In a shared instance, "shared" refers to the sharing mode of CPU resources, [Learn more](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#1J0if7MX). Instances that adopt this model include:


* [Shared Economy e](https://docs.byteplus.com/en/docs/ecs/Shared#0C5qnIXc)

* [Burstable instance](https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To learn about instance types, estimated instance fees, to view the status of instance specification modifications, and to understand instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance Type and Specification Overview</a>.</div>


<span id="0C5qnIXc"></span>
## Sharing Economy e

**Specifications and features**


|type |Performance |
|---|---|
|Compute |* Processor: Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors<br><br>* Supports multiple processor\-to\-memory ratios, including 1:1, 1:2, and 1:4<br><br>* Supports up to 8 vCPUs, 32 GiB |
|Storage |* Supports enhanced SSD volumes and TSSD volumes.<br><br>* Storage I/O performance is related to computing specifications; higher specifications deliver better performance. |
|Network |* Instance network performance has burst capability<br><br>* Network performance is related to computing specifications; higher specifications result in better performance. |


**Scenarios**


* Small and medium\-sized websites

* Web application server

* Lightweight databases and caches

* Lightweight enterprise applications and integrated application services

* Development environments, build servers, code repositories, microservices, and testing and staging environments


**Specifications and metric details**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Due to differences in business scenarios, maximum throughput (PPS) varies significantly. Therefore, we recommend that you conduct a business stress test to understand the performance of the instance, so that you can select the appropriate instance type.</div>


* <div data-tips="true" data-tips-type="tip">The network performance of this instance supports burst capability. See the table below for details.</div>




|Instance type |vCPU |Memory (GiB) |Outbound and inbound network bandwidth: baseline and burst capability (Gbit/s) |Maximum queues per network interface |elastic network interface (including one primary network interface) |Private IP for a single network interface |Volume IOPS (×10,000) |Volume bandwidth (Gbit/s) |
|---|---|---|---|---|---|---|---|---|
|ecs.e\-c1m1.large |2 |2 |<div style="text-align: center"><br>0.2/max. 2</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>0.8</div><br> |
|ecs.e\-c1m2.large |2 |4 |<div style="text-align: center"><br>0.2/max. 2</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>0.8</div><br> |
|ecs.e\-c1m4.large |2 |8 |<div style="text-align: center"><br>0.4/max. 2</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>1.8</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.e\-c1m1.xlarge |4 |4 |<div style="text-align: center"><br>0.4/max. 2</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>1.8</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.e\-c1m2.xlarge |4 |8 |<div style="text-align: center"><br>0.4/max. 3</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>1.8</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.e\-c1m4.xlarge |4 |16 |<div style="text-align: center"><br>0.8/max. 4</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>1.8</div><br> |<div style="text-align: center"><br>1.2</div><br> |
|ecs.e\-c1m1.2xlarge |8 |8 |<div style="text-align: center"><br>0.8/max. 4</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1.2</div><br> |
|ecs.e\-c1m2.2xlarge |8 |16 |<div style="text-align: center"><br>1.2/max. 6</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2.4</div><br> |<div style="text-align: center"><br>1.2</div><br> |
|ecs.e\-c1m4.2xlarge |8 |32 |<div style="text-align: center"><br>1.2/max. 6</div><br> |<div style="text-align: center"><br>1</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2.4</div><br> |<div style="text-align: center"><br>1.2</div><br> |


<span id=".5YWx5Lqr5Z6L5a6e5L6LczI="></span>
## FAQs


* [What does "shared" mean in a shared instance?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#bs5wL0HW)

* [What is the difference between Shared instances and dedicated instance types (such as General-purpose, EBM, and GPU Accelerated)?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#1J0if7MX)

* [Does a shared instance have guaranteed performance?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#ANU9dKM8)
