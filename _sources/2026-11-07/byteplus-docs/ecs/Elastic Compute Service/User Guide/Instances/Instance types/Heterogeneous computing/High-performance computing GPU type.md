---
title: "High-performance computing GPU type"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h"
---

<span id="nenopO2D"></span>
## Overview

Based on the GPU Accelerated type, HPC\-optimized instances have added an RDMA network, which significantly enhances network performance and increases the speed\-up ratio of large\-scale clusters. This type is applicable for scenarios like high\-performance computing, artificial intelligence, and machine learning.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


* <div data-tips="true" data-tips-type="warning">For HPC\-optimized instances, you can not change the instance type.</div>



<span id="geei1gqm"></span>
## Limits


* The specifications and lifecycle of local volumes depend on the ECS instance types cannot be purchased separately. Local volumes cannot be separately mounted, unmounted, or scaled up.

* When you delete an instance, all the data stored in the local volume is automatically cleared. Please [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) before you delete the instance.

* A physical server failure or local volume damage may cause data loss. Therefore, do not store the data for long\-term use on a local volume and [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) timely.

   * We strongly recommend that you use a high\-availability architecture and deploy your services on multiple instances, or enable the cloud volume for data backup. These measures ensure high availability of your services and data reliability.

   * We strongly recommend that you store the data on a cloud volume for long\-term use.


<span id="ycaqZd1y"></span>
## HPC\-optimized hpcpni3ln

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance type is in Beta. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">You can create an instance of this type by using any of the following images:</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 22.04 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 20.04 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">Rocky Linux 8.8 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">CentOS 8.3 with GPU Driver 535.161.08 and doca 64 bit (If you need to use this image, please contact your account manager to apply)</div>


* <div data-tips="true" data-tips-type="tip">Before you use an instance of this instance type family, please make sure that the boot mode of the image is UEFI. Otherwise, the instance may fail to start. For more information, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux">How to change the image boot mode to UEFI</a>.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* Max.: 180 vCPUs, 1960 GiB<br><br>* GPU graphics card: NVIDIA GPU (96 GB memory/card), supporting NVSwitch. You can mount a maximum of 8 graphics cards for one instance. |
|Storage |* ESSD volume.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |* Maximum network bandwidth: 320 Gbit/s.<br><br>* Maximum throughput: 32,000,000 PPS.<br><br>* 1600 Gbps bandwidth is provided for inter\-instance interconnection. |


**Applicable scenarios**


* Training of small and medium\-sized models and FP8 precision large model training, such as traditional CV models, autonomous driving, advertisement recommendation, and LLM.

* Large model inference. Distributed inference is supported. such as generative AI, intelligent Q&A, and speech generation.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance types |vCPU |Memory (GiB) |Local storage (GB) |GPU |GPU memory (GB) |RDMA network (Gbit/s) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.hpcpni3ln.45xlarge |180 |1,960 |3,840 \* 4 |GPU \* 8 |96 \* 8 |400 \* 4 |320 |3,200 |400 |31 |9 |30 |40 |24 |31 |4 |


<span id="WGZcMGnX"></span>
## HPC\-optimized ebmhpcpni3ln

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This instance is currently in Beta in the China (Beijing) region. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="default">You can create an instance of this type by using any of the following images:</div>


   * <div data-tips="true" data-tips-type="default">veLinux 1.0 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="default">Ubuntu 22.04 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="default">Ubuntu 20.04 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="default">Rocky Linux 8.8 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="default">CentOS 8.3 with GPU Driver 535.161.08 and doca 64 bit (If you need to use this image, please contact your account manager to apply)</div>


* <div data-tips="true" data-tips-type="default">Before you use an instance of this instance type family, please make sure that the boot mode of the image is UEFI. Otherwise, the instance may fail to start. For more information, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux">How to change the image boot mode to UEFI</a>.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* Max.: 192 vCPUs, 2048 GiB<br><br>* GPU graphics card: NVIDIA GPU (96 GB memory/card), supporting NVSwitch. You can mount a maximum of 8 graphics cards for one instance. |
|Storage |* ESSD volume.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |* Maximum network bandwidth: 96 Gbit/s.<br><br>* Maximum throughput: 36,000,000 PPS.<br><br>* 3200 Gbps bandwidth is supported for inter\-instance interconnection. |


**Applicable scenarios**

AI training, Large Language Model (LLM) training and inference, such as generative AI, intelligent Q&A, video and image generation, code generation, image classification, visual perception, and advertisement recommendation.

**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance types |vCPU |Memory (GiB) |Local storage (GB) |GPU |GPU memory (GB) |RDMA network (Gbit/s) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmhpcpni3l.48xlarge |192 |2,048 |3,840 \* 4 |GPU \* 8 |96 \* 8 |4\*400 |96 |3,600 |600 |32 |16 |30 |40 |32 |16 |8 |


<span id="86HwHX7e"></span>
## HPC\-optimized hpcpni3le

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This instance is currently in Beta in the China (Beijing) and China (Shanghai) regions. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="default">You can create an instance of this type by using any of the following images:</div>


   * <div data-tips="true" data-tips-type="default">veLinux 1.0 with GPU Driver 535.216.03 and doca 2.9.1 64 bit</div>


   * <div data-tips="true" data-tips-type="default">Ubuntu 20.04 with GPU Driver 535.230.02 and doca 2.9.1 64 bit</div>


   * <div data-tips="true" data-tips-type="default">Ubuntu 22.04 with GPU Driver 535.230.02 and doca 2.9.1 64 bit</div>


   * <div data-tips="true" data-tips-type="default">RockyLinux 8.8 with GPU Driver 535.230.02 and doca 2.9.1 64 bit</div>


* <div data-tips="true" data-tips-type="default">Before you use an instance of this instance type family, please make sure that the boot mode of the image is UEFI. Otherwise, the instance may fail to start. For more information, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux">How to change the image boot mode to UEFI</a>.</div>



**Features**


|**Type** |**Performance** |
|---|---|
|Computing |Processor: the 6th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Granite Rapids, GNR) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.4 GHz. |
||Max.: 240 vCPUs, 1954 GiB |
||GPU graphics card: NVIDIA GPU (141 GB memory/card). 900GB/s NVLink is provided for communication between GPUs. You can mount a maximum of 8 graphics cards for one instance. |
|Storage |You can use ESSD volumes. A maximum of 64 volumes (including 1 system volume) can be mounted. |
||High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |Max network bandwidth: 320 Gbit/s |
||Maximum throughput: 36,000,000 PPS |
||1600 Gbps RDMA bandwidth is provided for inter\-instance interconnection. |


**Applicable scenarios**


* Training of models, such as traditional CV models, autonomous driving, advertisement recommendation, and LLM.

* Large model inference, such as DeepSeek\-R1 128K inference, generative AI, intelligent Q&A, and voice generation.


**Instance types and metrics**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|**Instance types** |**vCPU** |**Memory (GiB)**  |**Local storage (GB)**  |**GPU** |**GPU memory (GB)**  |**RDMA network (Gbit/s)**  |**Maximum network bandwidth (outbound + inbound, Gbit/s)**  |Maximum queues per network interface |**Elastic network interfaces (including 1 primary network interface)**  |**Private IP addresses for one network interface** |**Volume IOPS (unit: 10,000)**  |**Volume bandwidth (Gbit/s)**  |**Volumes (including 1 system volume)**  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.hpcpni3le.60xlarge |240 |1,954 |3,840 \* 4 |GPU\-H3e \* 8 |141 GB \* 8 |400 \* 4 |320 |31 |9 |30 |40 |24 |64 |


<span id="dQ90MFyH"></span>
## HPC\-optimized ebmhpcpni3l

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance type is in Beta. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">You can create an instance of this type by using any of the following images:</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 22.04 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 20.04 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">Rocky Linux 8.8 with GPU Driver 535.161.08 and doca 64 bit</div>


   * <div data-tips="true" data-tips-type="tip">CentOS 8.3 with GPU Driver 535.161.08 and doca 64 bit (If you need to use this image, please contact your account manager to apply)</div>


* <div data-tips="true" data-tips-type="tip">Before you use an instance of this instance type family, please make sure that the boot mode of the image is UEFI. Otherwise, the instance may fail to start. For more information, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux">How to change the image boot mode to UEFI</a>.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* Max.: 192 vCPUs, 2048 GiB<br><br>* GPU graphics card: NVIDIA GPU (96 GB memory/card), supporting NVSwitch. You can mount a maximum of 8 graphics cards for one instance. |
|Storage |* ESSD volume.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |* Maximum network bandwidth: 96 Gbit/s.<br><br>* Maximum throughput: 36,000,000 PPS.<br><br>* 3200 Gbps bandwidth is supported for inter\-instance interconnection. |


**Applicable scenarios**

AI training, Large Language Model (LLM) training and inference, such as generative AI, intelligent Q&A, video and image generation, code generation, image classification, visual perception, and advertisement recommendation.

**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance types |vCPU |Memory (GiB) |Local storage (GB) |GPU |GPU memory (GB) |RDMA network (Gbit/s) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmhpcpni3l.48xlarge |192 |2,048 |3,840 \* 4 |GPU \* 8 |96 \* 8 |400 \* 8 |96 |3,600 |600 |32 |16 |30 |40 |32 |16 |8 |


<span id="8606QuMw"></span>
## HPC\-optimized hpcpni3h

<div data-tips="true" data-tips-type="tip">Description</div>



* <div data-tips="true" data-tips-type="tip">This instance type is in Beta. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">To create an instance of this type, you can use one of the following images only:</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0</div>


   * <div data-tips="true" data-tips-type="tip">Debian 12</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 22.04</div>



**Prerequisites**

InfiniBand is a network communication protocol specifically designed for remote direct memory access (RDMA), featuring high throughput and low latency.

> InfiniBand is a network communication protocol specifically designed for remote direct memory access (RDMA), featuring high throughput and low latency.


> * How to create an InfiniBand cluster?

>    1. Log in to [the HPC Cluster console](https://console.byteplus.com/ecs/hpcCluster).

>    2. Click "Create HPC cluster", configure the region, availability zone, and name for the HPC cluster, and select InfiniBand as the cluster attribute.

>    3. Click Create. The instance is created.

> * How to select cluster attribute?

   > Currently, only hpcpni3h instances require an InfiniBand cluster.


**Features**


|Type |Performance |
|---|---|
|Computing |Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz. |
||Max.: 168 vCPUs, 1960 GiB |
||GPU graphics card: NVIDIA GPU (80 GB memory/card). You can mount a maximum of 8 graphics cards for one instance. |
|Storage |You can use ESSD volumes. A maximum of 31 volumes (including 1 system volume) can be mounted. |
||High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |Max network bandwidth: 210 Gbit/s |
||Maximum throughput: 20,000,000 PPS |
||3200 Gbps bandwidth is provided for inter\-instance interconnection. |


**Applicable scenarios**


* Super\-large\-scale AI training, such as Large Language Model training and generative AI like intelligent Q&A, video and image generation, and code generation.

* Applications with high\-performance computing, such as drug research and development, gene sequencing, seismic analysis, and quantum simulation of materials.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance types |vCPU |Memory (GiB) |Local storage (GB) |GPU |GPU memory (GB) |RDMA network (Gbit/s) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.hpcpni3h.42xlarge |168 |1,960 |3,840 \* 8 |GPU \* 8 |80 GB \* 8 |400 \* 8 |210 |2,000 |400 |64 |16 |30 |40 |24 |31 |4 |


<span id="BnkhBkbE"></span>
##
