---
title: "Troubleshooting and solution for high disk BPS/IOPS load of ECS instance with Linux system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_BPS_or_IOPS_load_issues_on_ECS_instance_disks_of_Linux_systems"
---

This topic describes how to use the iostat and Atop tools to troubleshoot issues caused by high disk BPS (bytes transferred per second) and IOPS (input/output operations per second), such as system lag, disk I/O throttling, and increased disk I/O latency that degrade the performance of your business processes.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following commands to install the iostat tool.

   * CentOS

      ```Plain Text
      sudo yum install sysstat -y
      ```
      

   * Ubuntu, Debian

      ```Plain Text
      sudo apt-get install sysstat -y
      ```
      

3. Execute the following command to query disk usage via the iostat tool.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Functions of command arguments are described below. Adjust based on your needs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>-d</code>: Displays disk usage.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>-k</code>: Displays data in KB units.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>3</code>Statistical time interval. Adjust based on your needs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>5</code>Number of statistical times. Adjust based on your needs.   </div>
   

   ```Plain Text
   iostat -d -k 3 5
   ```
   

   Sample output

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e821f7c9537d2844a9e627d5900f69f0.png) </span>

   Parameter description

   
   |Parameter​ |Description |
   |---|---|
   |Device |Disk name. |
   |tps |Number of I/O requests sent per second. |
   |Blk_read/s |Number of blocks read per second. |
   |Blk_wrtn/s |Number of blocks written per second. |
   |Blk_read |Total number of blocks read. |
   |Blk_wrtn |Total number of blocks written. |
   

4. Use the Atop tool to view the disk usage ranking.

   1. Make sure that the Atop tool is installed on the target instance. If it is not installed, execute the following commands to complete the operation.

      * CentOS

         ```Plain Text
         sudo yum -y install atop
         ```
         

      * Ubuntu, Debian

         ```Plain Text
         sudo apt update 
         sudo apt -y install atop
         ```
         

   2. Execute the following command to view the real\-time disk usage ranking.

      ```Plain Text
      atop -d
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8fd41b51dd7524d06677260f28108b1.png) </span>

   3. Based on `RDDSK` (amount of data read per second), `WRDSK` (amount of data written per second), `WCANCAL` (number of disk activities per second), `DSK` (disk utilization), and `CMD` (process name), confirm whether the process with high disk usage meets expectations, and obtain the `PID` (process identifier) of the target process.

      * **If the process meets expectations**

         Optimize the program processing logic for this process to reduce disk usage. You may also upgrade your instance configuration, scale up the EBS Volume, or Modify the EBS Volume specification to ensure the program is not constrained by EBS Volume performance, preventing normal operation. For operation details, you can view [Modify the instance type](https://docs.byteplus.com/en/docs/ecs/Overview-2), [Scaling up the EBS Volume](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux), [Modify the EBS Volume specification](https://docs.byteplus.com/en/docs/ecs/Modify-volume-type).

      * **If the process fails to meet expectations**

         You can execute the following commands to manually terminate the abnormal process.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Terminating the process may cause data loss of the target process.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Terminating key operating system processes may cause the system to restart. Please proceed with caution.         </div>
         

         1. On the Atop monitoring page, press the `k` key to enter process termination mode.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63f2c60a00b605f08c4dd12b4886eb10.png) </span>

         2. Enter the target process `PID`, and press the Enter key to confirm.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb9f2817d628e08a930f1cf03dc86f24.png) </span>

         3. Enter `9` and press the Enter key to confirm and forcibly close the process.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_554cdb1d92702b0a546d7c2a75c6d4f7.png) </span>
