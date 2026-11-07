---
title: "Creating a file system on a raw device"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create-a-file-system-on-raw-devices"
---

This topic uses an ECS instance running CentOS 7.6 to illustrate how to create a file system on a raw device. If you do not need logical partitions (e.g., `/dev/vdb1` or `/dev/vdb2`) for your volume, create a file system directly on the volume instead of partitioning it. Note that this operation only applies to Linux systems.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a volume and attached it to an ECS instance. For more information, see [Creating a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume) and [Attaching a volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

* Use e2fsprogs version 1.42 or later if your volume is 16 TiB or larger, or if you plan to expand it to that size. Errors will occur during formatting if the e2fsprogs package version is below 1.42. For more information, see [How to upgrade e2fsprogs version](https://docs.byteplus.com/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB).


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run this command to find the name of the volume you want to manage.

   ```Plain Text
   fdisk -l
   ```
   

   As shown in the output below, the instance has two attached volumes: the system volume, `/dev/vda1`, and the newly added data volume, `/dev/vdb`.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ba55c67182a5d80f93fa9aeeea7c4496.png) </span>

3. Run the `mkfs -t <file system format> /dev/vdb` command to create a file system directly on the raw device, `/dev/vdb`.

   Different file systems support different partition sizes. Select a file system that best meets your business needs. The following command sets the file system to `xfs`.

   ```Plain Text
   mkfs -t xfs /dev/vdb
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Formatting takes time. Monitor the system status and do not exit.   </div>
   

4. Run the `mkdir <mount point>` command to create a mount point.

   The following command creates a mount point, `/data`.

   ```Plain Text
   mkdir /data
   ```
   

5. Run the `mount /dev/vdb <mount point>` command to mount the volume to the newly created mount point.

   The following command mounts the volume to the mount point, `/data`.

   ```Plain Text
   mount /dev/vdb /data
   ```
   

6. Run this command to verify the mount result.

   ```Plain Text
   df -Th
   ```
   

   The output below shows the mount point corresponding to the volume, indicating that the mount was successful.

   ```Plain Text
   Filesystem     Type      Size  Used Avail Use% Mounted on
   /dev/vda1      ext4       39G  1.7G   37G   5% /
   devtmpfs       devtmpfs  4.1G     0  4.1G   0% /dev
   tmpfs          tmpfs     4.2G     0  4.2G   0% /dev/shm
   tmpfs          tmpfs     4.2G  9.1M  4.1G   1% /run
   tmpfs          tmpfs     4.2G     0  4.2G   0% /sys/fs/cgroup
   tmpfs          tmpfs     821M     0  821M   0% /run/user/0
   /dev/vdb       xfs        21G   34M   20G   1% /data
   ```
