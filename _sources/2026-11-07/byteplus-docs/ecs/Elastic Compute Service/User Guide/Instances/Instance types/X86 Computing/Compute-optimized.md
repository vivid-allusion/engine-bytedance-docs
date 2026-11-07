---
title: "Compute-optimized"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Computing-optimized"
---

Overview

The processor\-to\-memory ratio of a Compute\-optimized instance is typically 1:2, offering reliable and stable computing performance. It is applicable for compute\-intensive applications such as batch processing workloads and distributed analysis. This topic describes the features, metric data, and applicable scenarios of each instance family of Compute\-optimized instances. By referring to this topic, you can select an instance type that meets your business needs. This helps you ensure that the selected type meets the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


<span id="DvtwPnpi"></span>
## Compute\-optimized c4i

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br>* Max.: 32 vCPUs |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 65 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 64 Gbit/s<br><br>* Maximum throughput: 24,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* Jumbo Frame is supported. [Learn more](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface)<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Web front\-end servers

* Data analysis and computing

* Small and medium\-sized database systems, caches, and clusters for searching

* High\-definition video transcoding


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>


* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See the details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>




|<div style="text-align: center"><br><strong>Instance specification</strong></div><br> |<div style="text-align: center"><br><strong>vCPU</strong></div><br> |<div style="text-align: center"><br><strong>Memory (GiB)</strong></div><br> |<div style="text-align: center"><br><strong>Network bandwidth (outbound + inbound, base/burst, Gbit/s)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum throughput (outbound + inbound) (10,000 PPS)</strong></div><br> |<div style="text-align: center"><br><strong>Connections (10,000)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum queues per network interface (primary network interface)</strong></div><br> |<div style="text-align: center"><br><strong>Elastic network interfaces (including 1 primary network interface)</strong></div><br> |<div style="text-align: center"><br><strong>Private IP addresses for one network interface</strong></div><br> |<div style="text-align: center"><br><strong>Volume IOPS (basic/burst, unit: 10,000)</strong></div><br> |<div style="text-align: center"><br><strong>Volume bandwidth (basic/burst, Gbit/s)</strong></div><br> |<div style="text-align: center"><br><strong>Volumes (including 1 system volume)</strong></div><br> |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c4i.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2/max. 6</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |
|ecs.c4i.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4/max. 6</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |
|ecs.c4i.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |
|ecs.c4i.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8/max. 10</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |
|ecs.c4i.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10/\-\-</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |


<span id=".6K6h566X5Z6LYzNpbA=="></span>
## Compute\-optimized c3il

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance, you can use Windows, Linux, or veLinux images.</div>


* <div data-tips="true" data-tips-type="tip">This instance type family has good compatibility with drivers and does not heavily rely on Virtio1.1 drivers.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) or the 5th\-generation Intel® Xeon® Scalable processor (Emerald Rapids), with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Web front\-end servers

* Game servers

* Data analysis, batch computing, video encoding/decoding

* AI inference applications


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c3il.large |2 |4 |2/max. 3 |30 |25 |2 |3 |6 |1 |1.5 |9 |
|ecs.c3il.xlarge |4 |8 |3/max. 5 |50 |25 |4 |4 |15 |2 |2 |9 |
|ecs.c3il.2xlarge |8 |16 |4/max. 6 |60 |25 |8 |4 |15 |3 |3 |16 |
|ecs.c3il.4xlarge |16 |32 |5/max. 10 |100 |60 |8 |8 |30 |4 |5 |16 |
|ecs.c3il.8xlarge |32 |64 |10/\-\- |180 |120 |16 |8 |30 |8 |6 |16 |
|ecs.c3il.12xlarge |48 |96 |13/\-\- |250 |180 |16 |8 |30 |12 |8 |16 |
|ecs.c3il.16xlarge |64 |128 |18/\-\- |350 |240 |32 |8 |30 |17 |10 |16 |
|ecs.c3il.23xlarge |90 |216 |27/\-\- |500 |300 |32 |8 |30 |19 |13 |16 |
|ecs.c3il.29xlarge |114 |228 |27/\-\- |500 |300 |32 |8 |30 |19 |13 |16 |


<span id=".6K6h566X5Z6LYzNhbA=="></span>
## Compute\-optimized c3al

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance, you can use Windows and other images. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>


* <div data-tips="true" data-tips-type="tip">This instance has good compatibility with drivers and does not rely on Virtio1.1 drivers.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Web front\-end servers

* Data analysis and computing

* Small and medium\-sized database systems, caches, and clusters for searching

* High\-definition video transcoding


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit:10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c3al.large |2 |4 |1.5/max. 6 |60 |25 |2 |3 |6 |1/max. 4 |1/max. 4 |5 |
|ecs.c3al.xlarge |4 |8 |2.5/max. 6 |90 |25 |4 |3 |15 |1.5/max. 4 |1.5/max. 5 |9 |
|ecs.c3al.2xlarge |8 |16 |4/max. 10 |100 |25 |8 |3 |15 |2/max. 6 |2/max. 5 |16 |
|ecs.c3al.4xlarge |16 |32 |7/max. 10 |120 |30 |16 |6 |30 |3/max. 6 |3/max. 5 |16 |
|ecs.c3al.8xlarge |32 |64 |10/max. 12 |180 |40 |24 |6 |30 |4/max. 6 |3.5/max. 5 |16 |
|ecs.c3al.12xlarge |48 |96 |12/max. 15 |200 |50 |32 |8 |30 |5/max. 6 |4/max. 5 |16 |
|ecs.c3al.16xlarge |64 |128 |15/\-\- |270 |70 |48 |8 |30 |7/\-\- |5/\-\- |16 |
|ecs.c3al.23xlarge |92 |184 |22/\-\- |400 |100 |64 |8 |30 |10/\-\- |8/\-\- |16 |
|ecs.c3al.32xlarge |128 |256 |30/\-\- |550 |140 |64 |8 |30 |14/\-\- |10/\-\- |16 |


<span id=".6K6h566X5Z6LYzNp"></span>
## Compute\-optimized c3i

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance family, you can not use Windows images.</div>


* <div data-tips="true" data-tips-type="tip">If you want to use ecs.c3i.48xlarge or ecs.c3i.60xlarge, please contact your account manager to apply.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) or the 5th\-generation Intel® Xeon® Scalable processor (Emerald Rapids), with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br>* Max.: 240 vCPUs, 480 GiB |
|Storage |* You can use ESSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage I/O performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Compute\-intensive scenarios such as data analysis, batch computing, video encoding/decoding, video rendering, and high\-performance scientific and engineering applications.

* General\-purpose applications such as MySQL database, Redis database, Nginx, and middleware MQ.

* Scenarios with high maximum throughput requirements, such as video barrage and telecom service forwarding.

* AI inference and training. This instance family is applicable for small and medium\-sized deep\-learning and training models and can enhance the deep\-learning and training performance on CPUs.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c3i.large |2 |4 |2.5/max. 12 |130 |Max. 30 |2 |3 |6 |1.5/max. 6 |1.5/max. 6 |9 |
|ecs.c3i.xlarge |4 |8 |4/max. 12 |140 |Max. 30 |4 |4 |15 |3/max. 6 |2/max. 6 |9 |
|ecs.c3i.2xlarge |8 |16 |6/max. 12 |160 |Max. 30 |8 |4 |15 |4/max. 8 |3/max. 6 |16 |
|ecs.c3i.4xlarge |16 |32 |12/max. 30 |300 |50 |8 |8 |30 |6/max. 8 |5/max. 6 |16 |
|ecs.c3i.8xlarge |32 |64 |24/max. 30 |600 |100 |16 |8 |30 |10/\-\- |6/\-\- |16 |
|ecs.c3i.12xlarge |48 |96 |36/\-\- |900 |150 |16 |8 |30 |15/\-\- |8/\-\- |16 |
|ecs.c3i.16xlarge |64 |128 |42/\-\- |1,200 |200 |32 |8 |30 |20/\-\- |10/\-\- |16 |
|ecs.c3i.24xlarge |96 |192 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
|ecs.c3i.30xlarge |120 |240 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
|ecs.c3i.48xlarge |192 |384 |96/\-\- |3600 |600 |32 |15 |30 |60/\-\- |32/\-\- |16 |
|ecs.c3i.60xlarge |240 |480 |96/\-\- |3600 |600 |32 |15 |30 |60/\-\- |32/\-\- |16 |


<span id=".6K6h566X5Z6LYzNh"></span>
## Compute\-optimized c3a

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information on images that can be used for this instance, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>


**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br>* Max.: 192 vCPUs, 384 GiB<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes only. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage I/O performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 64 Gbit/s<br><br>* Maximum throughput: 18,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Website/application servers

* Game servers

* Audio/video transcoding applications

* Small and medium\-sized database systems

* AI training and inference


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance type |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c3a.large |2 |4 |1.5/max. 12.5 |130 |Max. 25 |2 |3 |6 |1/max. 4 |1/max. 4 |5 |
|ecs.c3a.xlarge |4 |8 |2.5/max. 12.5 |140 |Max. 25 |4 |3 |15 |1.5/max. 4 |1.5/max. 5 |9 |
|ecs.c3a.2xlarge |8 |16 |4/max. 12.5 |160 |Max. 25 |8 |3 |15 |2/max. 6 |2/max. 5 |16 |
|ecs.c3a.4xlarge |16 |32 |7/max. 12.5 |200 |30 |8 |6 |30 |3/max. 6 |3/max. 5 |16 |
|ecs.c3a.8xlarge |32 |64 |12/max. 25 |300 |50 |16 |6 |30 |5/max. 8 |3.5/max. 5 |16 |
|ecs.c3a.12xlarge |48 |96 |16/max. 25 |450 |75 |16 |8 |30 |8/\-\- |4/max. 5 |16 |
|ecs.c3a.16xlarge |64 |128 |20/max. 25 |600 |100 |24 |8 |30 |10/\-\- |5/\-\- |16 |
|ecs.c3a.24xlarge |96 |192 |32/\-\- |900 |150 |32 |8 |30 |15/\-\- |8/\-\- |16 |
|ecs.c3a.32xlarge |128 |256 |40/\-\- |1,200 |200 |32 |8 |30 |20/\-\- |10/\-\- |16 |
|ecs.c3a.48xlarge |192 |384 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
