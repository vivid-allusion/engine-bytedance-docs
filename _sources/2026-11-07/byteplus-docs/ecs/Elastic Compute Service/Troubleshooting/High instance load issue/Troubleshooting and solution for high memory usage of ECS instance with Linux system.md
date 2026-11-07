---
title: "Troubleshooting and solution for high memory usage of ECS instance with Linux system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_memory_usage_in_ECS_instances_on_Linux_systems"
---

This topic describes how to use the free command and the Atop tool to troubleshoot the issue of high memory usage (usage exceeding 80%) on a Linux instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to query the real\-time memory usage.

   ```Plain Text
   free -g
   ```
   

   **Sample output**

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48ae485751bf802a9bf4d54a5e0da8e9.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Memory usage = (<code>total</code>\-<code>free</code>) /<code>total</code>. When memory usage exceeds or is equal to 80%, the usage is considered too high.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>total</code>: Indicates memory size available to the system, that is, physical memory minus reserved memory and memory used by the kernel. The value at the intersection of this column and the <code>Mem</code> row is the total memory size.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>free</code>: Indicates memory that is completely unused by the current system. The value at the intersection of this column and the <code>Mem</code> row is the available memory size.   </div>
   

3. Use the Atop tool to view the memory usage ranking.

   1. Make sure that the Atop tool is installed on the target instance. If the Atop tool is not installed, execute the following commands to complete the installation.

      * CentOS

         ```Plain Text
         sudo yum -y install atop
         ```
         

      * Ubuntu, Debian

         ```Plain Text
         sudo apt update 
         sudo apt -y install atop
         ```
         

   2. Execute the following command to view the real\-time memory usage ranking.

      ```Plain Text
      atop -m
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53ffa0cd0925bae1ea92c894b9ad880f.png) </span>

   3. Based on `VSIZE` (virtual memory), `RSIZE` (actual memory), and `CMD` (process name), confirm whether the process with high memory usage meets expectations, and obtain the `PID` (process identifier) of the target process.

      * **If the process meets expectations**

         Optimize the program processing logic for this process to reduce memory usage. You can also upgrade your instance configuration to prevent program operations from being affected due to low instance specifications. For details, see [Changing instance types](https://docs.byteplus.com/en/docs/ecs/Overview-2).

      * **If the process fails to meet expectations**

         You can execute the following commands to manually terminate the abnormal process.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Terminating the process may cause data loss of the target process.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Terminating key operating system processes may cause the system to restart. Please proceed with caution.         </div>
         

         1. On the Atop monitoring page, press `k` key to enter process termination mode.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7b16c7dc754d4c00c7ac33eb0b28c25.png) </span>

         2. Enter the target process `PID` and press Enter to confirm.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_381ece819ab0b07ff2f74066703565cc.png) </span>

         3. Enter `9` and press the Enter key to confirm and forcibly close the process.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e608dd43fd878c4a7a497c47e0fbd7b6.png) </span>
