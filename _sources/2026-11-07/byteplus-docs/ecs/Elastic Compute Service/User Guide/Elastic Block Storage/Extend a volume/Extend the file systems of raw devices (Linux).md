---
title: "Extend the file systems of raw devices (Linux)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Extend-the-file-systems-of-raw-devices-Linux"
---

In a scenario in which you create a file system without partitioning a volume, perform the procedure described in this topic to expand your volume.

<span id="precautions"></span>
## Precautions

This operation can be performed on a Linux system.

<span id="procedure"></span>
## Procedure


1. [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to view the file system type of your volume:

   ```Plain Text
   df -ihT
   ```
   

   A result is returned as displayed below. The following result indicates that XFS is used as the file system type:

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0b776135d9c6fffbdf67a4746d89cbf5.png) </span>

3. Run either of the following commands to expand your volume based on its file system type:

   * Ext file system:

      ```Plain Text
      resize2fs /dev/vdb
      ```
      

   * XFS file system:

      ```Plain Text
      xfs_growfs /dev/vdb
      ```
      

4. Run the following command to view information on the drive space of your file system:

   ```Plain Text
   df -h
   ```
