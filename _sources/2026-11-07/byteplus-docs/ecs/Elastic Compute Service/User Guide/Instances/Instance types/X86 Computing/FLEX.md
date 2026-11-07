---
title: "FLEX"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/FLEX"
---

<span id="W2GJCiyO"></span>
## Overview

FLEX Compute\-optimized​ instance (or FLEX for short) is a Compute\-optimized​ instance based on the X86 architecture, launched by the platform. This instance type is ideal for scenarios where you do not need full CPU power all the time, but require high performance during business peak periods. The following picture shows how the CPU computing power of the FLEX instance changes over time.

For these scenarios, FLEX instances offer more cost\-effective options, with the following key features:


* Mainstream CPU platforms are used to deliver high computing performance.

* CPU sharing technology is used to provide a 40% performance baseline. This means you have at least 40% of CPU performance ensured with FLEX instances at any time.

* With load\-aware and dynamic scheduling, 100% CPU performance can be ensured 95% of the time over a 24\-hour period.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Based on the implementation principle of FLEX instances, we can infer that it is unlikely for a FLEX instance to experience maximum computing power limitation. This issue usually occurs when the instance runs under high CPU load for a long period:</div>


   * <div data-tips="true" data-tips-type="default">When the maximum computing power is limited, if the instance is consuming a large amount of computing power, performance fluctuations may be observed. The platform will use technical measures to quickly restore the computing power of the instance and keep the fluctuation duration within minutes.</div>


   * <div data-tips="true" data-tips-type="default">When the maximum computing power is limited, the instance can still reach 40% of the baseline performance standard.</div>


   * <div data-tips="true" data-tips-type="default">Within a 24\-hour period, the total duration during which the maximum computing power is limited will not exceed 5%.</div>


* <div data-tips="true" data-tips-type="default">If your business requires high performance stability, you can select an instance type with dedicated CPU. For information about instance types, estimated instance fees, instance type changes, and instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>



<span id="9IAeRqiq"></span>
## FLEX g4i\-flex

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz. This instance type is of the Self\-Developed Hardware\-Software Co\-Designed Virtualization Architecture and thereby delivers stable computing power and I/O and network performance.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 32 vCPUs, 128 GiB |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 25 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 16 Gbit/s<br><br>* Maximum throughput: 4,000,000 PPS<br><br>* All instance types have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Big data applications

* Website/application servers

* Game servers

* Virtual desktop


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g4i\-flex.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>7</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.g4i\-flex.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.g4i\-flex.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.g4i\-flex.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.g4i\-flex.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>4</div><br> |


<span id="Ht3Ua8pW"></span>
## FLEX g4il\-flex

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz.<br><br>* The processor\-to\-memory ratio is 1:4.<br><br>* Max.: 32 vCPUs, 128 GiB |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 25 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 16 Gbit/s<br><br>* Maximum throughput: 4,000,000 PPS<br><br>* All instance types have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* General enterprise applications

* Big data applications

* Website/application servers

* Game servers

* Virtual desktop


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.g4il\-flex.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>7</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.g4il\-flex.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.g4il\-flex.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.g4il\-flex.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.g4il\-flex.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>4</div><br> |


<span id="37qHy1w8"></span>
## FLEX c4i\-flex

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz. This instance type is of the Self\-Developed Hardware\-Software Co\-Designed Virtualization Architecture and thereby delivers stable computing power and I/O and network performance.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br>* Max.: 32 vCPUs, 64 GiB |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 25 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 16 Gbit/s<br><br>* Maximum throughput: 4,000,000 PPS<br><br>* All instance types have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Web front\-end servers

* Data analysis and computing

* Small and medium\-sized database systems, caches, and clusters for searching

* AI inference and AI agent services


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, base/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c4i\-flex.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>7</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.c4i\-flex.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.c4i\-flex.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.c4i\-flex.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.c4i\-flex.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>4</div><br> |


<span id="hs1nZ9F2"></span>
## FLEX c4il\-flex

**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids) with a processor base frequency of 2.8 GHz and a maximum all\-core turbo frequency of 3.3 GHz.<br><br>* The processor\-to\-memory ratio is 1:2.<br><br>* Max.: 32 vCPUs, 64 GiB |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 25 volumes (including 1 system volume) can be mounted.<br><br>* Small and medium\-sized instances have burstable storage performance.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 16 Gbit/s<br><br>* Maximum throughput: 4,000,000 PPS<br><br>* All instance types have burstable network performance.<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Web front\-end servers

* Data analysis and computing

* Small and medium\-sized database systems, caches, and clusters for searching

* AI inference and AI agent services


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |Network bandwidth (outbound + inbound, basic/burst, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (basic/burst, Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.c4il\-flex.large |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2.5/max. 10</div><br> |<div style="text-align: center"><br>130</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>3</div><br> |<div style="text-align: center"><br>6</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>1.5/max. 8</div><br> |<div style="text-align: center"><br>7</div><br> |<div style="text-align: center"><br>1</div><br> |
|ecs.c4il\-flex.xlarge |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4/max. 10</div><br> |<div style="text-align: center"><br>140</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>2/max. 8</div><br> |<div style="text-align: center"><br>9</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.c4il\-flex.2xlarge |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>6/max. 10</div><br> |<div style="text-align: center"><br>160</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>15</div><br> |<div style="text-align: center"><br>5</div><br> |<div style="text-align: center"><br>3/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.c4il\-flex.4xlarge |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10/max. 15</div><br> |<div style="text-align: center"><br>300</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>5/max. 8</div><br> |<div style="text-align: center"><br>17</div><br> |<div style="text-align: center"><br>2</div><br> |
|ecs.c4il\-flex.8xlarge |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>16/max. 20</div><br> |<div style="text-align: center"><br>400</div><br> |<div style="text-align: center"><br>60</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>30</div><br> |<div style="text-align: center"><br>10</div><br> |<div style="text-align: center"><br>8/\-\-</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>4</div><br> |
