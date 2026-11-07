---
title: "Modifying timeout parameters for NVMe disks in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/timeout-argument-for-NVMe-drives"
---

This topic describes how to configure the timeout periods for NVMe disks on a Linux instance mounted with NVMe disks.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This practice is only applicable to instances running the Linux operating system and using NVMe disks. For details of instance types, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types</a>. </div>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

For instances that use Nonvolatile Memory Express (NVMe) disks, you can configure the following parameters​ to set the timeout periods for NVMe disks to process I/O commands or Admin commands.

<span id="nvme_core.io_timeout"></span>
### nvme_core.io_timeout

This parameter specifies the timeout period for I/O commands of a device (commands for data transmission operations, such as reading from or writing to a disk). The unit is seconds, with a default value of 30 seconds.

When the driver detects a timeout of an I/O operation, it will wake up the timeout handler (a mechanism or module for handling timeout errors). Based on the error handling policy, the handler will decide to retry the I/O operation, return failure information, or perform device recovery.

<span id="nvme_core.admin_timeout"></span>
### nvme_core.admin_timeout

This parameter specifies the timeout period for Admin commands of a device (commands for a host to manage and control SSD operations, such as creating I/O submission queues). The unit is seconds, with a default value of 60 seconds.

When the driver detects a timeout of an Admin operation, it will wake up the timeout handler (a mechanism or module for handling timeout errors). Based on the error handling policy, the handler will decide to retry the I/O operation, return failure information, or perform device recovery.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

<span id=".5o-Q5Y2HSS9P5ZON5bqU5pe26Ze0"></span>
### Accelerate I/O response

For applications requiring fast responses, you can appropriately **reduce** the timeout period to improve the response speed of I/O operations.

<span id=".5o-Q5Y2H6LWE5rqQ5Yip55So546H"></span>
### Improve resource utilization

If resources are tight and you need to improve resource utilization, you can appropriately **reduce** the timeout period. This allows faster release of resources occupied by timed\-out I/O operations. In turn, other tasks or I/O operations can obtain resources promptly, thereby improving the overall efficiency of the system.

<span id=".5aKe5YqgSS9P5ZCe5ZCQ6YeP"></span>
### Increase I/O throughput

To increase the I/O throughput of NVMe disks, you can appropriately **extend** the timeout period. This allows more I/O operations to be performed simultaneously, thereby making full use of the parallel processing capability of NVMe devices and improving data transmission speed and overall performance.

<span id=".5aKe5Yqg5Y-v6Z2g5oCn5ZKM5pWw5o2u5a6M5pW05oCn"></span>
### Increase reliability and data integrity

For scenarios requiring high reliability and data integrity, you can appropriately **extend** the timeout period to ensure that I/O operations have sufficient time to complete, thereby reducing data loss or errors caused by timeouts.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The principle of the timeout parameter is to increase delay tolerance, which means delaying the sending of abort commands. If you specify an excessively long timeout period and the disk remains unresponsive afterward, the I/O operation of the NVMe disk will not be aborted for a long time, nor will retries be performed. This will cause the application to get stuck in this I/O operation and run abnormally.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u6LaF5pe25Y-C5pWw"></span>
### Step 1: Configure the timeout parameters


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check whether the timeout parameters are configured in the grub file.

   ```Plain Text
   grep -r "timeout" /etc/default/grub
   ```
   

   * If no value is displayed in the output, execute the following command to add timeout parameters to the grub file.

      ```Plain Text
      sed -i "/GRUB_CMDLINE_LINUX=/s/\"$/ nvme_core.io_timeout=4294967295 nvme_core.admin_timeout=4294967295 \"/" /etc/default/grub
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>4294967295</code> in the command with the actual timeout periods based on your needs. The unit is seconds.      </div>
      

   * If the following output is displayed, execute the following command to modify the timeout parameter values.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3153e9c9cf4311d5c06c74571c9dcad.png) </span>

      1. Execute the following command to open the grub file.

         ```Plain Text
         vim /etc/default/grub
         ```
         

      2. Press the `i` key to enter edit mode and modify the values of the `nvme_core.io_timeout` and `nvme_core.admin_timeout` parameters.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Modify the timeout periods based on your needs. The unit is seconds.         </div>
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_18d6ee65287a709f2239fccfaedbfb6c.png) </span>

      3. Press `Esc`, enter `:wq`, and then press Enter to save and close the file.

3. Depending on the operating system and boot mode type, execute the following commands to apply the timeout parameter configuration.

   * CentOS

      * Legacy boot mode

         ```Plain Text
         grub2-mkconfig -o /boot/grub2/grub.cfg
         ```
         

      * UEFI boot mode

         ```Plain Text
         grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
         ```
         

   * Debian

      * Legacy boot mode

         ```Plain Text
         grub-mkconfig -o /boot/grub2/grub.cfg
         ```
         

      * UEFI boot mode

         ```Plain Text
         grub-mkconfig -o /boot/efi/EFI/debian/grub.cfg
         ```
         

   * Ubuntu

      * Legacy boot mode

         ```Plain Text
         grub-mkconfig -o /boot/grub2/grub.cfg
         ```
         

      * UEFI boot mode

         ```Plain Text
         grub-mkconfig -o /boot/efi/EFI/ubuntu/grub.cfg
         ```
         

4. Execute the following command to restart the instance for the configuration to take effect.

   ```Plain Text
   reboot
   ```
   


<span id=".5q2l6aqk5LqM77ya6aqM6K-B6YWN572u"></span>
### Step 2: Verify configuration


* Execute the following command to view startup parameter information.

   ```Plain Text
   cat /proc/cmdline | grep "timeout"
   ```
   

   As shown in the following figure, the timeout period for both instance I/O operations and Admin operations is `4294967295` seconds.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15c406f02daa9f768c9a042011570e58.png) </span>

* Execute the following command to view parameter information of the NVMe module.

   ```Plain Text
   cat /sys/module/nvme_core/parameters/io_timeout
   cat /sys/module/nvme_core/parameters/admin_timeout
   ```
   

   As shown in the following figure, the timeout period for both instance I/O operations and Admin operations is `4294967295` seconds.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c899b47801aa982da535ccfbc9e22b9.png) </span>
