---
title: "Unmount a file system"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Unmount-a-file-system"
---

This topic describes the steps to uninstall a file system on an ECS instance.

<span id="前提条件"></span>
## Prerequisite

The file system has been mounted to the ECS instance. For specific steps, please refer to [Mounting a file system](https://docs.byteplus.com/docs/nas/Mounting-a-file-system).

<span id="操作步骤"></span>
## **Procedure**


1. [Using the console to log on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the information of the mounted file systems.

   ```Plain
   mount -l
   ```
   

3. Execute the following command to uninstall the file system.

   ```Plain
   umount <directory name>
   ```
   

   Example：

   ```Plain
   umount /localdir
   ```
