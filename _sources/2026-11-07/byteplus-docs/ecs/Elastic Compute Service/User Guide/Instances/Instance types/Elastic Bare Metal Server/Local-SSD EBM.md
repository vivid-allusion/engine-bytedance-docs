---
title: "Local-SSD EBM"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Local-SSD-EBM"
---

<span id=".5qaC6L-w"></span>
## Overview

Please refer to the information below to select the instance type that meets your business requirements, and ensure that the selected type satisfies the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information about Elastic Bare Metal instances, refer to <a href="https://docs.byteplus.com/en/docs/ecs/EBM-overview">Elastic Bare Metal Overview</a>.</div>




|Instance type |Scenarios |
|---|---|
|[Local-SSD EBM ebmi3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-EBM#HNkJ3Plb) |IO\-intensive applications: suitable for scenarios such as distributed databases, high\-performance NoSQL databases, and Elasticsearch. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The specifications and lifecycle of SSD local disks are tied to the instance. They cannot be purchased separately, nor can they be mounted, unmounted, or scaled up separately.

* When you delete an instance, data on the local disk will be automatically cleared. Please make sure to [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) in advance.

* If the physical machine crashes or the local disk is damaged, there is a risk of data loss on the local disk. Do not store data that needs to be retained for a long time on the local disk, and promptly perform [data backup](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration).

   * We recommend adopting a high availability architecture by distributing your services across multiple instances or using volume backups to ensure the high availability of your services and the reliability of your data.

   * If the data architecture of your application is not reliable, we strongly recommend that you use volumes for data backup.


<span id="HNkJ3Plb"></span>
## Local\-SSD EBM ebmi3s

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently in Beta. To request a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="tip">The instance type cannot be changed.</div>



**Specifications and features**


|type |Performance |
|---|---|
|Compute |* Equipped with 4th Gen Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Sapphire Rapids), with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz<br><br>* The processor\-to\-memory ratio is 1:8. |
|Storage |* Supports Enhanced SSD Volumes; up to 16 volumes can be mounted (including one system volume).<br><br>* Equipped with high\-performance local SSDs (high IOPS, high throughput, and low access latency) |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36 million PPS |


**Specifications and metric details**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to differences in business scenarios, there are significant differences in maximum throughput (PPS). Therefore, it is recommended that you perform a business stress test to understand the performance of the instance, so that you can select the appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |Local storage (GB) |(outbound and inbound) network bandwidth capability (Gbit/s) |Maximum throughput (inbound and outbound) (10,000 PPS) |Number of connections (×10,000) |Maximum queues per network interface |Elastic network interfaces (including a primary network interface) |Private IP for a single network interface |Volume IOPS (×10,000) |Volume bandwidth (Gbit/s) |Number of volumes (including one system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmi3s.48xlarge |192 |1536 |3840 \* 16 |96 |3600 |600 |32 |15 |30 |60 |32 |16 |
