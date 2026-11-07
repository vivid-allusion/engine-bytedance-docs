---
title: "Step 2: Replace the faulty volume (EBM instances)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/EBM-replacing-faulty-volumes"
---

This topic describes how to authorize the replacement of a faulty local disk when a local volume mounted to an EBM instance fails.

> This feature is in Beta. If you need a trial, please contact your account manager.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please read carefully and follow this document, which is part of the ECS service rules provided to you by BytePlus. If you do not follow the instructions here, your business may suffer losses, and you acknowledge and agree to bear all the losses​.</div>


<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When you receive a DiskErrorDetected (disk exception) event, you can authorize BytePlus to replace the faulty disk. This helps prevent more serious issues such as instance downtime caused by the disk failure.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This feature is only available for instances of the [Local SSD EBM ebmi3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-EBM#.5pys5Zywc3Nk5Z6L5by55oCn6KO46YeR5bGeZWJtaTNz) type.

* Please follow the [procedure](https://docs.byteplus.com/en/docs/ecs/EBM-replacing-faulty-volumes#.5pON5L2c5q2l6aqk) to modify the local disk configuration first before you authorize O&M operations. Otherwise, the newly replaced local volume may not be recognized properly.

* There is a risk of data loss during replacement of the faulty volume. Please back up data in advance to prevent data loss. You can back up data using [volumes](https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh), [TOS](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh), or other methods.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6I635Y-W5pWF6Zqc56Gs55uY5bqP5YiX5Y-3"></span>
### Step 1: Obtain the serial number of the faulty hard disk

When a local volume mounted to an instance fails, BytePlus synchronizes the serial number (SN) of the faulty hard disk with you. Therefore, you can locate the faulty hard disk for the instance easily.

You can call the [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation and pass in the event ID based on DiskErrorDetected (disk exception). The value of the `SystemEvents.ExtraInfo.Serial` parameter in the returned data is the SN of the faulty hard disk.

<span id=".5q2l6aqk5LqM77ya5L-u5pS556Gs55uY6YWN572u"></span>
### Step 2: Modify the hard disk configuration


1. Log in to the ECS instance where the faulty volume is mounted. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to view the drive letter of the faulty local volume.

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
      |nofail |When a local volume is present in the file system but actually missing, this parameter will not interrupt the ECS instance startup process. |
      

   3. Press `Esc` and enter `:wq` to save the change and exit.

5. Execute the following command unmount the faulty local volume.

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

   2. Click the "Authorize maintenance" button, then click the "Confirm" button in the confirmation pop\-up window to authorize BytePlus O&M personnel to replace the faulty hard disk.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After authorization, a DiskError.ReplaceDisk (Hard disk replacement due to exception) event will be generated. The event aims to remind you of the progress of replacing the faulty disk.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After authorization, do not perform any lifecycle operation on the instance (such as restart and shutdown).      </div>
      

6. If an issue occurs during the faulty volume replacement, you will receive a DiskError.ReplaceDisk:Pending event notification. After you receive the notification, follow the instructions to restart the instance or submit a ticket to resolve the issue.

   * Resolve the issue by restarting the instance

      As shown in the picture below, follow the instructions, click the "Restart instance" button, and restart the instance to resolve the issue.

   * Resolve the issue by submitting a ticket

      As shown in the picture below, follow the instructions and submit a ticket to contact BytePlus O&M personnel to resolve the issue.

7. After the faulty volume is replaced, you will receive a DiskError.ReplaceDisk:Succeeded event notification.


<span id=".5q2l6aqk5Zub77ya6L-b6KGM56Gs5Lu25qOA5rWL"></span>
### Step 4: Conduct hardware detection


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. Execute the following command in the instance to perform an in\-situ detection and confirm whether the local volume is connected to the system and available.

   ```Plain Text
   nvme list
   ```
   

   **Sample output**

   This topic takes the faulty disk `/dev/nvme0n1` as an example. The output shown below. If the relevant disk metrics are displayed normally, it means that the `/dev/nvme0n1` disk is present.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_501d066d7c7ca86c56810808ba8860ee.png) </span>

3. Execute the following command to check the health status, bad sector information, and other SMART data.

   > Replace `/dev/nvme0` with the name of the actual disk.   
   

   ```Plain Text
   smartctl -d nvme -a /dev/nvme0
   ```
   

   * **Sample output**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_43fe2c7ec30a67e0cfe0205bbe5cde85.png) </span>

   * **Parameter description**

      Pay attention to the following content of the output.

      
      |Parameter​ |No exception |Exception description |
      |---|---|---|
      |Critical Warning |0x00 |* 0x01 = available spare has fallen below threshold<br><br>* 0x02 = temperature is above or below threshold<br><br>* 0x04 = NVM subsystem reliability has been degraded<br><br>* 0x08 = media has been placed in read only mode<br><br>* 0x10 = volatile memory backup device has failed<br><br>* 0x1f = unknown critical warning(s) |
      |Error Information |No Errors Logged |`error`\-level errors are self\-correcting and can be ignored. |
      |Error Information Log Entries |0 |If there are more than 0 entries, the device has an exception. To view the exception details, check the returned information in the `Error Information` parameter. |
      

4. If no exception occurs during hardware detection, you can mount the hard disk.


<span id=".5q2l6aqk5LqU77ya5oyC6L2956Gs55uY"></span>
### Step 5: Mount the hard disk


1. After the hardware detection, you need to log in to the instance to mount the local volume.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance fails to identify the local volume after the faulty volume is replaced, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> for technical support.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you use UUID instead of device names (such as /dev/data1) for mounting.   </div>
   

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

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
