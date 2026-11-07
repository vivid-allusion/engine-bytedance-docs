---
title: "Step 2: Replace the faulty volume (non-EBM instances)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Replacing-faulty-volumes"
---

This topic describes how to authorize the replacement of a faulty local disk when a local volume fails.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please read carefully and follow this document, which is part of the ECS service rules provided to you. If you do not follow the instructions here, your business may suffer losses, and you acknowledge and agree to take full responsibility for the losses.</div>


<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When you receive a DiskErrorDetected (disk exception) event, you can authorize BytePlus to replace the faulty disk. This helps prevent more serious issues such as instance downtime caused by the disk failure.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This feature is currently not available for instances of the Elastic Bare Metal (EBM) type, Local SSD i2g, and HPC\-optimized types (hpcpni2, ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2). For details, refer to [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* Please follow the [procedure](https://docs.byteplus.com/en/docs/ecs/Replacing-faulty-volumes#.5pON5L2c5q2l6aqk) to modify the local disk configuration first before you authorize O&M operations. Otherwise, the newly replaced local volume may not be recognized properly.

* There is a risk of data loss during replacement of the faulty volume. Please back up data in advance to prevent data loss. You can back up data using [volumes](https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh), [TOS](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh), or other methods.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6I635Y-W5pWF6Zqc56Gs55uY5bqP5YiX5Y-3"></span>
### Step 1: Obtain the serial number of the faulty hard disk

When a local volume mounted to an instance fails, BytePlus will synchronize the serial number (SN) of the faulty hard disk with you. Therefore, you can locate the faulty hard disk for the instance accurately and easily.

You can call the [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) interface, pass in the event ID of the hard disk exception, and obtain the SN of the faulty hard disk from the returned data.


* If the instance with the faulty hard disk is a first\-generation HDD instance (for example, Big Data Storage\-optimized d1s), the value of the `SystemEvents.ExtraInfo.Address` parameter in the returned data is the SN of the faulty hard disk.

* If the instance with the faulty hard disk is a second\-generation HDD instance (for example, [Big Data d2s](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5Z6LZDJz), [Big Data d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5Z6LZDJj), and [Big Data d2](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5Z6LZDI=)), or an instance of Local SSD type (for example, [Local SSD i2](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#.5pys5Zywc3Nk5Z6LaTJn)), the value of the `SystemEvents.ExtraInfo.Serial` parameter in the returned data is the SN of the faulty hard disk.


<span id=".5q2l6aqk5LqM77ya5L-u5pS556Gs55uY6YWN572u"></span>
### Step 2: Modify the hard disk configuration


1. Log in to the ECS instance where the faulty volume is mounted. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to view the drive letter of the faulty local volume.

   * First\-generation HDD instance

      If your instance is a first\-generation HDD instance (for example, [Big Data Storage-optimized d1s](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5a2Y5YKo5Z6LZDFz)), execute the following command to view the drive letter of the faulty hard disk.

      > Replace `$SN$` with the actual SN of the hard disk.      
      

      ```Plain Text
      ls -al /dev/disk/by-path/ | grep $SN$
      ```
      

   * Second\-generation HDD or Local SSD instance

      If your instance is a second\-generation HDD instance (for example, [Big Data d2s](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5Z6LZDJz), [Big Data d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5Z6LZDJj), and [Big Data d2](https://docs.byteplus.com/en/docs/ecs/Big-data-based#.5aSn5pWw5o2u5Z6LZDI=)), or an instance of Local SSD type (for example, [Local SSD i2](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#.5pys5Zywc3Nk5Z6LaTJn)), execute the following command to view the drive letter of the faulty hard disk.

      > Replace `$SN$` with the actual SN of the hard disk.      
      

      ```Plain Text
      lsblk -oNAME,SERIAL | grep $SN$
      ```
      

3. Execute the following command to view the file system and UUID of the faulty local volume.

   > Replace `/dev/vda2` with the actual drive letter of the faulty volume obtained in the previous step.   
   

   ```Plain Text
   blkid /dev/vda2
   ```
   

4. Execute the following command to edit the /etc/fstab file.

   1. Open the /etc/fstab file.

      ```Plain Text
        vim /etc/fstab
      ```
      

   2. Press the `i` key to enter edit mode, and add the `nofail` parameter after the target local volume in the file.

      > Only the `nofail` parameter needs to be added and no other content requires adjustment.      
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29d13830ebee801744cce4f7830cfd2e.png) </span>

      **Description of fstab file arguments**

      
      |Parameter​ |Description |
      |---|---|
      |24fd1325\-bbf3\-4814\-b7e9\-041deba\*\*\*\*\* |The UUID of the faulty local volume. |
      |/ |The mount point of the faulty local volume. |
      |ext4 |The file system type of the faulty local volume. |
      |nofail |When a local volume is present in the file system but actually missing, the startup process of the ECS instance will not be interrupted. |
      

   3. Press `Esc` and enter `:wq` to save the change and exit.

5. Execute the following command to unmount the faulty local volume.

   ```Plain Text
   umount /dev/vda2
   ```
   


<span id=".5q2l6aqk5LiJ77ya5o6I5p2D6L-Q57u0"></span>
### Step 3: Authorize O&M


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events" to go to the Events page.

3. In the top menu bar, select the region and project of your business.

4. On the Events page, you can search the target event based on the time range, event ID, or instance ID.

5. Click the "Maintenance operation" button in the "Actions" column of the target event to go to the maintenance configuration page.

   1. Select "Replace the faulty volume" for "Operation and maintenance method".

   2. (**Optional**) Before you replace the faulty volume, if you need to prevent applications running on the instance from reading from and writing to the faulty volume to minimize data loss, authorize isolating the hard disk first. For more information, refer to [Isolating the local volume (optional)](https://docs.byteplus.com/en/docs/ecs/Isolating-local-volumes).

   3. Click the "Authorize maintenance" button, then click the "Confirm" button in the confirmation pop\-up window to authorize BytePlus O&M personnel to replace the faulty hard disk.

      > After the authorization, a DiskError.ReplaceDisk (Hard disk replacement due to exception) event will be generated. The event aims to inform you the progress of replacing the faulty disk.      
      

6. If an issue occurs during the faulty volume replacement, you will receive a DiskError.ReplaceDisk:Pending event notification. After you receive the notification, follow the instructions to restart the instance or submit a ticket to resolve the issue.

   * Resolve the issue by restarting the instance

      As shown in the picture below, follow the instructions, click the "Restart instance" button, and restart the instance to resolve the issue.

   * Resolve the issue by submitting a ticket

      As shown in the picture below, follow the instructions and submit a ticket to contact BytePlus O&M personnel to resolve the issue.


<span id=".5q2l6aqk5Zub77ya5oyC6L2956Gs55uY"></span>
### Step 4: Mount the hard disk


1. After the faulty volume is replaced, you will receive a DiskError.ReplaceDisk:Succeeded event notification. After receiving the notification, you need to log in to the instance to mount the local volume.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance fails to identify the local volume after the faulty volume is replaced, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> for technical support.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you use UUID instead of device names (such as /dev/data1) for mounting.   </div>
   

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   2. Execute the following command to view information about the unmounted data volume (the new local volume).

      ```Plain Text
      lsblk -l
      ```
      

   3. Execute the following command to create a file system for the data volume to be mounted.

      ```Plain Text
      mkfs -t <File System> <UUID>
      ```
      

   4. Execute the following command to mount the data volume.

      ```Plain Text
      mount -U <UUID> <Mount Point>
      ```
      

2. Execute the following command to check whether the data volume is mounted.

   ```Plain Text
   df -h
   ```
