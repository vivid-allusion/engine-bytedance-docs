---
title: "Enabling Kdump service in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enabling_Kdump_service_in_Linux_operating_system"
---

You can enable Kdump on an ECS instance running the Linux operating system to quickly identify the cause of a kernel crash within the instance.

In the example provided in this topic, the CentOS 7.9 operating system is used to describe how to install, configure, and enable Kdump.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Enabling Kdump consumes some operating system memory and disk space, which may affect system performance.</div>


* <div data-tips="true" data-tips-type="warning">The methods for enabling Kdump vary across different Linux operating systems. For the specific methods, see the following official documentation:</div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/kernel_administration_guide/kernel_crash_dump_guide">Red Hat Enterprise Linux/CentOS</a></div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://ubuntu.com/server/docs/kernel-crash-dump">Debian/Ubuntu</a></div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://doc.opensuse.org/documentation/leap/tuning/html/book-tuning/cha-tuning-kexec.html">SUSE/OpenSUSE</a></div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://www.kernel.org/doc/Documentation/kdump/kdump.txt">Other Unix\-like operating systems</a></div>



<span id=".5LuA5LmI5pivS2R1bXDvvJ8="></span>
## What is Kdump?

Kdump is a kernel crash dumping technology based on kexec. When the Linux system kernel crashes due to hardware failures, software errors, driver issues, or other reasons that render the system inoperable, Kdump can capture the memory state information of the kernel at the time of the crash and save this information to the disk. Maintenance personnel can analyze and identify the cause of the kernel crash based on the Kdump dump file. [Learn more](https://www.kernel.org/doc/Documentation/kdump/kdump.txt).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to install the Kdump tool.

   ```Plain Text
   yum install crash kexec-tools makedumpfile -y
   ```
   

3. Specify the size of memory for crash dumps.

   1. Execute the following command to open the kernel configuration file.

      ```Plain Text
      vim /etc/default/grub
      ```
      

   2. Press the `i` key to enter edit mode, and change the value of the `crashkernel` parameter in `GRUB_CMDLINE_LINUX` from `auto` to `128M`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>128M</code> with the amount of memory you want to reserve for crash dumps (Kdump).      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the <code>GRUB_CMDLINE_LINUX</code> line does not contain the <code>crashkernel</code> parameter, manually add the parameter.      </div>
      

      Example after modification:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_683becd65ccdcecb7af4c55ab1652497.png) </span>

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

   4. Execute the following command to update the GRUB configuration file for the configuration to take effect.

      * BIOS boot mode

         ```Plain Text
         sudo grub2-mkconfig -o /boot/grub2/grub.cfg
         ```
         

      * UEFI boot mode

         ```Plain Text
         sudo grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
         ```
         

   5. Execute the following command to restart the instance.

      ```Plain Text
      reboot
      ```
      

4. Configure Kdump.

   1. Execute the following command to open the kernel configuration file.

      ```Plain Text
      vim /etc/kdump.conf
      ```
      

   2. Press the `i` key to enter edit mode and modify the following content:

      * `path /var/crash`: Replace `/var/crash` with the directory where you want to store Kdump files. In the example provided in this topic, the default path is used.

      * `core_collector makedumpfile -l -message-level 1 -d 31`: Add the `-c` parameter to compress the Kdump file for lower disk usage.

      * `default reboot`: Add this line to specify that the operating system restarts after Kdump is generated.

      Example after modification:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb5277e5f35803e90104c4c8665bc56b.png) </span>

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

5. Enable Kdump.

   1. Execute the following command to run the Kdump tool.

      ```Plain Text
      systemctl start kdump.service
      ```
      

   2. Execute the following command to specify that the Kdump tool automatically starts upon instance startup.

      ```Plain Text
      systemctl enable kdump.service
      ```
      

   3. Execute the following command to view the Kdump running status.

      ```Plain Text
      systemctl status kdump.service
      ```
      

      Sample output when Kdump runs as expected:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6e3b85a1c0ed256c8ff946ee26fcba91.png) </span>

6. Execute the following commands in sequence to manually trigger a kernel crash, and then verify whether Kdump is available.

   ```Plain Text
   echo 1 > /proc/sys/kernel/sysrq
   echo c > /proc/sysrq-trigger
   ```
   

   * If Kdump is running as expected, the system automatically restarts and generates the content shown in the following figure in the Kdump file storage directory you specified (in this topic, `/var/crash`).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f99c06812f0c3d4f379d40c92da1904e.png) </span>

   * If Kdump is not running as expected, refer to the previous sections to check whether Kdump is correctly installed and configured.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

You can use the crash tool to read important contents from Kdump files and analyze the cause of the kernel crash.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Install the kernel\-debug package.

   1. Execute the following command to view the current kernel version of the operating system.

      ```Plain Text
      uname -r
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c66aa86c25de5b463ade6312f80f26d2.png) </span>

   2. Go to the [official CentOS mirror site](http://debuginfo.centos.org/7/x86_64/) and obtain the download links for the two RPM packages, kernel\-debuginfo\-common and kernel\-debuginfo, which match the kernel version of your instance.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d77f7137dc9f7ac8aa1da9163dad12a.png) </span>

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b04570c9031da8cf1e936ded7d970a58.png) </span>

   3. Download and install the corresponding RPM packages.

      1. Execute the following command to download the kernel\-debuginfo\-common package.

         ```Plain Text
         wget http://debuginfo.centos.org/7/x86_64/kernel-debuginfo-common-x86_64-3.10.0-1160.102.1.el7.x86_64.rpm
         ```
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Replace the link after the <code>wget</code> command with the actual RPM package download link.         </div>
         

      3. Execute the following command to install the kernel\-debuginfo\-common package.

         ```Plain Text
         rpm -ivh kernel-debuginfo-common-x86_64-3.10.0-1160.102.1.el7.x86_64.rpm
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>kernel-debuginfo-common-x86_64-3.10.0-1160.102.1.el7.x86_64.rpm</code> with the actual name of the downloaded RPM package.         </div>
         

               3. Execute the following command to download the kernel\-debuginfo package.

         ```Plain Text
         wget http://debuginfo.centos.org/7/x86_64/kernel-debuginfo-3.10.0-1160.102.1.el7.x86_64.rpm
         ```
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Replace the link after the <code>wget</code> command with the actual RPM package download link.         </div>
         

      4. Execute the following command to install the kernel\-debuginfo package.

         ```Plain Text
         rpm -ivh kernel-debuginfo-3.10.0-1160.102.1.el7.x86_64.rpm
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>kernel-debuginfo-3.10.0-1160.102.1.el7.x86_64.rpm</code> with the actual name of the downloaded RPM package.         </div>
         

3. Install crash.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also go to the <a href="https://crash-utility.github.io/">official crash website</a> to download and install the required version.   </div>
   

   ```Plain Text
   yum install crash -y
   ```
   

4. Execute the following command to view the crash version and check whether crash is installed.

   ```Plain Text
   crash -v
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9fa716589c48f7ca0954386588bb12c9.png) </span>

5. Use crash to view Kdump information.

   1. Execute the following command to enter the crash command line page and view Kdump file information.

      ```Plain Text
      crash /usr/lib/debug/lib/modules/$(uname -r)/vmlinux /var/crash/<timestamp>/vmcore
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code><timestamp></code> with the timestamp when the Kdump file is generated.      </div>
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b773a7e04d247e676e61edb357e95621.png) </span>

   2. The crash tool provides various commands to help you quickly extract key information from the Kdump file. [Learn more](https://crash-utility.github.io/help.html).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b4082600a766262ce3601c6e8a35b01.png) </span>

   3. To exit crash interactive mode and stop crash, enter `exit` or `q`, and then press the Enter key to confirm.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9df11ea3531b1d6ef1b93ea419297d9a.png) </span>
