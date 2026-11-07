---
title: "How to handle hangs when mounting file systems for Local SSD instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How_to_solve_the_issue_of_Local_Disk_instance_file_system_mount_hanging"
---

<span id="GkufL0Mb"></span>
## Issue description

When you perform the mount operation for file systems, like the ext4 file system in instances associated with local volumes (for example, instances of the Big data type and Local SSD type) for the first time, lock contention may occur. This can cause command hangs.

<span id="1ACtSGV9"></span>
## Causes

The inode table needs to be initialized when the mount operation is performed for the first time. For Linux kernel versions 2.6.37 and later, the lazyinit (delayed initialization) feature is enabled by default. This causes the initialization of the inode table to be postponed until after the mount operation. During initialization, the local volume consumes significant throughput. As a result, the business operates less stably, and operational exceptions may also occur, such as lagging or slow response.

<span id="KeZowes1"></span>
## Solutions


* Method 1: Disable lazyinit during mkfs formatting

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   2. Execute the following command to disable lazyinit.

      ```Bash
      mkfs.ext4 -E lazy_itable_init=0,lazy_journal_init=0 /dev/sda1
      ```
      

   3. View the I/O status of the formatted local volume.

      ```Bash
      iostat -x 5
      ```
      

      When the I/O activity of the local volume shows zero, which indicates that initialization is completed, perform the mount operation.

* Method 2: Use xfs file system or select an image with kernel version 4.x or later

   Using the xfs file system can effectively avoid this issue. Or, select images such as veLinux 1.0 CentOS compatible edition with 5.10 kernel, CentOS Stream 9, and other images with kernel version 4.x or later. This can also mitigate this issue.
