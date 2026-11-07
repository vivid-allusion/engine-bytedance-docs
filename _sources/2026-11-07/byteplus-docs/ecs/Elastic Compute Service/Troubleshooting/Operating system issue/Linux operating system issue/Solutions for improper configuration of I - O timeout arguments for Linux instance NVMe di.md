---
title: "Solutions for improper configuration of I/O timeout arguments for Linux instance NVMe disks"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solutions_for_improper_configuration_of_IO_timeout_arguments_for_Linux_instance_NVMe_disks"
---

If the ECS instance of the Linux system uses the NVMe system disk and experiences unexpected slow I/O reads and writes due to improper configuration of I/O timeout arguments (such as the timeout period for I/O read and write operations on NVMe disks being set too small), leading to system and application exceptions or business interruptions, you can solve the issue by adjusting the `io_timeout` argument of the NVMe driver.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Slow I/O read and write: Refers to the execution speed of input/output operations during disk read/write processes being lower than expected or required time.</div>


<span id="7n1GeBYb"></span>
### Causes

The `io_timeout` argument in the NVMe driver is used to control the maximum tolerable I/O timeout period. If the latency of the I/O read/write operation is too high and exceeds the configured value of this argument, the NVMe driver will return an I/O failure. This will cause the file system on the NVMe disk to switch from the previously mounted readable and writable status to a read\-only status, making subsequent write operations all fail, and thereby resulting in system and application exceptions or business interruptions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In most Linux platform versions, the argument is set to a default configuration of 30 seconds.</div>


<span id="H2B3kkI7"></span>
## Procedure


<Tabs>
<Tab zoneid="CYabTjDdOw" title="Configure the io_timeout argument (temporary)">
<TabTitle>Configure the io_timeout argument (temporary)</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The temporary configuration of the <code>io_timeout</code> argument will expire after restarting the instance.</div>



1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check the `path` of the kernel module where the io_timeout argument is located.

   ```Plain Text
   cat /sys/module/nvme_core/parameters/io_timeout
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Due to differences in kernel version, the kernel module for the NVMe driver may also vary. It generally includes <code>nvme.ko</code> or <code>nvme_core.ko</code>, so the complete name of the timeout argument is <code>nvme.io_timeout</code> or <code>nvme_core.io_timeout</code>.   </div>
   

3. Execute the following command to write the desired timeout period into the kernel module. Once configured, it will take effect immediately.

   ```Plain Text
   sudo sh -c 'echo {Value} > /sys/module/nvme_core/parameters/io_timeout'
   ```
   

    or 

   ```Plain Text
   sudo sh -c 'echo {Value} > /sys/module/nvme/parameters/io_timeout'
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace the <code>Value</code> in the command with the actual timeout period to be adjusted.   </div>
   


</Tab>
<Tab zoneid="ksW2prb378" title="Configure the io_timeout argument (permanent)">
<TabTitle>Configure the io_timeout argument (permanent)</TabTitle>

You can modify grub to updatethe io_timeout argument for permanent configuration effect.


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Run the following command to access the `/etc/default/grub` file.

   ```Plain Text
   sudo nano /etc/default/grub
   ```
   

3. Add `nvme_core.io_timeout={Value}` to `the GRUB_CMDLINE_LINUX` field.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace <code>Value</code> in the command with the actual timeout period to be adjusted.   </div>
   

4. Input `:wq` and press Enter to save and exit.

5. Run the following command to update the GRUB bootloader configuration file.

   ```Plain Text
   update-grub
   ```
   

6. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to make the configuration take effect.


</Tab>
</Tabs>
