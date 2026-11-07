---
title: "Step 1: Isolate the local volume (optional)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Isolating-local-volumes"
---

This topic describes how to isolate a faulty local volume when a local volume failure event occurs.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

When you receive a DiskErrorDetected (disk exception) event, if you directly authorize BytePlus to replace the disk, your application will keep reading from and writing to the faulty local volume during processing. We recommend that you first isolate the faulty volume, make sure applications that run on the instance stop reading from and writing to the volume, then authorize BytePlus to replace the disk. This can help you to minimize data loss.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Currently, you can only isolate faulty volumes associated with Linux instances.

* This feature is only available for the following instance type families:

   
   |System architecture |Instance type families |
   |---|---|
   |x86 |* Big data<br><br>   * [Big Data d2c](https://docs.byteplus.com/en/docs/ecs/Big-data-based)<br><br>* Local SSD<br><br>   * [Local SSD i3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#8IH6RHiz) |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="EUCIfXgW"></span>
### Step 1: Obtain the serial number of the faulty hard disk

When a local volume mounted to an instance fails, BytePlus will synchronize the serial number (SN) of the faulty hard disk with you. Therefore, you can locate the faulty hard disk for the instance accurately and easily. You can call the [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation, pass in the event ID of the hard disk exception, and obtain the SN of the faulty hard disk from the returned data.


* If the instance with the faulty hard disk is a first\-generation HDD instance (for example, Big Data Storage\-optimized d1s), the value of the `SystemEvents.ExtraInfo.Address` parameter in the returned data is the SN of the faulty hard disk.

* If the instance with the faulty hard disk is a second\-generation HDD instance (for example, Big Data d2s, Big Data d2c, and Big Data d2), or an instance of Local SSD type (for example, Local SSD i2), the value of the `SystemEvents.ExtraInfo.Serial` parameter in the returned data is the SN of the faulty hard disk.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For ease of use, we recommend that you record the obtained SN of the faulty disk. This is because you need to use the SN for "Step 2: Check the drive letter of the faulty local volume<strong>"</strong>.</div>


<span id="zJwkDtZK"></span>
### **Step 2: Check the drive letter of the faulty local volume**

You can view the drive letter of the faulty local volume to quickly locate the storage zone where the volume failure occurs.


1. Log in to the ECS instance where the faulty volume is mounted. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to view the drive letter of the faulty local volume.

   * First\-generation HDD instance

      If your instance is a first\-generation HDD instance (for example, Big Data Storage\-optimized d1s), execute the following command to view the drive letter of the faulty hard disk.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

Replace `$SN$` with the actual SN of the faulty hard disk.


```Plain Text
ls -al /dev/disk/by-path/ | grep $SN$
```


   * Second\-generation HDD or Local SSD instance

      If your instance is a second\-generation HDD instance (for example, Big Data d2s, Big Data d2c, and Big Data d2), or an instance of Local SSD type (for example, Local SSD i2), execute the following command to view the drive letter of the faulty hard disk.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

Replace `$SN$` with the actual SN of the faulty hard disk.


```Plain Text
lsblk -oNAME,SERIAL | grep $SN$
```



<span id="utZUGQFF"></span>
### Step 3: View the mount point, file system, and UUID of the faulty local volume


1. Execute the following command to check the mount point of the faulty local volume. This example uses the faulty local volume "/dev/vda2".

   ```Plain Text
   df -h
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For ease of use, we recommend that you record the obtained mount point of the faulty local volume. This is because you need to use the mount point for "<strong>Step 4: Edit /etc/fstab file</strong>".   </div>
   

2. Execute the following command to view the file system and UUID of the faulty local volume.

   ```Plain Text
   blkid /dev/vda2
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For ease of use, we recommend that you record the obtained file system and UUID of the faulty local volume. This is because you need to use them in <strong>"Step 4: Edit /etc/fstab file"</strong>.   </div>
   

<span id="Gr0wwZ5T"></span>
### Step 4: Edit /etc/fstab file


1. Execute the following command to edit the /etc/fstab file.

   ```Plain Text
   vim /etc/fstab
   ```
   

2. Press the `i` key to add the `nofail` parameter after the target local volume in the file.

   > Only the `nofail` parameter needs to be added and no other content requires adjustment.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ceb854f5dfa34cd3a833990af84e673.png) </span>

   **Description of fstab file arguments**

   
   |Parameter​ |Description |
   |---|---|
   |24fd1325\-bbf3\-4814\-b7e9\-041deba\*\*\*\*\* |File system UUID. |
   |/ |The mount point of the faulty local volume. |
   |ext4 |The file system type of the faulty local volume. |
   |nofail |If a local volume is present in the file system but actually missing, this parameter will not interrupt the ECS instance startup process. |
   

3. Press `Esc` and enter `:wq` to save the change and exit.


<span id="olS3aaHB"></span>
### Step 5: Cancel the faulty local disk mount

Execute the following command to cancel mounting the faulty local volume.

```JSON
unmount /dev/vda2
```


<span id="oMuh64fd"></span>
### Step 6: Isolate the faulty volume


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the resource that has triggered the event.

4. Find the target instance, and click the instance name to go to the instance details page.

5. Click the "System Events" tab, here you can filter event information based on a time range or event ID and take actions.

6. In the "Actions" column of the target event, select "Maintenance operation \> Isolate the fault disk" to authorize BytePlus to isolate the faulty volume.

   > The isolation process may take several minutes. If it takes too long to complete, try refreshing the page.   
   

7. After isolation is complete, you can hover your mouse over the "Isolate the fault disk" button.

   * If the **Isolated** state occurs, it means that the isolation succeeds.

   * If error feedback occurs, it means that the isolation fails.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operation

After isolation is complete, you can select "Maintenance operation \> Authorize maintenance" in the "Actions" column. Then, select the "Replace the faulty volume" to authorize and notify the O&M personnel of the BytePlus for maintenance. For details, refer to [Replacing faulty volumes](https://docs.byteplus.com/en/docs/ecs/Replacing-faulty-volumes). 

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents)
