---
title: "How do I handle RDMA network connectivity issues for nodes with multiple A100/A800 GPUs?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-can-I-handle-RDMA-network-connectivity-exceptions-for-the-multi-card-GPU-A100_A800-instance-type"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

For nodes that use multiple A100/A800 GPUs, the GPUs fail to connect to each other.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The NVIDIA\-Fabric Manager service ensures that multiple GPUs that support NVSwitch (such as A100 and A800) are interconnected through NVSwitch. This guarantees normal network connectivity. If the NVIDIA\-Fabric Manager service is not enabled on the node, the connection among multiple GPUs that support NVSwitch cannot be established.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

In scenarios such as creating a node pool or adding new nodes, the NVIDIA\-Fabric Manager package can be built into a custom image. In scenarios where nodes already exist, you can directly install NVIDIA\-Fabric Manager to resolve this issue.

**Solution 1** for scenarios where new nodes are added


1. Package a custom image. For packaging methods, see [Overview of operating system (OS) images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

2. Select the packaged custom image to create a node pool or scale out nodes.


**Solution 2** for scenarios where nodes already exist

Install and start the NVIDIA\-Fabric Manager package that corresponds to the GPU driver version for the GPU node. For details, see [Installing the NVIDIA-Fabric Manager package](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager).
