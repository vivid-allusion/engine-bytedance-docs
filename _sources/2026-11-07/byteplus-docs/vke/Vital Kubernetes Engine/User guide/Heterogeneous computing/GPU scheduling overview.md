---
title: "GPU scheduling overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/GPU-scheduling-labels"
---

NVIDIA GPU devices are widely used in scenarios such as scientific computing and graphics rendering, providing acceleration for a wide range of computing applications. VKE supports unified scheduling and O&M management of GPU resources of different models, significantly improving the resource utilization of GPU clusters. This topic describes modes of GPU scheduling in clusters.

<span id="2hCRpkPw"></span>
## Background

Driven by rapid advances in machine learning and deep learning, technology enterprises are significantly increasing investments in these fields. However, building a comprehensive AI system from scratch presents substantial barriers and complexity. For example, in deep learning scenarios, computing power is the foundation for model training and inference. To leverage massive datasets for developing higher\-performance models while accelerating end\-to\-end business processes, enterprise IT infrastructure requires robust capabilities for ‌efficiently scheduling and uniformly managing large\-scale GPU resources.

To address these requirements, VKE provides multiple solutions to GPU scheduling in clusters. These solutions are built on the cloud\-native Kubernetes architecture and integrated with mainstream cloud\-native technologies and best practices. They enable seamless deployment of model training and deep learning workloads in clusters, optimize GPU utilization‌, and drive operational cost efficiency.


|Scheduling mode |Description |Reference |
|---|---|---|
|NVIDIA GPU scheduling |The Kubernetes\-native GPU scheduling solution. In this solution, a VKE container can occupy one or more entire GPUs, with full access to all computing power and video memory of these GPUs. |[Configuring NVIDIA GPU scheduling](https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling) |
|DRA\-based GPU scheduling |A declarative resource management mechanism provided by Kubernetes. DRA is designed to address complex resource control challenges in scenarios such as fine\-grained allocation, topology\-aware scheduling, and cross\-node sharing for GPUs and other high\-performance hardware. |[Implementing NVIDIA GPU scheduling based on DRA](https://docs.byteplus.com/en/docs/vke/Implementing_NVIDIA_GPU_scheduling_based_on_DRA) |
|mGPU scheduling |A multi\-container GPU (mGPU) sharing solution leveraging kernel\-level virtualization and a proprietary scheduling framework.<br><br>While ensuring performance and fault isolation, mGPU scheduling enables multiple containers to share a single GPU. It supports flexible scheduling and strict isolation of computing power and GPU memory, reduces GPU costs, and provides efficient resource utilization for training/inference workloads. |[Configuring mGPU scheduling](https://docs.byteplus.com/en/docs/vke/Using-mGPU) |


<span id=".6IqC54K55qCH562-6K-05piO"></span>
## Scheduling labels

GPU scheduling solutions are based on node labels, which specify different scheduling modes, resource allocation policies, and other information to enable fine\-grained resource management and efficient scheduling.


|Tag |Description |
|---|---|
|vke.node.gpu.schedule=nvidia |Enables NVIDIA GPU scheduling on the GPU node. |
|vke.node.gpu.schedule=nvidia\-dra |Enables DRA\-based GPU scheduling on the GPU node. |
|vke.node.gpu.schedule=mgpu |Enables mGPU scheduling and GPU video memory isolation on the GPU node. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a GPU node does not have a label with the key <code>vke.node.gpu.schedule</code>, NVIDIA scheduling is used for the node by default.</div>


* <div data-tips="true" data-tips-type="tip">If <code>vke.node.gpu.schedule</code> is set to an invalid value, the system will determine that the node does not support GPU scheduling.</div>



<span id=".5L2_55So5qCH562-5rOo5oSP5LqL6aG5"></span>
## Switching scheduling modes

VKE allows you to switch between the GPU scheduling modes on a node by changing the value of the label for GPU scheduling. However, you need to ensure that Pods requesting GPU resources on the node have completed execution before switching.

For example, to switch from NVIDIA GPU scheduling to mGPU scheduling, change the node label from `vke.node.gpu.schedule=nvidia` to `vke.node.gpu.schedule=mgpu`. You need to make sure that all pods that have requested GPU resources (computing power or GPU video memory) on the node have finished running before the node label is switched. Otherwise, the original NVIDIA GPU scheduling task will fail.
