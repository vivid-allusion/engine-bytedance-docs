---
title: "Solution for link exceptions in NVML link libraries"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_NVML_link_library_link_exception"
---

This topic describes how to troubleshoot link exceptions in the NVML link library.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance). 

2. Execute the following command to check whether a link library exists in the instance.

   ```Plain Text
   ldconfig -p | grep nvidia-ml
   ```
   

   * The following is a sample output when a link library exists:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6d25e84df0cb0ba6f7b61799604e2c9.png) </span>

   * When the link library does not exist, execute the following command to check whether the driver is installed on the instance or whether the driver is installed incorrectly.

      ```Plain Text
      nvidia-smi
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If "command not found" is displayed, the driver is not installed.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If an error message is displayed, such as "NVIDIA\-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.", the driver cannot work correctly due to an exception.      </div>
      

3. If no driver is installed or the driver is installed incorrectly, [please install a GPU driver](https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers).
