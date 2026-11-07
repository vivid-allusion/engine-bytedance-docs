---
title: "mGPU overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/mGPU-overview"
---

Vital Kubernetes Engine (VKE) provides the multi\-container GPU (mGPU) solution to enable containers to share a GPU.

<span id="qrZD4UFS"></span>
## Introduction to mGPU

mGPU is a container\-sharing GPU solution based on kernel virtualization and isolation of GPUs and a self\-developed scheduling framework. While ensuring performance and fault isolation, mGPU enables multiple containers to share a single GPU, flexibly schedules and strictly isolates computing power and GPU memory, reduces GPU usage costs, and enables you to efficiently use GPU hardware resources for training and inference.

<span id="vIY9rUKT"></span>
## Benefits


* Strict isolation

   mGPU achieves strict isolation of GPU memory and computing power, fine\-grained configuration of computing power amount and proportion, and highest GPU resource utilization.

* High compatibility

   mGPU is compatible with mainstream architectures such as Volta, Turing, and Ampere, and is adapted to the standard open source Kubernetes.

* Multi\-dimensional monitoring

   mGPU provides built\-in monitoring clients, which provide multi\-dimensional metrics to quickly achieve visual observation.

* High performance

   mGPU can dynamically adjust timeslices, which improves the throughput of business processes and then achieves high business performance.


<span id="k7SwEBzC"></span>
## Solution architecture

The following figure shows the architecture of the mGPU solution.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fc584bea10e5073a08934efd0b362c7.png) </span>

In the mGPU solution, GPU devices and GPU drivers form the underlying GPU device, which achieves strict isolation of GPU memory and computing power and achieves fault isolation combined with the kernel\-mode driver module of mGPU. mGPU Container Runtime provides a container\-runtime configuration API. VKE provides you with configuration entries based on the Device Plugin and Scheduler Plugin capabilities.

<span id="dcvbuT3V"></span>
## Application scenario

mGPU enables multiple containers to share a GPU. It is suitable for scenarios where a single business application does not need to use the entire GPU, which has strong computing power. mGPU enables multiple applications to share a GPU and isolates the computing power of applications, which improves GPU utilization, reduces costs, and ensures business secure isolation.
