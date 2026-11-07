---
title: "How to view process information in a container"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/How_to_view_process_information_in_a_container"
---

NVIDIA\-SMI is a command\-line tool provided by NVIDIA for monitoring and managing systems running NVIDIA GPUs. This article describes how to use mlp\-nvidia\-smi to view process information in the container of Dev boxes/custom tasks/inference services. Currently, only regular commands are supported, and other parameters are temporarily not supported. If there is a need for continuous refresh, you can check it through nvidia\-smi first.

<span id="#1dZL7V4C"></span>
# Use posture

<span id="#V3zsYY1P"></span>
## Dev boxes

Support for executing commands directly within the container.

```Bash
mlp-nvidia-smi
```



> 1. If the execution of the command in the Dev boxes is unsuccessful, and an error such as "not found" appears, you can <mark>first </mark>**<mark>shut down and then turn it on </mark>** to upgrade the version of the Dev boxes.

> 2. Dev boxes that do not currently support mGPU use this command.


<span id="#hM56YXYT"></span>
## Custom tasks/inference services

You need to download the binary package yourself and unzip it before execution.

```Bash
wget https://ml-platform-public-examples-cn-beijing.tos-cn-beijing.volces.com/bin/mlp-nvidia-smi
chmod +x mlp-nvidia-smi
./mlp-nvidia-smi
```
