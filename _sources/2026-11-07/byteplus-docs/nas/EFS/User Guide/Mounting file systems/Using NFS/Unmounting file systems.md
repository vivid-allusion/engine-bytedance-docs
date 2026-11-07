---
title: "Unmounting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Unmounting_file_systems_NFS"
---

This topic explains how to unmount a file system from an ECS instance.

<span id="kmAg8B9R"></span>
## Prerequisites

The file system is already mounted on the ECS instance. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_NFS).

<span id="6jnKJI91"></span>
## Steps


1. [Use the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run this command to view information about the mounted file system.

   ```Plain Text
   mount -l
   ```
   

3. Run this command to unmount the file system.

   ```Plain Text
   umount <mount directory>
   ```
   

   Example command:

   ```Plain Text
   umount /localdir
   ```
