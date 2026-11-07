---
title: "Unmounting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Unmounting_file_systems"
---

This topic explains how to unmount a file system from an ECS instance.

<span id="d1fb3d11"></span>
## Prerequisites 

The file system has been mounted on the ECS instance. For detailed steps, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/Mounting_file_systems).

<span id="5d90345c"></span>
## Steps


1. [Use the console to log onto a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run this command to see the details of the file system mounted.

   ```Plain
   mount -l
   ```
   

3. Run this command to unmount the file system.

   ```Plain
   umount <directory name>
   ```
   

   Example:

   ```Plain
   umount /localdir
   ```
