---
title: "Troubleshooting and solution for high CPU usage or load of ECS instance with Linux system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_CPU_usage_or_CPU_load_issues_on_the__instance"
---

This topic describes how to use the Atop tool to troubleshoot high CPU usage or CPU load on a Linux instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Make sure that the Atop tool is installed on the target instance. If the Atop tool is not installed, execute the following commands to complete the installation.

   * CentOS

      ```Plain Text
      yum -y install atop
      ```
      

   * Ubuntu, Debian

      ```Plain Text
      apt -y install atop
      ```
      

3. Use the Atop tool to identify processes affecting CPU usage or CPU load.

   1. Execute the following command in the target instance to view the real\-time CPU usage ranking.

      ```Plain Text
      atop
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb5cf8d05e6b163a1de60bdbaaaaec5d.png) </span>

   2. View historical system usage.

      1. Execute the following command to view the system usage at the target time point.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">In this example, the time point of March 5, 2024, is used as the time when the problem occurred. Replace it with the actual time point.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Make sure that the specified abnormal time point is after you installed the Atop tool.         </div>
         

         ```Plain Text
         atop -r /var/log/atop/atop_20240305
         ```
         

      2. Press `t` key to adjust and view later times. Press `shift` + `t` key to adjust and view earlier times.

      3. View the CPU usage at the abnormal time point.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7033c592d8377bc3ea04d2989360909a.png) </span>

   3. Identify the PID of the process that may cause issues based on real\-time and historical usage.

   4. Based on your current business, confirm whether the running status of the process that caused issues meets expectations.

      * **If the process meets expectations**

         Optimize the program processing logic for this process to reduce CPU usage. You can also upgrade your instance configuration to prevent program operations from being affected due to low instance specifications. For details, see [Changing instance types](https://docs.byteplus.com/en/docs/ecs/Overview-2).

      * **If the process fails to meet expectations**

         You can execute the following commands to manually terminate the abnormal process.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Terminating the process may cause data loss of the target process.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Terminating key operating system processes may cause the system to restart. Please proceed with caution.         </div>
         

         1. On the Atop monitoring page, press the `k` key to enter process termination mode.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7b16c7dc754d4c00c7ac33eb0b28c25.png) </span>

         2. Enter the target process `PID`, and press the Enter key to confirm.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_381ece819ab0b07ff2f74066703565cc.png) </span>

         3. Press the `9` key and press Enter to confirm and forcibly close the process.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0ec8b1054bdad3a735d95fefb2f18a2.png) </span>
