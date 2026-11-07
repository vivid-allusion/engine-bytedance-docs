---
title: "Kernel live patching overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview_of_kernel_live_patching"
---

BytePlus provides live patching capabilities to fix high\-severity Common Vulnerabilities and Exposures (CVEs) and important bugs in the veLinux image kernel. With these capabilities, you can quickly and seamlessly apply patches to the kernel without restarting the instance or the applications running on it, waiting for long\-running tasks to complete, asking users to log out and log back in, or migrating applications. This improves the stability and security of the kernel.

<span id="vDP1nou7"></span>
## Usage notes

The kernel live patching capabilities mainly apply to CVEs of Critical or higher severity and critical bugs. Each patch consists of the following components:


* DEB/RPM package: Contains kernel modules (ko files) and the patch description file. The kernel fixes issues by loading the kernel modules included in the patch.

* Livepatch system service: A system daemon (systemd) for kernel live patching. This service loads kernel modules for each patch during the operating system initialization phase to fix kernel issues.


<span id="Cro9Qo4i"></span>
## Precautions


* Supported operating systems

   
   |Operating system |Operating system version |Kernel version |
   |---|---|---|
   |veLinux |veLinux 2.0 |* All kernel versions support live patching.<br><br>* No special configurations are required. |
   ||veLinux 1.0 |* Kernel version ＜ 5.4.250\-1\-velinux<br><br>* Kernel version ＞ 5.4.250\-5\-velinux1u1<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the kernel version of your operating system falls within the range of 5.4.250\-1\-velinux to 5.4.250\-5\-velinux1u1 (including 5.4.250\-1\-velinux and 5.4.250\-5\-velinux1u1), the kernel live patching feature is not supported. In this case, we recommend that you upgrade the kernel version.</div><br> |
   

* For each kernel version of the veLinux operating system, veLinux provides kernel live patching capabilities within a validity period of one year. After the validity period ends, you need to upgrade the kernel version of the operating system to the latest version.

* You can use the kernel live patching capabilities to fix only specific CVEs of the High severity and specific important bugs. The kernel live patching capabilities aim to reduce instance restarts caused by patch updates but cannot eliminate instance restarts.

* Kernel live patching is not a universal kernel update solution. It is only applicable to fixing CVEs of the High severity and important bugs in scenarios where you do not want to restart the instance immediately.

* During the patch update process and after the patch takes effect, you cannot use tools such as SystemTap or kprobe to test or trace the functions involved in the patch. Otherwise, the patch becomes invalid.


<span id="chuDGqEx"></span>
## Live patching solution

[How do I solve the disk Inflight I/O hang issue that occurs on ECS instances using the veLinux 1.0 image?](https://docs.byteplus.com/en/docs/ecs/solve_the_disk_Inflight_I_O_hang_issue)
