---
title: "Attaching a volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Attach-a-volume"
---

You can attach available data volumes to ECS instances. This topic explains how to do so.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For instructions on how to automatically mount your volumes on boot, see <a href="https://docs.byteplus.com/en/docs/ecs/Allowing-disk-partitions-to-be-automatically-mounted-during-restarts">Setting up automatic mounting of volume partitions upon boot</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Attach operations are only available for pay\-as\-you\-go data volumes. They can be attached to either pay\-as\-you\-go or subscription instances.

* You can only attach a volume to an instance within the same availability zone.

* You can attach data volumes either online or offline. The target instance's status must be "Running" or "Stopped".

* The target volume must be in the "Available" status and must be a data volume.

* Your account must have no outstanding balance and must not be more than two hours overdue.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Different instance types support different types of volumes. You cannot attach an ESSD and a PTSSD volume to the same instance at the same time. For more information, see [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* You can only attach a volume to an instance within the same availability zone. Once you have attached the volume, you cannot change the availability zone.


<span id=".5Zyo5a6e5L6L6aG16Z2i5oyC6L29"></span>
## Attaching volumes from the Instances page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region where the instance resides.

4. On the "Instances" page, use one of the following methods to access the "Attach Volume" page.

   * Select "··· \> Volumes & Image \> Attach volumes" in the "Actions" column of the instance.

   * Click the name of the instance to access its details page. Then, select the "Volumes" tab and click "Attach" in the upper\-left corner of the page.

5. Select the desired volume and choose whether to enable the "Delete with instance" feature, which is disabled by default.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you enable "Delete with instance" and delete the instance, all data on the attached data volume will be deleted and billing will stop.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not select "Delete with instance" and then delete the instance, how the system handles the data on the attached data volume depends on the instance's billing method. If the instance adopts the pay\-as\-you\-go billing method, the data volume is automatically detached and retained, and billing continues. If the instance is subscription\-based, the data volume is deleted with the instance.   </div>
   

6. Click "Attach" to attach the new data volume to the instance.

7. If you are attaching a newly created volume, refer to [Partitioning and formatting a volume](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview) to learn how to partition and format it with a file system before you can use it.

   A successfully attached volume will appear on the "Volumes" tab of the instance details page.


<span id=".5Zyo5LqR55uY5YiX6KGo6aG16Z2i5oyC6L29"></span>
## Attaching volumes from the Volumes page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region in which you want to create a volume.

4. On the "Volumes" page, select the desired volume and click "Attach" in the lower\-left corner.

5. In the "Attach Volume" panel, select the instance to which you want to attach the volume.

6. Choose whether to enable the "Delete with instance" feature, which is disabled by default.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you enable "Delete with instance" and delete the instance, all data on the attached data volume will be deleted and billing will stop.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not select "Delete with instance" and then delete the instance, how the system handles the data on the attached data volume depends on the instance's billing method. If the instance adopts the pay\-as\-you\-go billing method, the data volume is automatically detached and retained, and billing continues. If the instance is subscription\-based, the data volume is deleted with the instance.   </div>
   

7. Click "Attach" to attach the data volume to the instance.

8. If you are attaching a newly created volume, refer to [Partitioning and formatting a volume](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview) to learn how to partition and format it with a file system before you can use it.

   After a successful attachment, you can view the instance to which the volume is attached in the "Instances" column on the "Volumes" page.
