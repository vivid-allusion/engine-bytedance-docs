---
title: "GPU Accelerated"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU-Accelerated-gni3cl"
---

<span id="Qw0L8l0P"></span>
## Overview

Based on multiple types of NVIDIA Tesla GPUs, GPU Accelerated instances offer high cost effectiveness in different inference and molecular computing scenarios. This instance family is applicable for deep learning and AI inference training, such as AI algorithm training for image processing and speech recognition. By referring to this topic, you can select an instance type that meets your business needs. This helps you ensure that the selected type meets the minimum CPU and memory requirements for your business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For information about instance types, estimated instance fees, instance type changes, and instance naming rules, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>


<span id="fxeOxsIS"></span>
## GPU Accelerated pni3l

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This instance is currently in Beta in the China (Shanghai), China (Beijing), and Asia Pacific (Johor) regions. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="default">You can change instance type within this instance family.</div>


* <div data-tips="true" data-tips-type="default">The following images are supported for creating this instance:</div>


   * <div data-tips="true" data-tips-type="default">veLinux 1.0</div>


   * <div data-tips="true" data-tips-type="default">Ubuntu 22.04</div>


   * <div data-tips="true" data-tips-type="default">Ubuntu 20.04</div>


   * <div data-tips="true" data-tips-type="default">Rocky Linux 8.8</div>


   * <div data-tips="true" data-tips-type="default">CentOS 8.3 (If you need to use this image, please contact your account manager to apply)</div>


* <div data-tips="true" data-tips-type="default">Before you use an instance of this instance type family, please make sure that the boot mode of the image is UEFI. Otherwise, the instance may fail to start. For more information, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux">How to change the image boot mode to UEFI</a>.</div>


* <div data-tips="true" data-tips-type="default">In this instance type family, instances equipped with two or more GPU cards are configured with an NVLink device by default. If the <code>nvidia-fabricmanager.service</code> status is <code>failed</code>, this is normal and does not affect business operations.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz. |
||Max.: 176 vCPUs, 1,956 GiB |
||GPU graphics card: NVIDIA GPU (96 GB memory/card), for which the maximum memory bandwidth is 4 TB/s. A 900 GB/s NVLINK between GPU cards is available. You can mount a maximum of 8 graphics cards for one instance. |
|Storage |You can use ESSD volumes. A maximum of 32 volumes (including 1 system volume) can be mounted. |
||The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |Max network bandwidth: 320 Gbit/s |
||Maximum throughput: 32,000,000 PPS |
||The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**

Large model inference and small\-sized model training scenarios:


* AI large model inference: The new 96 GB memory accelerates ultra\-large model inference tasks and supports FP8 floating point number format. This instance type supports inference of models with tens of billions to hundreds of billions of parameters, and leads in multi\-card parallel inference performance.

* Small model training: training in traditional AI scenarios such as image classification, image recognition, advertisement recommendation, and autonomous driving scenarios.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |GPU |GPU memory (GB) |Local storage (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interfaces (including 1 primary network interface) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.pni3l.5xlarge |22 |244 |NVIDIA GPU \* 1 |96 GB \* 1 |\- |40 |400 |50 |22 |4 |30 |5 |3 |4 |4 |
|ecs.pni3l.11xlarge |44 |488 |NVIDIA H20 \* 2 |96GB \* 2 |\- |80 |800 |100 |31 |8 |30 |10 |6 |8 |4 |
|ecs.pni3l.22xlarge |88 |976 |NVIDIA GPU \* 4 |96 GB \* 4 |\- |160 |1,600 |200 |31 |9 |30 |20 |12 |16 |4 |
|ecs.pni3l.44xlarge |176 |1,956 |NVIDIA GPU \* 8 |96 GB \* 8 |\- |320 |3,200 |400 |31 |9 |30 |40 |24 |32 |4 |
|ecs.pni3ld.44xlarge |176 |1,956 |NVIDIA GPU \* 8 |96 GB \* 8 |3,840 \* 4 |320 |3,200 |400 |31 |9 |30 |40 |24 |31 |4 |


<span id="AmEoLCBb"></span>
## GPU Accelerated gni3c

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently in Beta in the China (Beijing) and China (Shanghai) regions. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">You can change instance type within this instance family.</div>


* <div data-tips="true" data-tips-type="tip">You can use the following images:</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 22.04</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 20.04</div>


   * <div data-tips="true" data-tips-type="tip">Debian 10</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0 CentOS Compatible</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:5.3.<br><br>* Max.: 192 vCPUs, 1,024 GiB.<br><br>* GPU graphics card: NVIDIA GPU (48 GB memory/card). You can mount a maximum of 8 graphics cards for one instance. |
|Storage |You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted. |
|Network |* Maximum network bandwidth: 96 Gbit/s.<br><br>* Maximum throughput: 36,000,000 PPS. |


**Applicable scenarios**


* Large model inference. Distributed inference is supported.

* AI inference in large\-scale deployment, such as image recognition, natural language processing, and speech recognition.

* Training for small and medium\-sized models.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |GPU |GPU memory (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interface (EniQuantity) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.gni3c.6xlarge |24 |128 |NVIDIA GPU \* 1 |48 GB \* 1 |12 |450 |75 |8 |4 |30 |8 |4 |16 |4 |
|ecs.gni3c.12xlarge |48 |256 |NVIDIA GPU \* 2 |48 GB \* 2 |24 |900 |150 |16 |8 |30 |15 |8 |16 |4 |
|ecs.gni3c.24xlarge |96 |512 |NVIDIA GPU \* 4 |48 GB \* 4 |48 |1,800 |300 |32 |16 |30 |30 |16 |16 |4 |
|ecs.gni3c.48xlarge |192 |1,024 |NVIDIA GPU \* 8 |48 GB \* 8 |96 |3,600 |600 |32 |16 |30 |60 |32 |16 |8 |


<span id="A4qG3ldp"></span>
## GPU Accelerated ebmgni3c

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently in Beta in the China (Beijing) and China (Shanghai) regions. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">The instance type can not be changed.</div>


* <div data-tips="true" data-tips-type="tip">You can use the following images:</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 22.04</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 20.04</div>


   * <div data-tips="true" data-tips-type="tip">Ubuntu 18.04</div>


   * <div data-tips="true" data-tips-type="tip">Debian 10</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0</div>


   * <div data-tips="true" data-tips-type="tip">veLinux 1.0 CentOS Compatible</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:5.3.<br><br>* Max.: 192 vCPUs, 1,024 GiB.<br><br>* GPU graphics card: NVIDIA GPU (48 GB memory/card). You can mount a maximum of 8 graphics cards for one instance. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* High\-performance (high IOPS, high throughput, low latency) local SSDs are configured. |
|Network |* Maximum network bandwidth: 96 Gbit/s.<br><br>* Maximum throughput: 36,000,000 PPS. |


**Applicable scenarios**


* Large model inference. Distributed inference is supported.

* AI inference in large\-scale deployment, such as image recognition, natural language processing, and speech recognition.

* Training for small and medium\-sized models.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |GPU |GPU memory (GB) |Local storage (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interface (EniQuantity) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.ebmgni3c.48xlarge |192 |1,024 |GPU \* 8 |48 \* 8 |1,920 \* 1 |96 |3,600 |600 |32 |16 |30 |70 |64 |16 |4 |


<span id="SBCQw2X5"></span>
## GPU Accelerated gni3cl

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This instance is currently in Beta in the China (Beijing), China (Shanghai), and Asia Pacific (Johor) regions. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">You can change instance type within this instance family.</div>



**Features**


|Type |Performance |
|---|---|
|Computing |* Processor: the 4th\-generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processor (Sapphire Rapids) with a processor base frequency of 2.6 GHz and an all\-core turbo frequency of 3.1 GHz.<br><br>* The processor\-to\-memory ratio is 1:5.3.<br><br>* Max.: 180 vCPUs, 960 GiB.<br><br>* GPU graphics card: NVIDIA GPU (48 GB memory/card). You can mount a maximum of 8 graphics cards for one instance. |
|Storage |* You can use ESSD volumes or TSSD volumes. A maximum of 16 volumes (including 1 system volume) can be mounted.<br><br>* The storage I/O performance depends on compute specification. A higher specification offers better performance. |
|Network |* Maximum network bandwidth: 160 Gbit/s.<br><br>* Maximum throughput: 14,000,000 PPS<br><br>* The network performance depends on compute specification. A higher specification offers better performance. |


**Applicable scenarios**


* Large model inference. Distributed inference is supported.

* AI inference in large\-scale deployment, such as image recognition, natural language processing, and speech recognition.

* Training for small and medium\-sized models.


**Instance types and metrics**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum throughput (PPS) varies significantly in different business scenarios. Therefore, we recommend that you conduct a business stress test to learn the instance performance. After that, you can select an appropriate instance type.</div>



|Instance specification |vCPU |Memory (GiB) |GPU |GPU memory (GB) |Local storage (GB) |Maximum network bandwidth (outbound + inbound, Gbit/s) |Maximum throughput (outbound + inbound) (10,000 PPS) |Connections (10,000) |Maximum queues per network interface |Elastic network interface (EniQuantity) |Private IP addresses for one network interface |Volume IOPS (unit: 10,000) |Volume bandwidth (Gbit/s) |Volumes (including 1 system volume) |Maximum queues per volume |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.gni3cl.5xlarge |22 |120 |GPU \* 1 |48 \* 1 |\- |20 |175 |75 |16 |4 |30 |5 |3 |16 |4 |
|ecs.gni3cl.11xlarge |44 |240 |GPU \* 2 |48 \* 2 |\- |40 |350 |150 |32 |8 |30 |10 |6 |16 |4 |
|ecs.gni3cl.22xlarge |90 |480 |GPU \* 4 |48 \* 4 |\- |80 |700 |300 |32 |8 |30 |20 |12 |16 |4 |
|ecs.gni3cl.45xlarge |180 |960 |GPU \* 8 |48 \* 8 |1,920 \* 2 |160 |1,400 |600 |32 |8 |30 |40 |24 |16 |4 |


&nbsp;
