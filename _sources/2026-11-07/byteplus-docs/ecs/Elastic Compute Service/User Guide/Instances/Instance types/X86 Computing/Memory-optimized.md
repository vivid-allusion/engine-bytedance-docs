---
title: "Memory-optimized"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Memory-optimized"
---

<span id="WC1SGCCF"></span>
## Overview

The processor\-to\-memory ratio for Memory\-optimized instances is typically 1:8 (1:16 for re3il), offering high memory capacity. They are applicable for scenarios that require high memory due to massive data access and big data. The scenarios include big data analysis, in\-memory databases, etc. This topic describes the features, metric data, and applicable scenarios of each instance family of Memory\-optimized instances. By referring to this topic, you can select an instance type that meets your business needs. This helps you ensure that the selected type meets the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


<span id="mgMpZfw5"></span>
## Memory\-optimized r4i

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 25 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* Jumbo Frame is supported. [Learn more](https://docs.byteplus.com/en/docs/ecs/Enabling_or_Disabling_jumbo_frames)<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* In\-memory databases, high\-performance databases, data analysis and mining, and distributed in\-memory cache

* Hadoop, Spark clusters, and other enterprise applications that require large memory


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>


* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See the details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>




|<div style="text-align: center"><br><strong>Instance specification</strong></div><br> |<div style="text-align: center"><br><strong>vCPU</strong></div><br> |<div style="text-align: center"><br><strong>Memory (GiB)</strong></div><br> |<div style="text-align: center"><br><strong>Network bandwidth (outbound + inbound, base/burst, Gbit/s)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum throughput (outbound + inbound) (10,000 PPS)</strong></div><br> |<div style="text-align: center"><br><strong>Connections (10,000)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum queues per network interface (primary network interface)</strong></div><br> |<div style="text-align: center"><br><strong>Elastic network interfaces (including 1 primary network interface)</strong></div><br> |<div style="text-align: center"><br><strong>Private IP addresses for one network interface</strong></div><br> |<div style="text-align: center"><br><strong>Volume IOPS (basic/burst, unit: 10,000)</strong></div><br> |<div style="text-align: center"><br><strong>Volume bandwidth (basic/burst, Gbit/s)</strong></div><br> |<div style="text-align: center"><br><strong>Volumes (including 1 system volume)</strong></div><br> |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.r4i.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2/max. 6</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |
|ecs.r4i.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4/max. 6</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |
|ecs.r4i.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |
|ecs.r4i.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8/max. 10</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |
|ecs.r4i.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10/\-\-</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |


<span id="JirQoNCM"></span>
## Memory\-optimized r3il

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance, you can use Windows, Linux, or veLinux images.</div>


* <div data-tips="true" data-tips-type="tip">This instance type family has good compatibility with drivers and does not heavily rely on Virtio1.1 drivers.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) or the 5th\-generation Intel® Xeon® Scalable processor (Emerald Rapids), with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* In\-memory databases, high\-performance databases, data analysis and mining, and distributed in\-memory cache

* Hadoop, Spark clusters, and other enterprise applications that require large memory


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.r3il.large |2 |16 |2/max. 3 |30 |25 |2 |3 |6 |1 |1.5 |9 |
|ecs.r3il.xlarge |4 |32 |3/max. 5 |50 |25 |4 |4 |15 |2 |2 |9 |
|ecs.r3il.2xlarge |8 |64 |4/max. 6 |60 |25 |8 |4 |15 |3 |3 |16 |
|ecs.r3il.4xlarge |16 |128 |5/max. 10 |100 |60 |8 |8 |30 |4 |5 |16 |
|ecs.r3il.8xlarge |32 |256 |10/\-\- |180 |120 |16 |8 |30 |8 |6 |16 |
|ecs.r3il.12xlarge |48 |384 |13/\-\- |250 |180 |16 |8 |30 |12 |8 |16 |
|ecs.r3il.16xlarge |64 |512 |18/\-\- |350 |240 |32 |8 |30 |17 |10 |16 |
|ecs.r3il.29xlarge |114 |974 |27/\-\- |500 |300 |32 |8 |30 |19 |13 |16 |


<span id="zOMddgDz"></span>
## Memory\-optimized r3al

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance, you can use Windows and other images. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>


* <div data-tips="true" data-tips-type="tip">This instance has good compatibility with drivers and does not rely on Virtio1.1 drivers.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Web front\-end servers

* Database systems, caches, and clusters for searching

* Hadoop, Spark clusters, and other enterprise applications that require large memory

* Distributed memory caches, such as Redis

* Data analysis and computing


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit:10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.r3al.large |2 |16 |1.5/max. 6 |60 |25 |2 |3 |6 |1/max. 4 |1/max. 4 |5 |
|ecs.r3al.xlarge |4 |32 |2.5/max. 6 |90 |25 |4 |3 |15 |1.5/max. 4 |1.5/max. 5 |9 |
|ecs.r3al.2xlarge |8 |64 |4/max. 10 |100 |25 |8 |3 |15 |2/max. 6 |2/max. 5 |16 |
|ecs.r3al.4xlarge |16 |128 |7/max. 10 |120 |30 |16 |6 |30 |3/max. 6 |3/max. 5 |16 |
|ecs.r3al.8xlarge |32 |256 |10/max. 12 |180 |40 |24 |6 |30 |4/max. 6 |3.5/max. 5 |16 |
|ecs.r3al.12xlarge |48 |384 |12/max. 15 |200 |50 |32 |8 |30 |5/max. 6 |4/max. 5 |16 |
|ecs.r3al.16xlarge |64 |512 |15/\-\- |270 |70 |48 |8 |30 |7/\-\- |5/\-\- |16 |
|ecs.r3al.23xlarge |92 |736 |22/\-\- |400 |100 |64 |8 |30 |10/\-\- |8/\-\- |16 |


<span id="uvEC2ygI"></span>
## Memory\-optimized r3i

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance family, you can not use Windows images.</div>


* <div data-tips="true" data-tips-type="tip">If you want to use ecs.r3i.48xlarge or ecs.r3i.60xlarge, please contact your account manager to apply.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) or the 5th\-generation Intel® Xeon® Scalable processor (Emerald Rapids), with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br>* Max.: 240 vCPUs, 1920 GiB |
|Storage |* You can use ESSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage I/O performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* In\-memory databases, high\-performance databases, data analysis and mining, and distributed in\-memory cache

* Hadoop, Spark clusters, and other enterprise applications that require large memory

* General\-purpose applications such as MySQL database, Redis database, Nginx, and middleware MQ.

* Scenarios with high maximum throughput requirements, such as video barrage and telecom service forwarding.

* AI inference and training. This instance family is applicable for small and medium\-sized deep\-learning and training models and can enhance the deep\-learning and training performance on CPUs.

* Compute\-intensive scenarios such as video encoding/decoding, video rendering, gaming, and engineering applications.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.r3i.large |2 |16 |2.5/max. 12 |130 |Max. 30 |2 |3 |6 |1.5/max. 6 |1.5/max. 6 |9 |
|ecs.r3i.xlarge |4 |32 |4/max. 12 |140 |Max. 30 |4 |4 |15 |3/max. 6 |2/max. 6 |9 |
|ecs.r3i.2xlarge |8 |64 |6/max. 12 |160 |max. 30 |8 |4 |15 |4/max. 8 |3/max. 6 |16 |
|ecs.r3i.4xlarge |16 |128 |12/max. 30 |300 |50 |8 |8 |30 |6/max. 8 |5/max. 6 |16 |
|ecs.r3i.8xlarge |32 |256 |24/max. 30 |600 |100 |16 |8 |30 |10/\-\- |6/\-\- |16 |
|ecs.r3i.12xlarge |48 |384 |36/\-\- |900 |150 |16 |8 |30 |15/\-\- |8/\-\- |16 |
|ecs.r3i.16xlarge |64 |512 |42/\-\- |1,200 |200 |32 |8 |30 |20/\-\- |10/\-\- |16 |
|ecs.r3i.24xlarge |96 |768 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
|ecs.r3i.30xlarge |120 |960 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
|ecs.r3i.48xlarge |192 |1,536 |96/\-\- |3600 |600 |32 |15 |30 |60/\-\- |32/\-\- |16 |
|ecs.r3i.60xlarge |240 |1,920 |96/\-\- |3600 |600 |32 |15 |30 |60/\-\- |32/\-\- |16 |


<span id="qEWtPNM0"></span>
## Memory\-optimized r3a

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information on images that can be used for this instance, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>


**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:8.<br><br>* Max.: 96 vCPUs, 768 GiB<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes only. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage I/O performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 32 Gbit/s<br><br>* Maximum throughput: 9,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications with high memory capacity requirement

* Website/application servers

* Audio/video transcoding applications

* In\-memory database

* AI training and inference


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.r3a.large |2 |16 |1.5/max. 12.5 |130 |Max. 25 |2 |3 |6 |1/max. 4 |1/max. 4 |5 |
|ecs.r3a.xlarge |4 |32 |2.5/max. 12.5 |140 |Max. 25 |4 |3 |15 |1.5/max. 4 |1.5/max. 5 |9 |
|ecs.r3a.2xlarge |8 |64 |4/max. 12.5 |160 |Max. 25 |8 |3 |15 |2/max. 6 |2/max. 5 |16 |
|ecs.r3a.4xlarge |16 |128 |7/max. 12.5 |200 |30 |8 |6 |30 |3/max. 6 |3/max. 5 |16 |
|ecs.r3a.8xlarge |32 |256 |12/max. 25 |300 |50 |16 |6 |30 |5/max. 8 |3.5/max. 5 |16 |
|ecs.r3a.12xlarge |48 |384 |16/max. 25 |450 |75 |16 |8 |30 |8/\-\- |4/max. 5 |16 |
|ecs.r3a.16xlarge |64 |512 |20/max. 25 |600 |100 |24 |8 |30 |10/\-\- |5/\-\- |16 |
|ecs.r3a.24xlarge |96 |768 |32/\-\- |900 |150 |32 |8 |30 |15/\-\- |8/\-\- |16 |
