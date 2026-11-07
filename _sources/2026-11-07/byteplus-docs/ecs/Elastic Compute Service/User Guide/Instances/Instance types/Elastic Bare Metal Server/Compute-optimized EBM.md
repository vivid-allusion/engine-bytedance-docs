---
title: "Compute-optimized EBM"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Compute-optimized-EBM"
---

<span id=".5qaC6L-w"></span>
## Overview

Please refer to the introduction below to select the instance type that meets your business requirements, and ensure that the selected type satisfies the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To learn about instance types, estimate instance fees, view the status of Modify Instance Spec, and understand instance naming rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance Type and Specification Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information about Elastic Bare Metal (EBM) instances, refer to <a href="https://docs.byteplus.com/en/docs/ecs/EBM-overview">Elastic Bare Metal Overview</a>.</div>




|Instance type |Scenarios |
|---|---|
|[Compute-optimized EBM ebmc3id](https://docs.byteplus.com/en/docs/ecs/Compute-optimized-EBM#.6K6h566X5Z6L5by55oCn6KO46YeR5bGeZWJtYzNpZA==) |Compute\-optimized dedicated compute resources: Provides dedicated physical compute resources, suitable for workloads with high compute performance requirements or those that require direct access to physical resources. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The specifications and lifecycle of SSD local disks are tied to the instance. Independent purchase, as well as independent mounting, unmounting, or scaling up, is not supported.

* When you delete an instance, data on the local disk will be automatically cleared. Please [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) in advance.

* If the physical server fails or the local disk is damaged, there is a risk of data loss on the local disk. Do not store data that needs to be stored long term on the local disk, and promptly perform [data backup](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration).

   * We recommend that you adopt a high availability architecture by distributing your workloads across multiple instances or using volume backups to ensure high availability and data reliability.

   * If your application's architecture cannot ensure data reliability, we strongly recommend that you select Volume to back up your data.


<span id=".6K6h566X5Z6L5by55oCn6KO46YeR5bGeZWJtYzNpZA=="></span>
## Compute\-optimized EBM ebmc3id

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently available for sale only in certain regions or availability zones. Please refer to the console for the most up\-to\-date information. To use, please contact your account manager to request access.</div>


* <div data-tips="true" data-tips-type="tip">The instance type can not be changed.</div>



**Specifications and features**


|type |Performance |
|---|---|
|Compute |* ecs.ebmc3id.48xlarge：<br><br>   * Processor: Equipped with 4th Gen Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Sapphire Rapids), processor base frequency of 2.6 GHz, all\-core turbo frequency of 3.1 GHz<br><br>   * The processor\-to\-memory ratio is 1:2.7.<br><br>* ecs.ebmc3id.60xlarge：<br><br>   * Processor: Equipped with 5th generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Emerald Rapids), with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.0 GHz<br><br>   * The processor\-to\-memory ratio is 1 to 2.1. |
|Storage |* Supports Enhanced SSD Volume and allows up to 8 volumes to be mounted, including one System Volume.<br><br>* Equipped with high\-performance SSD local disks (high IOPS, high throughput, and low access latency)<br><br>* Storage I/O performance is related to computing specifications; the higher the specifications, the better the performance. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36 million PPS |


**Specifications and metric details**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to differences in business scenarios, the PPS (packets per second) of network packet transmission can vary significantly. Therefore, it is recommended that you perform a business stress test to understand the performance of the instance, so that you can select the appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |Local storage (GB) |Outbound and inbound network bandwidth capability (Gbit/s) |Maximum throughput (send + receive) (10,000 PPS) |Number of connections (in ten thousands) |Maximum queues per network interface |an elastic network interface (including a primary network interface) |Private IP address for a single network interface |Volume IOPS (×10,000) |Volume bandwidth (Gbit/s) |Number of volumes (including one system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmc3id.48xlarge |192 |512 |3840 \* 2 |96 |3600 |600 |32 |8 |30 |60 |32 |8 |
|ecs.ebmc3id.60xlarge |240 |512 |3840 \* 2 |96 |3600 |600 |32 |8 |30 |60 |32 |8 |
