---
title: "Modifying RIs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

After you purchase an RI, if your business needs change, you can adjust the RI through the RI modification function. This feature allows you change the name, availability zone, instance type and number, associated project and tag, and auto\-renewal function of RI. The specific scenarios are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For ease of description, the RI to be changed is called the original RI, and the one obtained after change is the target RI.</div>



|Scenarios |Description |
|---|---|
|Change RI attribute |Such as change of the name, instance type, instance number. |
||You can change the availability zone of RI on the following occasions:<br><br><br>* You can change the availability zone within the same region of a zonal RI.<br><br>* You can change zonal RI to regional RI within the same region.<br><br>* You can change regional RI to zonal RI within the same region.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Accounts that have not enabled regional RIs can not change the availability zone attribute. Regional RI is currently in Beta. If you need a trial, contact your account manager to apply.</div><br> |
|Split RI |You can split one or more RIs into multiple RIs with less computing power. This allows you match them with pay\-as\-you\-go instances of the corresponding types and handle traffic distribution of your business. |
|Merge RI |If your business demand is concentrated, you can merge multiple RIs into one or more RIs with greater computing power. Therefore, you can match RIs with pay\-as\-you\-go instances of corresponding type. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The original RI must be **In effect**.

* Instances of original RI and the target RI must belong to the same instance family. And the original RI and the target RI must have the same expiration time.

* When you modify RI, the total computing power of the original RI and target RI must be the same. For information related to the normalization factor, refer to [Viewing normalization factor](https://docs.byteplus.com/en/docs/ecs/Check-normalization-factor).

* You can modify a maximum of 10 original RIs one time. The number of target RIs generated from the change must not exceed 50.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

**Some RIs do not support changing the instance type.** 

For RIs of certain instance families/types, you **can not** change their instance type. However, you can still change the number of instances and RIs. Those instance families/types are listed below:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For HPC\-optimized RIs, in addition to the number of both instances and RIs, you can also change the HPC Cluster that instances belong to.</div>


* <div data-tips="true" data-tips-type="tip">RIs that do not support instance type change and those that do, can not be converted between each other.</div>




|Instance type family |Instance type that does not support specification change |
|---|---|
|General\-purpose g2i |ecs.g2i.14xlarge |
|Local SSD i2 |All |
|Shared |ecs.s2\-c1m2.2xlarge |
|EBM |All |
|HPC\-optimized |All |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="KPKobpbJVs" title="Change RI attribute">
<TabTitle>Change RI attribute</TabTitle>

1. Log in to the [Offsetting resources console](https://console.byteplus.com/ecs/ri).

2. In the top menu bar, select the region and project of your business.

3. On the RI list page under the "Reserved instances" tab, click the "··· \> Modify Reserved Instances" button in the "Actions" column of the selected RI.

4. On the "Modify Reserved Instances" page, configure the target RI name, availability zone, instance type and number.

   You can click the "Add RI" button. You can add up to 10 original RIs one time. The RI to be added must match the selected RI in terms of region, instance type family, support for instance type modification, expiration time, and project.

5. Complete other configurations.

   * Tag/Project: The newly generated target RI is not associated with the same tag/project as the original RI. You can add a new tag/project to it. Once added, all target RIs generated this time are associated with the same tag/project.

   * Auto\-renewal: After you enable auto\-renewal function, the platform automatically deducts the renewal expenses before the expiration of all the target RIs generated this time. You don't need to manually renew them.

6. Click Confirm to complete the operation.


</Tab>
<Tab zoneid="iiOMpDKtxc" title="Split RI">
<TabTitle>Split RI</TabTitle>

1. Log in to the [Offsetting resources console](https://console.byteplus.com/ecs/ri).

2. In the top menu bar, select the region and project of your business.

3. On the RI list page under the "Reserved instances" tab, click the "··· \> Modify Reserved Instances" button in the "Actions" column of the selected RI.

4. On the "Modify Reserved Instances" page, confirm the information of the selected original RI.

   If you need to add multiple original RIs, you can click the "Add RI" button. You can add up to 10 original RIs one time.

5. Once you confirm all details, you can click the "Add Target RI" button, add them one by one and configure each accordingly. You can add up to 50 target RIs one time.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To split RI, the total computing power of the original RI and target RI must be the same.   </div>
   

6. Complete other configurations.

   * Tag/Project: The newly generated target RI is not associated with the same tag/project as the original RI. You can add a new tag/project to it. Once added, all target RIs generated this time are associated with the same tag/project.

   * Auto\-renewal: After you enable auto\-renewal function, the platform automatically deducts the renewal expenses before the expiration of all the target RIs generated this time. You don't need to manually renew them.

7. Click Confirm to complete the operation.


A sample of splitting RI is shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9455834110ff1dbcc2f10a4cb7dc86d.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_107df37e3f6bfe2aa8ba7121226637eb.png) </span>


</Tab>
<Tab zoneid="MrKFJwOym3" title="Merge RI">
<TabTitle>Merge RI</TabTitle>

1. Log in to the [Offsetting resources console](https://console.byteplus.com/ecs/ri).

2. In the top menu bar, select the region and project of your business.

3. On the RI list page under the "Reserved instances" tab, click the "··· \> Modify Reserved Instances" button in the "Actions" column of the selected RI.

4. On the "Modify Reserved Instances" page, confirm the information of the selected original RI.

   If you need to add multiple original coupons, you can click the "Add RI" button. You can add up to 10 original coupons in one operation.

5. Once you confirm all details, configure the name, instance type, and instance count of target RI.

   If you need to generate multiple target RIs, you can click the "Add Target RI" button, add them one by one and configure each accordingly.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The total computing power of the original RI and target RI must be the same for successful change.   </div>
   

6. Complete other configurations.

   * Tag/Project: The newly generated target RI is not associated with the same tag/project as the original RI. You can add a new tag/project to it. Once added, all target RIs generated this time are associated with the same tag/project.

   * Auto\-renewal: After you enable auto\-renewal function, the platform automatically deducts the renewal expenses before the expiration of all the target RIs generated this time. You don't need to manually renew them.

7. Click Confirm to complete the operation.


A sample of merging RIs is shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2ee5d62a1ee712a9a5fc3980f98b61c.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9ab457bcf58b2ec4938305ec8c9f940.png) </span>


</Tab>
</Tabs>


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results

After you split or merge RIs, the original RI enters the **Changing** status. The target RI appears with the status of **Creating**.


<Tabs>
<Tab zoneid="WnnsqpIFwZ" title="Success">
<TabTitle>Success</TabTitle>

* **Original RI**: It expires, and its expiration time is the same as the modification time. The remaining value on the original RI is allocated to the newly generated target RI .

* **Target RI**: It becomes **In effect**. Its creation time is the same as the modification time. The time it starts working and can be used for deductions is calculated on the hour. It expires at the same time as the original RI, and the type of reserved resources updates automatically. If the target RI matches the pay\-as\-you\-go instance, it begins to deduct the pay\-as\-you\-go bill at the same time.

* **Success example**

   Suppose at 13:35:00 on December 20, 2022, you successfully changed a zonal RI with the specification ecs.g2i.2xlarge (RI1) into two zonal RIs with the specification ecs.g2i.xlarge (RI2 and RI3),

   Then:

   RI1 would expire at 13:35:00 on December 20, 2022. It could only be used to offset hourly bills for ecs.g2i.2xlarge instances generated before 13:00:00 on December 20, 2022.

   RI2 and RI3 were also created at 13:35:00 on December 20, 2022. They could be used to offset hourly bills for ecs.g2i.xlarge instances from 13:00:00 on December 20, 2022 until they expired. Additionally, the resources they could offset and reserve would change from ecs.g2i.2xlarge to ecs.g2i.xlarge. If RI2 and RI3 successfully matched with an instance immediately after they took effect, they would start to deduct the hourly bill of the ecs.g2i.xlarge instance from December 20, 2022 13:00:00.


</Tab>
<Tab zoneid="E5uGRiZ9EG" title="Failure">
<TabTitle>Failure</TabTitle>

The original RI remains available, and the tag/project associated with it remains unchanged.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyReservedInstances - Changes Reserved Instances (RI)](https://docs.byteplus.com/en/docs/ecs/ModifyReservedInstances)
