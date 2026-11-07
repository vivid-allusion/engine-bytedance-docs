---
title: "Changing operating systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Changing-OS"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

Changing the operating system is an important means to reset the system volume and recover instances from system failures.


* When an existing instance encounters a system failure, you can change the operating system (that is, reset the system volume) to restore the instance to its initial status at startup.

* When the current operating system of an existing instance does not meet your business requirements, you can also change the operating system to meet business requirements.

   > You can change the operating system regardless of whether you change the operating system type. For example, you can change a Windows operating system to another Windows operating system. You can also change a Linux operating system to a Windows operating system.   
   

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also use the operating system migration feature of the SMC to change the CentOS operating system of an instance to the CentOS\-compatible veLinux operating system without downtime. <a href="https://docs.byteplus.com/en/docs/smc/Operating-System-Migration-Task">Learn more</a>.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Usage notes

Changing the operating system is a high\-risk operation that may cause prolonged business interruptions. Read the following precautions before you proceed.


|**Preparations** ||
|---|---|
|Stop instance |* Make sure that your ECS instance is in the **Stopped** status. Otherwise, data currently being written may be lost. If your instance has not been stopped yet, stop the instance by referring to [Stopping instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances?LibVersion=markdown备份版本).<br><br>* After you enable the "Economical Mode" feature for a pay\-as\-you\-go instance, the instance may fail to start as expected after the operating system is changed. |
|**Usage notes** ||
|Image selection |* We recommend that you use a public image provided by the platform to change the operating system. We recommend that you do not use images from unknown sources. Do not perform other actions when the operating system is being changed.<br><br>* To access instance metadata in **Security Hardening Mode**, select a custom image that supports Security Hardening Mode.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Accessing metadata in <strong>Security Hardening Mode</strong> is currently in Beta. If you want to have a trial,  contact your account manager.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can create a custom image that supports Security Hardening Mode. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images">Creating custom images</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Instance metadata contains the basic information of the ECS instance on the cloud platform. <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata">Learn more</a>.   </div><br>   <br><br>* If you select a whole image (custom image containing both the system volume and data volume), use only the system volume to change the operating system. Make sure that dependencies do not exist between the system volume and the data volume in your business design. If dependencies exist between the system volume and the data volume, make sure that the operations performed by the system volume on the data volume do not affect your business process after the system volume is changed. |
|Host name |After the Linux operating system is changed to a Windows operating system, the first 15 characters of the hostname are retained by default. |
|Network |The EIP address of the instance will not change after the operating system is changed. |
|Volume |* **System volume**:<br><br>   * After the operating system is changed, the system volume ID remains unchanged.<br><br>   * **The data in the system volume will be lost after the operating system is changed.**  Make sure that important information in the system volume is backed up by creating a custom image or snapshot in advance. [Learn more](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration).<br><br>* **Data Volume:** <br><br>   * After the operating system is changed, the data volume ID remains unchanged.<br><br>   * **Data in the data volume** ** will be retained after the operating system** ** is changed**.<br><br>   * After the Linux operating system is changed to another Linux operating system, you need to manually mount the data volume within the instance. [Learn more](https://docs.byteplus.com/en/docs/ecs/Changing-OS#yQk34fgJ).<br><br>   * After you change a Windows operating system to a Linux operating system or change a Linux operating system to a Windows operating system, the new operating system cannot identify the file system format of the original data volume. You must re\-initialize the data volume or install software to help the system identify the data volume. [Learn more](https://docs.byteplus.com/en/docs/ecs/Changing-OS#yQk34fgJ). |
|Local volume |After the operating system is changed, the data in the [local volume](https://docs.byteplus.com/en/docs/ecs/Local-volumes) (such as local NVMe SSD and SATA HDD) mounted on the instance is retained. |
|Protection |After the operating system is changed as follows, HIDS is disabled in the ECS console by default. . [Learn more](https://docs.byteplus.com/en/docs/ecs/Security-enhancement).<br><br><br>* Custom image changed to any other image.<br><br>* Public image changed to a custom image. |
|Metadata access method |After you change the operating system, the instance metadata access method remains unchanged.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the operating system is changed, you can call the <a href="https://docs.byteplus.com/en/docs/ecs/ModifyInstanceMetadataOptions">ModifyInstanceMetadataOptions</a> operation to adjust the instance metadata access method. For example,</div><br><br><br><div data-tips="true" data-tips-type="default">when the instance cannot start as expected because <strong>Security Hardening Mode</strong> is not supported by the image, you need to call the operation to change the instance metadata access method to <strong>Normal Mode</strong>.</div><br> |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can change the operating system of one or multiple existing instances at the same time to restore the system volume to the initial status.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you change the operating system of multiple existing instances at the same time, take note of the following items:</div>



* <div data-tips="true" data-tips-type="tip">The instances for which you want to change the operating system must remain in <strong>Stopped</strong> state, and their associated availability zones, images, and billing methods must be identical.</div>


* <div data-tips="true" data-tips-type="tip">You can change the operating system for up to 20 instances at the same time.</div>


* <div data-tips="true" data-tips-type="tip">You can log in to the instances for which you have changed the operating system at the same time by using the newly configured credentials.</div>


1. Log in to the [instance console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region and project where the target instance resides.

3. On the Instances page, click "Stop" in the "Actions" column of the target instance to stop the instance.

4. After the instance is stopped, click "... \> Volumes & Image \> Replace operating system" in the "Actions" column of the instance. Configure the parameters described in the following table.

   
   |Parameter​ |Description |
   |---|---|
   |Image |Public Image, Custom Image, Shared Images are supported. The current image type is selected by default. You can select the type of image that you want to use to change the operating system.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the custom image you select has any items that are strongly recommended to be fixed, click the "View details" button and follow the guidance to complete the fixes before you use the custom image. This helps prevent instance malfunctions caused by image issues. <a href="https://docs.byteplus.com/en/docs/ecs/Detect_item_description">Learn more</a></div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you use a custom image belonging to a project to change the operating system, your account must have permissions to perform operations on the project. Otherwise, you cannot use the custom image.</div><br> |
   |Login credentials |"Password", "Key pair", and "Keep Image settings" are supported. We recommend that you select "Key pair" for higher security.<br><br><br>* Password: If you select "Password", specify a complex password to enhance security.<br><br>* Key pair (recommended): A key pair consists of a public key and a private key. If you already have a key pair, select the name of the key pair to associate it. After association, you can log in to Linux instances with the private key. If you do not have a key pair, click the "Create key pair" button to go to the key pair page and create one.<br><br>* Keep Image settings: When you use a custom image or shared image, you can log in to the instance by using the preset credentials (password/key pair) in the image.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You cannot select "Key pair" for a Windows image.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you select "Keep image settings" for a Windows image, take note of the following items. Otherwise, you cannot log in to the instance by using the preset password of the image.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Before November 10, 2022, instances created by using Windows public images provided by the platform need to have their operating system or the Cloudbase\-init configuration files changed. The Cloudbase\-init configuration files of custom images or shared images generated by using the instances also need to be changed. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LiJ5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWRiYXNlLWluaXQ=">Installing Cloudbase\-init on virtual machine</a>.</div><br> |
   

5. Read the precautions for replacing the system volume and click the "Confirm the order" button to submit the request.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target instance is running a Linux operating system and the billing method is subscription, when you change the Linux operating system to a Windows operating system, you will be redirected to the order information confirmation page. On the order information confirmation page, you can confirm the new configuration information and choose whether to use a coupon to offset fees.   </div>
   

<span id=".5pON5L2c57uT5p6c"></span>
## Operation results


* Successful: After you submit the request for changing the operating system, the instance changes to the **Rebuilding** status. Approximately 10 minutes later, the operating system is changed, the instance automatically starts, and the status changes to **Running**. Billing is resumed for instances in economical mode. Click the instance name to go to the instance details page, on which the new image is displayed.

* Failed: The status changes from **Rebuilding** to **Stopped**. The instance will roll back to the pre\-failure status and remain in the shutdown status. Please retry or contact customer service for assistance.


<span id="yQk34fgJ"></span>
## Subsequent operations

After you change the operating system, you must perform the following operations before the data disk can be used as expected.


<Tabs>
<Tab zoneid="S9rpxRC8Ic" title="Switch between Linux operating systems">
<TabTitle>Switch between Linux operating systems</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view information about unmounted data volumes.

   ```Plain Text
   lsblk
   ```
   

   If the following result is displayed, the original data volume `vdb` (this volume contains one partition `vdb1`) is not mounted.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_444e28dd7ebf8f7c7c690f9f15a15340.png) </span>

3. Execute the following command to create a mount point.

   ```Plain Text
   sudo mkdir /data
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/data</code> with the name of the target mount point.   </div>
   

4. Execute the following command to mount the data volume to the target mount point.

   ```Plain Text
   sudo mount /dev/vdb1 /data/
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/dev/vdb1</code> with the name of the target data volume partition.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/data/</code> with the name of the target mount point.   </div>
   

5. Configure automatic mounting.

   1. Execute the following command to query the UUID of the partition.

      ```Plain Text
      sudo blkid /dev/vdb1
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please replace <code>/dev/vdb1</code> with the target data disk partition name.      </div>
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60f1c71cde4508bd12d8c86deb57d35c.png) </span>

   2. Run the following command to open the /etc/fstab file.

      ```Plain Text
      vim /etc/fstab
      ```
      

   3. Press the`i`key to enter edit mode and add the following content at the end.

      ```Plain Text
      UUID=9439749e-8d07-4ce2-9591-xxxxxbc9 /data ext4 defaults 0 0
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>9439749e-8d07-4ce2-9591-xxxxxbc9</code> with the actual UUID of the target volume partition.      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>/data</code> with the actual mount point name for the target volume partition.      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>ext4</code> with the actual file system format of the target volume partition.      </div>
      

   4. Press the `esc` key to exit editing, enter `:wq`, and press Enter to save and exit the file.


</Tab>
<Tab zoneid="VU2U33KE47" title="Switch between Windows and Linux operating systems">
<TabTitle>Switch between Windows and Linux operating systems</TabTitle>

* After the Linux operating system is changed to a Windows operating system, the Windows operating system cannot recognize file system formats such as ext3, ext4, and XFS by default.

   * If your data volume contains important data, you can install software (such as Ext2Read or Ext2Fsd) to recognize the data volume and obtain the data.

   * If your data volume does not contain important data, we recommend that you [re-initialize the data volume](https://docs.byteplus.com/en/docs/ecs/Reinitialize-volume) and then [partition and format the volume (Windows)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-larger-than-2-TiB) so that the data volume can be used as expected.

* After the Windows operating system is changed to a Linux operating system, the Linux operating system cannot recognize the NTFS file system format by default.

   * If your data volume contains important data, you can install software (such as ntfsprogs) to recognize the data volume and retrieve the data.

   * If your data volume does not contain important data, we recommend that you [re-initialize the data volume](https://docs.byteplus.com/en/docs/ecs/Reinitialize-volume) and then [partition and format the volume (Linux)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB) so that the data volume can be used as expected.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ReplaceSystemVolume](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume)
