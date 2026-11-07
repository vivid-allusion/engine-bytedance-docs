---
title: "General-purpose"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/General-purpose"
---

<span id=".5qaC6L-w"></span>
## Overview

The processor\-to\-memory ratio of General\-purpose instances is usually 1:4, providing balanced compute, memory, and network resources. This instance type is applicable for scenarios such as web servers, databases, AI inference, and data analysis. This topic describes the features, metrics, and applicable scenarios of each instance family of General\-purpose instances. By referring to this topic, you can select an instance type that meets your business needs. This helps you ensure that the selected type meets the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


<span id="ZHRHYffU"></span>
## General\-purpose g4i

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 240 vCPUs |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 65 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 64 Gbit/s<br><br>* Maximum throughput: 24,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* Jumbo Frame is supported. [Learn more](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface)<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Big data applications

* Audio/video transcoding applications

* Website/application servers

* Game servers

* AI training and inference


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>


* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See the details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>




|<div style="text-align: center"><br><strong>Instance specification</strong></div><br> |<div style="text-align: center"><br><strong>vCPU</strong></div><br> |<div style="text-align: center"><br><strong>Memory (GiB)</strong></div><br> |<div style="text-align: center"><br><strong>Network bandwidth (outbound + inbound, basic/burst, Gbit/s)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum throughput (outbound + inbound) (10,000 PPS)</strong></div><br> |<div style="text-align: center"><br><strong>Connections (10,000)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum queues per network interface (primary network interface)</strong></div><br> |<div style="text-align: center"><br><strong>Elastic network interfaces (including 1 primary network interface)</strong></div><br> |<div style="text-align: center"><br><strong>Private IP addresses for one network interface</strong></div><br> |<div style="text-align: center"><br><strong>Volume IOPS (basic/burst, unit: 10,000)</strong></div><br> |<div style="text-align: center"><br><strong>Volume bandwidth (basic/burst, Gbit/s)</strong></div><br> |<div style="text-align: center"><br><strong>Volumes (including 1 system volume)</strong></div><br> |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g4i.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2/max. 6</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |
|ecs.g4i.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4/max. 6</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |
|ecs.g4i.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |
|ecs.g4i.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8/max. 10</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |
|ecs.g4i.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10/\-\-</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |
|ecs.g4i.12xlarge |<div style="text-align: center"><br>48</div><br> |<div style="text-align: center"><br>192</div><br> |<div style="text-align: center"><br>18/max. 20</div><br> |<div style="text-align: center"><br>500</div><br> |<div style="text-align: center"><br>70</div><br> |<div style="text-align: center"><br>48</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>12/\-\-</div><br> |<div style="text-align: center"><br>10/\-\-</div><br> |<div style="text-align: center"><br>33</div><br> |
|ecs.g4i.16xlarge |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>20/\-\-</div><br> |<div style="text-align: center"><br>600</div><br> |<div style="text-align: center"><br>80</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>16/\-\-</div><br> |<div style="text-align: center"><br>12/\-\-</div><br> |<div style="text-align: center"><br>33</div><br> |
|ecs.g4i.20xlarge |<div style="text-align: center"><br>80</div><br> |<div style="text-align: center"><br>384</div><br> |<div style="text-align: center"><br>24/\-\-</div><br> |<div style="text-align: center"><br>800</div><br> |<div style="text-align: center"><br>100</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>20/\-\-</div><br> |<div style="text-align: center"><br>15/\-\-</div><br> |<div style="text-align: center"><br>33</div><br> |
|ecs.g4i.40xlarge |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>768</div><br> |<div style="text-align: center"><br>40/\-\-</div><br> |<div style="text-align: center"><br>1,600</div><br> |<div style="text-align: center"><br>200</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>32/\-\-</div><br> |<div style="text-align: center"><br>24/\-\-</div><br> |<div style="text-align: center"><br>65</div><br> |
|ecs.g4i.60xlarge |<div style="text-align: center"><br>240</div><br> |<div style="text-align: center"><br>1,152</div><br> |<div style="text-align: center"><br>64/\-\-</div><br> |<div style="text-align: center"><br>2,400</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>50</div><br> |<div style="text-align: center"><br>40/\-\-</div><br> |<div style="text-align: center"><br>32/\-\-</div><br> |<div style="text-align: center"><br>65</div><br> |


<span id=".6YCa55So5Z6LZzNpbA=="></span>
## General\-purpose g3il

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance, you can use Windows, Linux, or veLinux images.</div>


* <div data-tips="true" data-tips-type="tip">This instance type family has good compatibility with drivers and does not heavily rely on Virtio1.1 drivers.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) or the 5th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Emerald Rapids), with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Small and medium\-sized database systems, caches, and clusters for searching

* Data analysis, batch computing, video encoding/decoding

* Game servers

* Website/application servers

* AI inference applications


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g3il.large |2 |8 |2/max. 3 |30 |25 |2 |3 |6 |1 |1.5 |9 |
|ecs.g3il.xlarge |4 |16 |3/max. 5 |50 |25 |4 |4 |15 |2 |2 |9 |
|ecs.g3il.2xlarge |8 |32 |4/max. 6 |60 |25 |8 |4 |15 |3 |3 |16 |
|ecs.g3il.4xlarge |16 |64 |5/max. 10 |100 |60 |8 |8 |30 |4 |5 |16 |
|ecs.g3il.8xlarge |32 |128 |10/\-\- |180 |120 |16 |8 |30 |8 |6 |16 |
|ecs.g3il.12xlarge |48 |192 |13/\-\- |250 |180 |16 |8 |30 |12 |8 |16 |
|ecs.g3il.16xlarge |64 |256 |18/\-\- |350 |240 |32 |8 |30 |17 |10 |16 |
|ecs.g3il.23xlarge |90 |472 |27/\-\- |500 |300 |32 |8 |30 |19 |13 |16 |
|ecs.g3il.29xlarge |114 |468 |27/\-\- |500 |300 |32 |8 |30 |19 |13 |16 |


<span id=".6YCa55So5Z6LZzNhbA=="></span>
## General\-purpose g3al

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance, you can use Windows and other images. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>


* <div data-tips="true" data-tips-type="tip">This instance has good compatibility with drivers and does not rely on Virtio1.1 drivers.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Website/application servers

* Small and medium\-sized database systems, caches, and search clusters

* High\-definition video transcoding

* Processing of digital images and model rendering

* Data analysis and computing


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g3al.large |2 |8 |1.5/max. 6 |60 |25 |2 |3 |6 |1/max. 4 |1/max. 4 |5 |
|ecs.g3al.xlarge |4 |16 |2.5/max. 6 |90 |25 |4 |3 |15 |1.5/max. 4 |1.5/max. 5 |9 |
|ecs.g3al.2xlarge |8 |32 |4/max. 10 |100 |25 |8 |3 |15 |2/max. 6 |2/max. 5 |16 |
|ecs.g3al.4xlarge |16 |64 |7/max. 10 |120 |30 |16 |6 |30 |3/max. 6 |3/max. 5 |16 |
|ecs.g3al.8xlarge |32 |128 |10/max. 12 |180 |40 |24 |6 |30 |4/max. 6 |3.5/max. 5 |16 |
|ecs.g3al.12xlarge |48 |192 |12/max. 15 |200 |50 |32 |8 |30 |5/max. 6 |4/max. 5 |16 |
|ecs.g3al.16xlarge |64 |256 |15/\-\- |270 |70 |48 |8 |30 |7/\-\- |5/\-\- |16 |
|ecs.g3al.23xlarge |92 |368 |22/\-\- |400 |100 |64 |8 |30 |10/\-\- |8/\-\- |16 |
|ecs.g3al.32xlarge |128 |512 |30/\-\- |550 |140 |64 |8 |30 |14/\-\- |10/\-\- |16 |
|ecs.g3al.46xlarge |184 |736 |45/\-\- |800 |200 |64 |15 |30 |20/\-\- |15/\-\- |16 |


<span id=".6YCa55So5Z6LZzNp"></span>
## General\-purpose g3i

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For this instance family, you can not use Windows images.</div>


* <div data-tips="true" data-tips-type="tip">If you want to use ecs.g3i.48xlarge or ecs.g3i.60xlarge, please contact your account manager to apply.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) or the 5th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Emerald Rapids), with a processor base frequency of 2.6 GHz and a maximum all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 240 vCPUs, 960 GiB |
|Storage |* You can use ESSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage I/O performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 96 Gbit/s<br><br>* Maximum throughput: 36,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General\-purpose applications such as MySQL database, Redis database, Nginx, and middleware MQ.

* Scenarios with high maximum throughput requirements, such as video barrage and telecom service forwarding.

* Compute\-intensive scenarios such as data analysis, batch computing, video encoding/decoding, video rendering, and high\-performance scientific and engineering applications.

* AI inference and training. This instance family is applicable for small and medium\-sized deep\-learning and training models and can enhance the deep\-learning and training performance on CPUs.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g3i.large |2 |8 |2.5/max. 12 |130 |Max. 30 |2 |3 |6 |1.5/max. 6 |1.5/max. 6 |9 |
|ecs.g3i.xlarge |4 |16 |4/max. 12 |140 |Max. 30 |4 |4 |15 |3/max. 6 |2/max. 6 |9 |
|ecs.g3i.2xlarge |8 |32 |6/max. 12 |160 |Max. 30 |8 |4 |15 |4/max. 8 |3/max. 6 |16 |
|ecs.g3i.4xlarge |16 |64 |12/max. 30 |300 |50 |8 |8 |30 |6/max. 8 |5/max. 6 |16 |
|ecs.g3i.8xlarge |32 |128 |24/max. 30 |600 |100 |16 |8 |30 |10/\-\- |6/\-\- |16 |
|ecs.g3i.12xlarge |48 |192 |36/\-\- |900 |150 |16 |8 |30 |15/\-\- |8/\-\- |16 |
|ecs.g3i.16xlarge |64 |256 |42/\-\- |1,200 |200 |32 |8 |30 |20/\-\- |10/\-\- |16 |
|ecs.g3i.24xlarge |96 |384 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
|ecs.g3i.30xlarge |120 |480 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
|ecs.g3i.48xlarge |192 |768 |96/\-\- |3600 |600 |32 |15 |30 |60/\-\- |32/\-\- |16 |
|ecs.g3i.60xlarge |240 |960 |96/\-\- |3600 |600 |32 |15 |30 |60/\-\- |32/\-\- |16 |


<span id=".6YCa55So5Z6LZzNh"></span>
## General\-purpose g3a

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information on images that can be used for this instance, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility">Instructions on compatibility between AMD instance types and operating systems</a>.</div>


**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation AMD EPYC<sup>™️</sup> Genoa processor with a processor base frequency of 2.6 GHz and a turbo frequency of 3.7 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 192 vCPUs, 768 GiB<br><br><br>> If you need an instance that can provide higher computing resources, please contact the account manager. |
|Storage |* You can use ESSD volumes only. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage I/O performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 64 Gbit/s<br><br>* Maximum throughput: 18,000,000 PPS<br><br>* Small and medium\-sized instances have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Website/application servers

* Game servers

* Audio/video transcoding applications

* AI training and inference


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Small and medium\-sized instances have burstable storage and network performance. See details in the following table. "\-\-" indicates that performance burst is not supported for the current instance type.</div>


* <div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. We recommend that you run a load test to evaluate instance performance and choose an appropriate instance type.</div>




|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (basic/burst, unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g3a.large |2 |8 |1.5/max. 12.5 |130 |Max. 25 |2 |3 |6 |1/max. 4 |1/max. 4 |5 |
|ecs.g3a.xlarge |4 |16 |2.5/max. 12.5 |140 |Max. 25 |4 |3 |15 |1.5/max. 4 |1.5/max. 5 |9 |
|ecs.g3a.2xlarge |8 |32 |4/max. 12.5 |160 |Max. 25 |8 |3 |15 |2/max. 6 |2/max. 5 |16 |
|ecs.g3a.4xlarge |16 |64 |7/max. 12.5 |200 |30 |8 |6 |30 |3/max. 6 |3/max. 5 |16 |
|ecs.g3a.8xlarge |32 |128 |12/max. 25 |300 |50 |16 |6 |30 |5/max. 8 |3.5/max. 5 |16 |
|ecs.g3a.12xlarge |48 |192 |16/max. 25 |450 |75 |16 |8 |30 |8/\-\- |4/max. 5 |16 |
|ecs.g3a.16xlarge |64 |256 |20/max. 25 |600 |100 |24 |8 |30 |10/\-\- |5/\-\- |16 |
|ecs.g3a.24xlarge |96 |384 |32/\-\- |900 |150 |32 |8 |30 |15/\-\- |8/\-\- |16 |
|ecs.g3a.32xlarge |128 |512 |40/\-\- |1,200 |200 |32 |8 |30 |20/\-\- |10/\-\- |16 |
|ecs.g3a.48xlarge |192 |768 |64/\-\- |1,800 |300 |32 |15 |30 |30/\-\- |16/\-\- |16 |
