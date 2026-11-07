---
title: "Solution for fixing 3rd-generation instances that fail to start due to Virtio driver issues"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_fixing_third-generation_instances_that_cannot_start_due_to_Virtio_driver_issues"
---

This topic describes how to troubleshoot and resolve the issue where a 3rd\-generation instance fails to start because the Virtio driver is not installed or its version does not meet the requirements.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you install the driver, install kernel\-headers and kernel\-devel, and make sure that they match the kernel version. Otherwise, the driver installation may fail. If the kernel is upgraded, restart the instance before you install the driver. You can also compile [the driver source code](https://github.com/volcengine/dkms-virtio1.1)   .

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Use a script to detect whether the Virtio driver version of the virtual machine meets the requirements.

   1. Execute the following command to download the detection script file via the public network.

      ```Plain Text
      wget -O virtio_tool https://virtio11-drivers.tos-cn-beijing.volces.com/virtio_tool_1.1.2
      ```
      

   2. Execute the following command to grant the execute permission on the script file.

      ```Plain Text
      chmod +x ./virtio_tool
      ```
      

   3. In the directory where the script file is stored, execute the following command to check whether the Virtio driver version meets the requirements.

      ```Plain Text
      ./virtio_tool -check
      ```
      

      * If the following output is displayed, the required Virtio driver is installed on your virtual machine. Skip the next step.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8cb5511e58012ab9b54a77a6774c33cf.png) </span>

      * If the following output is displayed, the required Virtio driver is not installed on your virtual machine. Proceed to the next step.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d70a837648f0df94567f92cacbb1cef0.png) </span>

2. Install the Virtio1.1 driver. For details, refer to [Installing the Virtio1.1 driver using virtio_tool](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo).
