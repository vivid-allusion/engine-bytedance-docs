---
title: "Modifying volume attributes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modify-volume-attribute"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Use cases

You can modify the attributes of a volume, including its name, description, behavior, and delete protection settings.

<span id=".6ZmQ5Yi25p2h5Lu2"></span>
## Restrictions


* You can only modify the attributes of pay\-as\-you\-go data volumes.

* The behavior setting, i.e., whether or not the volume is deleted when the instance is deleted, only applies to volumes that are attached to an ECS instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, click "... \> Modify attributes" in the "Actions" column of the volume.

5. In the "Modify volume attributes" dialog, perform the following operations if necessary: change the volume name and description; check the box that says, "The volume is deleted along with the instance"; or enable "Delete protection".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only select the "delete with instance" option for volumes attached to ECS instances.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Selecting "delete with instance" will delete all data on the data volume and stop billing when the instance is deleted (pay\-as\-you\-go) or expires (subscription).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not select "delete with instance" and the instance is subsequently deleted or expires, how the system handles the data volume depends on the instance's billing method. If the instance adopts the pay\-as\-you\-go billing method, the data volume is automatically released and retained, and billing continues. If the instance is subscription\-based, the data volume is deleted with the instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Even after setting the "delete with instance" attribute for a volume, you can still change it when deleting the instance — for example, from enabled to disabled or vice versa. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">Deleting instance</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, snapshot data with delete protection is retained permanently. However, you can set a retention period ranging from 1 to 65,536 days. The default period is 30 days. After this period, snapshots are automatically deleted. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Delete-volume?lang=en">Deleting a volume</a>.   </div>
   

6. Click "Save" to save the changes.
