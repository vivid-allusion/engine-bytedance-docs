---
title: "GPU instance FAQ"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU-Compute-Service-FAQs"
---

<span id=".5L2V5pe25bqU6YCJ5oup5L2_55SoR1BV55qE5a6e5L6L77yf"></span>
## When to use a GPU instance?

GPU is a computing chip with distinct advantages. It features real\-time high speed, powerful parallel computing capability, and strong floating\-point computing capability, making it especially suitable for applications with extremely high parallelism, such as:


* Workloads that require thousands of threads.

* Graphic processing involves a large number of computational requirements with relatively small tasks. A set of operations is executed as a pipeline, where the throughput of the pipeline is more important than the latency of a single operation.


<span id=".R1BV5LiOQ1BV55qE5Yy65Yir5piv5LuA5LmI77yf"></span>
## What is the difference between a GPU and a CPU?

GPUs consist of a large number of arithmetic logic units (ALUs) that excel at large\-scale concurrent operations and relatively simple logic control units. This makes GPUs applicable to high\-throughput computing scenarios that require multithreaded parallelism.

CPUs consist of powerful arithmetic logic units (ALUs) and complex logic control units, making them applicable to serial computing scenarios that require high responsiveness and complex logic.

<span id=".5aaC5L2V5p-l55yLR1BV5a6e5L6L55qE5Lu35qC877yf"></span>
## How to view the price of a GPU instance?

On the [Price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2) page, you can see the instance price and configuration items (such as system volumes, data volumes, and EIPs). The price calculator provides reference prices. The actual costs are the fee results displayed when you order in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance).

<span id=".5aaC5L2V5p-l55yLR1BV5a6e5L6L5pCt6L2955qE5pi-5Y2h5Y-K5YW25pWw6YeP77yf"></span>
## How to view the GPU graphics cards mounted to a GPU instance and the specific number?

If you need to view which types of graphics card are mounted to the instance families, refer to [Instance types](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types). To view the number of GPU graphics cards for different instance types, refer to the "GPU memory (GB)" column in the instance specification metric list.

<span id=".5aaC5L2V5p-l55yLR1BV5pi-5Y2h55qE6K-m57uG5L-h5oGv77yf"></span>
## How to view detailed information about a GPU graphics card?


* GPU instances on Linux operating systems: After logging in to the instance, you can execute the `nvidia-smi` command to query detailed information about GPU graphics cards.

* GPU instances on Windows operating systems: After logging in to the instance, you can view detailed information about the GPU graphics cards on the Device Manager.


<span id=".6LSt5LmwR1BV5a6e5L6L5ZCO55m75b2V57O757uf5piv5LiN5piv5Y-v5Lul55u05o6l5L2_55SoR1BV6LWE5rqQ5LqG77yf"></span>
## After I log in to the system of the purchased GPU instance, can I directly use the GPU resources?

To use GPU resources in the operating system of your GPU instance, you need to install the corresponding NVIDIA driver first. For driver installation instructions, refer to [NVIDIA driver introduction](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide).

<span id=".5aaC5L2V5ZyoR1BV5a6e5L6L5ZKMRUNT5a6e5L6L5LmL6Ze05Lyg6L6T5pWw5o2u77yf"></span>
## How can data be transferred between a GPU instance and an ECS instance?

Except for GPU acceleration capabilities, all other features offered by a GPU instance are the same as those of a regular ECS instance. GPU instances and ECS instances within the same security group can communicate over the intranet. No additional configuration is required.

<span id=".RUNT5a6e5L6L5Y-v5Lul5Y-Y5pu05Li6R1BV5a6e5L6L5ZCX77yf"></span>
## Can an ECS instance be changed to a GPU instance?

No. ECS instances can not be changed to GPU instances and do not support GPU graphics cards.

<span id=".R1BV5a6e5L6L5Y-v5Lul5L-u5pS56KeE5qC85ZCX77yf"></span>
## Can I change the type of a GPU instance?

The type of certain GPU instances can be modified. For details, refer to [Instance types supporting type change](https://docs.byteplus.com/en/docs/ecs/Overview-2).
