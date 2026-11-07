---
title: "Deleting a volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delete-volume"
---

You can delete unused volumes to save resources and costs. If you want to keep your data after deleting a volume, you can use the deletion protection feature. This feature automatically creates a snapshot when a volume is deleted, adding an extra layer of protection. This topic explains how to manually delete a volume and enable deletion protection.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* In the console, you can only manually delete a pay\-as\-you\-go volume that is in the "Available" state. This means that the volume is not currently attached to an ECS instance.

* If you prefer not to manually delete a pay\-as\-you\-go volume, you can configure it to be deleted automatically when the instance is deleted. You can enable "delete with instance" in the following ways

   * When creating an ECS instance, select the “delete with instance” option. For instructions, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * When attaching a volume, check the box that says, "The volume is deleted along with the instance". For instructions, see [Attaching a volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

   * When modifying a volume's attributes, check the box that says, "The volume is deleted along with the instance". For instructions, see [Modifying volume attributes](https://docs.byteplus.com/en/docs/ecs/Modify-volume-attribute).

   * When deleting an instance, select the volumes you want to delete. For instructions, see [Deleting instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances).

* Delete protection is only available for volumes that support snapshots. It is not available for elastic remote volumes, PTSSD volumes, or volumes attached to multiple instances.

* Any associated manual snapshots are retained after a volume is deleted. If you no longer need them, you can delete the snapshots yourself.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deleting an instance will also delete the associated system volume. If your instance is shut down due to expiration, an overdue payment, or cancellation, the system volume will enter a retention period. It will be retained for 15 days by default, during which time you will not be billed. The volume is automatically deleted when the retention period ends.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Delete protection

Delete protection is a feature that prevents the accidental deletion of data. When enabled, the system automatically creates a snapshot of the volume before deleting it. This snapshot can then be used to create a new volume and restore the original data. This effectively prevents permanent data loss due to accidental actions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When a protected volume is deleted, the system automatically creates a snapshot within seconds. During the snapshot dump process, which takes minutes or hours, the volume will remain in the "Deleting" state and stop billing. You can check the status of the volume by its ID.</div>


<span id="KOu3DwwZ"></span>
## Configuring delete protection

You can enable, disable, or modify delete protection when creating a volume or for an existing volume.


* To enable deletion protection when creating a volume: On the [Create volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume) page, enable "Delete protection" and specify the number of days to retain the snapshot.

* To enable deletion protection for an existing volume: On the "Volumes" page, use the "Modify attributes" action to enable or disable delete protection and adjust snapshot retention.


By default, snapshot data with delete protection is retained permanently. However, you can set a retention period ranging from 1 to 65,536 days. The default period is 30 days. After this period, snapshots are automatically deleted.

<span id="mgu3IYAb"></span>
## Deleting a volume


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, select the desired volume and click "Delete" in the lower\-left corner of the page.

5. In the box that appears, confirm the deletion by clicking "Delete".

   If the deletion is successful, the volume will disappear from the volume list.
