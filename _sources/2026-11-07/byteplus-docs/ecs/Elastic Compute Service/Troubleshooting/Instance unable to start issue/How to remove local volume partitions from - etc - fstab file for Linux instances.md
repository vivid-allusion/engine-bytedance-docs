---
title: "How to remove local volume partitions from /etc/fstab file for Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/remove-instances_etc_local"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

If you have configured custom partitions for your instance mounted with local volumes, you need to remove the local volume partition information from the /etc/fstab file before cold migration or failure evacuation is performed. Otherwise, the instance fails to start normally after migration.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

When the custom partition feature is configured for a local volume of an instance, and the partition information of the local volume after migration is missing, the migrated instance fails to start normally.

You need to remove the information of local volume partitions as instructed in the solution. After cold migration, you can use ECS Terminal to log in to the instance normally. Otherwise, you cannot use ECS Terminal to log in to the instance, and when you log in to the instance using VNC, the instance enters emergency mode. In this case, see [Solution of /etc/fstab configuration repair for Linux instances](https://docs.byteplus.com/en/docs/ecs/Linux_instance_fstab_configuration_repair_solution) to fix the issue.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During cold migration, all the data stored in the local volume is automatically cleared. Please ensure that you back up the data beforehand.</div>



1. Use VNC to log in to the instance to be cold\-migrated. For detailed operations, refer to [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to enter the /etc/fstab file.

   ```Plain Text
   vim /etc/fstab
   ```
   

   Example:

   /data00, /data01, and /data02 are mount points for partitions of the local data volumes.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ee47bef712b01e89fd59f69e9159c8a.png) </span>

3. Press the `i` key to enter the edit mode, delete all partition information of the local data volumes, and retain only the mount information of the system volume.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff4fd4767a5cfa3460ff93ad0c401865.png) </span>

4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

5. After the /etc/fstab file is modified, cold migration or instance evacuation can be performed.
