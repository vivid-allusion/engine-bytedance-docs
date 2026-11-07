---
title: "Solution for unloading of kernel modules required by NVIDIA"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_unloaded_NVIDIA_required_kernel_modules"
---

This topic describes how to troubleshoot the issue where the kernel module required by an instance is not loaded.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).  

2. Execute the following command to check if the NVIDIA module exists.

   ```Plain Text
   lsmod | grep nvidia
   ```
   

   * If the NVIDIA module exists, the output contains `nvidia_peermem`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cbca1921ce87a3953bf276a22538cd75.png) </span>

   * If the NVIDIA module does not exist, execute the following command to reload the nvidia_peermem module.

      ```Plain Text
      modprobe nvidia_peermem
      ```
