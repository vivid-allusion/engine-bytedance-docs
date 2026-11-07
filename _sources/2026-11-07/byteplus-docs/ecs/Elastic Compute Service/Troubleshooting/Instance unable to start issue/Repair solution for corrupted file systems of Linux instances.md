---
title: "Repair solution for corrupted file systems of Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Repair_plan_for_damaged_file_system_of_Linux_instance"
---

This topic describes how to repair corrupted file systems of a Linux instance, with` /dev/vdb` used as an example.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

We recommend [creating a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) first to back up instance data. This improves your fault tolerance and ensures data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to confirm whether a file system is mounted on the instance.

   ```Plain Text
   df -h
   ```
   

3. (**Optional**) If a file system is mounted, execute the following command to unmount it.

   ```Plain Text
   umount /dev/vdb
   ```
   

4. Execute the following command to view the file system type of the target partition or storage device.

   ```Plain Text
   blkid
   ```
   

   **Sample output:** 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80c26ce9e171fa13830318d7ab16af97.png) </span>

5. Execute commands to check and repair the file system based on the file system type.

   
   <Tabs>
   <Tab zoneid="xtdLKhAWgS" title="EXT3/EXT4 file system">
   <TabTitle>EXT3/EXT4 file system</TabTitle>
   
   1. Execute the following command to check whether an error exists in the file system.
   
      ```Plain Text
      sudo fsck -n /dev/vdb
      ```
      
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the output contains an error about <code>The super block Cloud no be read or does not describe a correct ext2 filesystem</code> when you check for file system errors, skip to Step 3 for repair.   </div>
      
   
   2. If an error exists in the file system, execute the following command to repair it.
   
      ```Plain Text
      sudo fsck -y /dev/vdb
      ```
      
   
   3. If the superblock is corrupted, follow the steps below to repair it.
   
      1. Execute the following command to obtain backup superblock numbers.
   
         ```Plain Text
         sudo mke2fs -n /dev/vdb
         ```
         
   
         * If the following output is displayed, it indicates that the backup superblock numbers for /dev/vdb are `32768`, `98304`, `163840`, `229376`, `294912`, `819200`, `884736`, `1605632`, `2654208`, and `4096000`.
   
            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cfaea0bbb70536a078fb2dd02982dcd9.png) </span>
   
         * When you cannot obtain the backup superblock numbers using the command, perform the following steps to obtain common backup superblock numbers.
   
            1. Execute the following command to obtain the block size.
   
               ```Plain Text
               sudo blockdev --getbsz /dev/vdb
               ```
               
   
               When the following output is displayed, it indicates that the block size of /dev/vdb is 4096 bytes:
   
               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_481dba0d0aef00a9f748f7c8f2924d0f.png) </span>
   
            2. Refer to the following table to obtain the common backup superblock numbers corresponding to the block size.
   
               
               |Block size (bytes) |Common backup superblock numbers |
               |---|---|
               |1,024 |8193, 24577, 40961... |
               |2,048 |16384, 49152, 81920... |
               |4096 |32768, 98304, 163840, 229376... |
               |8192 |65536, 196608, 327680... |
               
   
      2. Execute the following command to repair the superblock using a backup superblock.
   
         ```Plain Text
         sudo e2fsck -b 32768 /dev/vdb
         ```
         
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>32768</code> with the actual backup superblock number. If the first backup superblock number is invalid, you can try other backup blocks in order.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>/dev/vdb</code> with the actual disk name rather than the partition name.      </div>
         
   
   
   </Tab>
   <Tab zoneid="mx7dbWlO8t" title="XFS file system">
   <TabTitle>XFS file system</TabTitle>
   
   1. Execute the following command to check whether an error exists in the file system.
   
      ```Plain Text
      sudo xfs_repair -n /dev/sdb
      ```
      
   
   2. If an error exists in the file system, execute the following command to repair it.
   
      ```Plain Text
      sudo xfs_repair /dev/sdb
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="fEFeMia3do" title="VFAT/FAT32 file system">
   <TabTitle>VFAT/FAT32 file system</TabTitle>
   
   1. Execute the following command to check whether an error exists in the file system.
   
      ```Plain Text
      sudo fsck.vfat -n /dev/sdb
      ```
      
   
   2. If an error exists in the file system, execute the following command to repair it.
   
      ```Plain Text
      sudo fsck.vfat -a /dev/sdb
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   

6. After the repair is completed, execute the following command to restart the instance.

   ```Plain Text
   reboot
   ```
   

7. (**Optional**) If the target volume is a system volume, mount the file system. If the target volume is a data volume, skip this step.

   1. Execute the following command to mount a file system.

   ```Plain Text
   mount /dev/vdb /mnt
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>/mnt</code> with the actual mount point.   </div>
   

   2. Execute the corresponding command again to check the mounted file system.

      * For XFS file system: `xfs_repair /dev/vdb`

      * For EXT3 and EXT4 file systems: `fsck -y /dev/vdb`

      Here, `fsck -y /dev/vdb` is used as an example. Output similar to the following information indicates that the repair succeeds.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0750f6fd27b320b0a1f536bd760fcf59.png) </span>
