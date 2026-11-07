---
title: "Method 2: Resolve local volume failures through instance redeployment"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Redeploying-instances"
---

This topic describes how to redeploy an instance when a local volume failure event occurs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you redeploy the instance, all data on the original local volumes of the instance (both faulty and non\-faulty volumes mounted to the instance) will be lost. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">If you need to redeploy the instance, back up local volume data in advance. You can back up data using <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh">volumes</a>, <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh">TOS</a>, or other methods.</div>



<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When you receive a DiskErrorDetected (disk exception) event, you can authorize BytePlus to migrate the instance to another host to restore normal operations of the instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This feature is only available for instances of the Big Data, Local SSD, EBM, and Heterogeneous Compute\-optimized types that are mounted with local volumes. For details, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* Please follow the [procedure](https://docs.byteplus.com/en/docs/ecs/Redeploying-instances#.5pON5L2c5q2l6aqk) to remove the partition information of the local data volume first before you authorize O&M operations. Otherwise, the redeployed instance may fail to restart.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the ECS instance where the faulty volume is mounted. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to edit the /etc/fstab file.

   1. Open the /etc/fstab file.

      ```Plain Text
        vim /etc/fstab
      ```
      

   2. Press the `i` key to enter edit mode, and add the `nofail` parameter after the target local volume in the file.

      > Only the `nofail` parameter needs to be added and no other content requires adjustment.      
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29d13830ebee801744cce4f7830cfd2e.png) </span>

      **Description of fstab file arguments**

      <mark>
      |Parameter​ |Description |
      |---|---|
      |bf734ac7\-0328\-4e7f\-8ada\-ca09\*\*\*\* |The UUID of the faulty local volume. |
      |/ |The mount point of the faulty local volume. |
      |ext4 |The file system type of the faulty local volume. |
      |nofail |When a local volume appears in the file system but is actually missing, this parameter does not interrupt the ECS instance startup process. |
      </mark>

3. Press `Esc` and enter `:wq` to save the change and exit the file.

4. After modifying the /etc/fstab file, you can continue the instance redeployment.

5. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

6. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events" to go to the Events page.

7. In the top menu bar, select the region and project of your business.

8. On the Events page, you can search the disk exception event based on the time range, event ID, or instance ID.

10. Click the "Maintenance operation" button in the "Actions" column of the target event to go to the maintenance configuration page.

   > After authorization, BytePlus generates a DiskError.Redeploy (Redeployment for unhealthy instances) event to synchronize your instance redeployment progress.   
   

   1. Select "Redeploy instance" for "Operation and maintenance method".

   2. Click the "Authorize maintenance" button.

   3. In the pop\-up window, select the desired time for instance redeployment.

11. After the instance is redeployed, BytePlus sends you a DiskError.Redeploy:Succeeded (Redeployment for unhealthy instances) event. This means that the instance redeployment succeeds. After receiving the notification, you need to log in to the instance to mount the local volume.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance fails to identify the local volume after the instance is redeployed, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> for technical support.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you use device names (such as /dev/data1) instead of UUID for mounting.   </div>
   

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

   2. Execute the following command to view information about unmounted data volumes.

      ```Plain Text
      lsblk -l
      ```
      

   3. Execute the following command to create a file system for the data volume to be mounted.

      ```Plain Text
      mkfs -t <File System> <Device Name>
      ```
      

   4. Execute the following command to mount the data volume.

      ```Plain Text
      mount <Device Name> <Mount Point>
      ```
      

12. Execute the following command to check whether the data volume is mounted.

   ```Plain Text
   lsblk -l
   ```
