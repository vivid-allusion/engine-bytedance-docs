---
title: "How do I solve the disk Inflight I/O hang issue that occurs on ECS instances using the veLinux 1.0 image?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/solve_the_disk_Inflight_I_O_hang_issue"
---

## Description

A disk Inflight I/O hang issue occurs on ECS instances running the veLinux 1.0 operating system with a 5.4.x kernel, and the following call stack information is displayed.

```Plain Text
[ffffb168439277f0] _raw_spin_lock at ffffffffb7a0327a
[ffffb168439277f8] ext4_mb_discard_group_preallocations at ffffffffc03627a1 [ext4]
[ffffb168439278a8] ext4_mb_new_blocks at ffffffffc03649e0 [ext4]
[ffffb16843927950] ext4_ext_map_blocks at ffffffffc033eae5 [ext4]
[ffffb16843927a18] ext4_map_blocks at ffffffffc035181f [ext4]
[ffffb16843927a88] ext4_writepages at ffffffffc03560c1 [ext4]
[ffffb16843927bd8] do_writepages at ffffffffb73f1e0e
[ffffb16843927c50] __filemap_fdatawrite_range at ffffffffb73e7f0b
[ffffb16843927cd8] ext4_release_file at ffffffffc03436ec [ext4]
[ffffb16843927cf8] __fput at ffffffffb74b1283
```

## Causes

Due to the continuous abnormal full load of the instance disk, a kernel failure is triggered, causing Kworker to get stuck by a spinlock. This results in a large number of hung tasks, and there are unfinished I/O operations (inflight I/O) in the block device cache, due to the malfunction of Write Back Throttling (WBT).

## Solutions

### Fix the issue by using the kernel live patching capability

You can fix the issue without the need to restart the instance or the applications running on the instance.

> **tip**

> BytePlus currently provides live patches only for the following kernel versions. For other kernel versions, you can [upgrade the kernel to the fixed version](https://docs.byteplus.com/en/docs/ecs/solve_the_disk_Inflight_I_O_hang_issue#uFLIBAeV).

* > 5.4.56\-1\-veLinux1u2

* > 5.4.56\-1\-veLinux1\-amd64

* > 5.4.250\-9\-veLinux1\-amd64

* > 5.4.250\-6.ve1.x86_64

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check the kernel version of the operating system.

   ```Plain Text
   sudo uname -r
   ```

   When the following output is displayed, the kernel version is `5.4.56-1-veLinux1`.

   ```Plain Text
   5.4.56-1-veLinux1-amd64
   ```

3. Install the hot patch by running the corresponding command according to the operating system and kernel version.

   **veLinux 1.0**

* **Kernel version: 5.4.56\-1\-velinux1**

      ```Plain Text
      sudo apt install -y livepatch-5.4.56-1-velinux1-ext4-abba-lock-fix
      ```

   * **Kernel version: 5.4.56\-1\-velinux1u2**

      ```Plain Text
      sudo apt install -y livepatch-5.4.56-1-velinux1u2-ext4-abba-lock-fix
      ```

   * **Kernel version: 5.4.250\-9\-velinux1**

      ```Plain Text
      sudo apt install -y livepatch-5.4.250-9-velinux1-ext4-abba-lock-fix
      ```

   **veLinux 1.0 CentOS Compatible**

**Kernel version: 5.4.250\-6.ve1**

   ```Plain Text
   sudo yum install -y livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix-1.0-1.x86_64.rpm
   ```

4. Execute the following command to check whether the hot patch is successfully installed.

   ```Plain Text
   sudo lsmod | grep livepatch
   ```

   When the following output is displayed, the hot patch is successfully installed.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc4da5ef731d345563a91dd0ef97d10b.png)

### **Upgrade the kernel to the fixed version**

> **warning**

> Upgrading the system kernel may lead to compatibility, stability, and security issues. We recommend that you [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) before you upgrade the kernel.

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Upgrade the kernel version.

   **veLinux 1.0**

```Plain Text
   Kernel_Version="<target kernel version>"
   sudo apt update && sudo apt install linux-headers-$Kernel_Version linux-image-$Kernel_Version
   ```

   **veLinux 1.0 CentOS Compatible**

```Plain Text
   Kernel_Version="<target kernel version>"
   sudo yum update kernel-$Kernel_Version kernel-devel-$Kernel_Version kernel-headers-$Kernel_Version
   ```

   > **tip**

   > Replace `<target kernel version>` with the kernel version that fixes the issue.

   * > veLinux 1.0: 5.4.250\-9\-velinux1u1\-amd64 and later

   * > veLinux 1.0 CentOS Compatible: 5.4.250\-9.1.ve1 and later

3. Execute the following command to restart the ECS instance.

   ```Plain Text
   sudo reboot
   ```
