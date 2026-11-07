---
title: "GPU Rendering"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/GPU_Rendering"
---

<span id="YTALgTvw"></span>
## Overview

A GPU Rendering instance has the NVIDIA GRID driver installed and a license server configured. This instance type is applicable for graphics and image processing (3D rendering, video encoding/decoding). When you use this type of instance, you do not need to manually configure a basic environment for GPU graphics and image processing.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


<span id="Ct0CrumL"></span>
## GPU rendering type gni3cl\-vws

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently in Beta in the China (Beijing) 2, China (Shanghai) 2, and Asia Pacific (Johor) regions. To apply for a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="tip">To create an instance of this type, you can use one of the following images only:</div>


   * <div data-tips="true" data-tips-type="tip">Windows Server 2022 Datacenter Edition with GRID 16.1</div>


   * <div data-tips="true" data-tips-type="tip">Windows Server 2019 Datacenter Edition with GRID 16.1</div>


   * <div data-tips="true" data-tips-type="tip">Windows Server 2016 Datacenter Edition with GRID 16.1</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* Processor\-to\-memory ratio is 1:5.4<br><br>* Max.: 180 vCPUs, 960 GiB<br><br>* GPU graphics card: NVIDIA GPU (48 GB memory/card). You can mount a maximum of 8 graphics cards for one instance. |
|Storage |Enhanced SSD Volume and TSSD, up to 16 cloud disks can be attached (including one Root Volume) |
|Network |* Maximum network bandwidth: 160 Gbit/s<br><br>* Maximum network throughput: 14 million PPS |


**Applicable scenarios**

High\-quality graphics and image rendering, such as cloud gaming and cloud desktops.

**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |GPU |GPU memory (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interface |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volume (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.gni3cl\-vws.5xlarge |22 |120 |GPU \* 1<br><br> |48 GB \* 1 |20<br><br> |175 |75 |16 |8 |30 |5 |3 |16 |4 |
|ecs.gni3cl\-vws.11xlarge |44 |240 |GPU \* 2 |48 GB \* 2 |40 |350 |150 |32 |15 |30 |10 |6 |16 |4 |
|ecs.gni3cl\-vws.22xlarge |90 |480 |GPU \* 4 |48 GB \* 4 |80 |700 |300 |32 |15 |30 |20 |12 |16 |4 |
|ecs.gni3cl\-vws.45xlarge |180 |960 |GPU \* 8 |48 GB \* 8 |160 |1,400 |600 |32 |15 |30 |40 |24 |16 |4 |


<span id="EDy4nd9u"></span>
## GPU rendering type gni3cg\-vws

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This instance is currently in Beta in the China (Beijing) and China (Shanghai) regions. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="default">To create an instance of this type, you can use one of the following images only:</div>


   * <div data-tips="true" data-tips-type="default">Windows Server 2022 Datacenter Edition with GRID 16.1</div>


   * <div data-tips="true" data-tips-type="default">Windows Server 2019 Datacenter Edition with GRID 16.1</div>


   * <div data-tips="true" data-tips-type="default">Windows Server 2016 Datacenter Edition with GRID 16.1</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* Processor\-to\-memory ratio is 1:5.4<br><br>* Supports up to 180 vCPU, 960GiB<br><br>* GPU graphics card: NVIDIA GPU (48 GB memory/card). You can mount a maximum of 8 graphics cards for one instance. |
|Storage |* Enhanced SSD Volume and TSSD, up to 16 volumes can be mounted (including one Root Volume) |
|Network |* Maximum network bandwidth: 160 Gbit/s<br><br>* Maximum network throughput: 14 million PPS |


**Applicable scenarios**

High\-quality graphics and image rendering, such as cloud gaming and cloud desktops.

**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |GPU |GPU memory (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volume (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.gni3cg\-vws.5xlarge |22 |120 |GPU \* 1<br><br> |48 GB \* 1 |20<br><br> |175 |75 |16 |8 |30 |5 |3 |16 |4 |
|ecs.gni3cg\-vws.22xlarge |44 |240 |GPU \* 2 |48 GB \* 2 |40 |350 |150 |32 |15 |30 |10 |6 |16 |4 |
|ecs.gni3cg\-vws.45xlarge |180 |960 |GPU \* 8 |48 GB \* 8 |160 |1,400 |600 |32 |15 |30 |40 |24 |16 |4 |


&nbsp;
