---
title: "Creating a volume from a snapshot"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create-a-volume-through-snapshot"
---

You can create a volume from an existing snapshot to copy the snapshot data to the new volume.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


|Category |Considerations |
|---|---|
|Availability zones |You can only attach a volume to an instance within the same availability zone. After creating a volume, you cannot change its zone. Make sure you select the correct zone when creating the volume. |
|Deleting snapshots |You cannot delete the snapshot while a new volume is being created from it. |
|Volume UUIDs |When you create a volume from a snapshot, the new volume's UUID is the same as the source volume's. Attempting to attach the new volume to the same instance to which the source volume is attached will result in a UUID conflict. This may cause the following issue: When using a system volume snapshot, if you attach the new volume to the same Linux instance that originally had the system volume, Linux may boot from the newly attached data volume instead of the original system volume. |
|Constraints and limitations |* The volumes discussed in this topic are all data volumes. System volumes are automatically created and attached when instances are created, and cannot be created independently.<br><br>* When creating a volume from a snapshot, you can only select "ESSD" as the volume type.<br><br>* You can only use snapshots that are in the "Available" status to create volumes. |


<span id=".5Zyo5Yib5bu65a6e5L6L5pe25Yib5bu65LqR55uY"></span>
## Creating a volume when creating an instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you create a volume while creating an ECS instance, the volume will automatically use the same billing method as the instance.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region where the snapshot resides.

4. Select "Create instance \> Custom purchase".

6. On the "Basic configuration" page, click "Add data volume" under "Storage". Then, configure the following parameters:

   * Type: Select "ESSD".

   * Performance level: Select the desired performance level. For more information about performance, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).

   * Capacity: Set the capacity as needed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The capacity of the new volume must be equal to or greater than that of the snapshot.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the two capacities are the same, you can attach and use the new volume directly after creation without taking any extra steps.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the new volume's capacity is larger than the snapshot's, you must repartition it to use the extra space.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the snapshot is smaller than 2 TiB but you need a volume larger than 2 TiB, make sure that the volume from which the snapshot was taken uses the GPT partitioning scheme. If it uses MBR, you must repartition and reformat the new volume, which will erase your data. Choose the capacity for the new volume carefully.   </div>
   

   * Delete with instance: This option is available for pay\-as\-you\-go volumes. By default, the volume is deleted with the instance.

   * Snapshot: Click "Create cloud disk with snapshots". Then, select the desired snapshot in the box that appears.

   After configuring the above parameters, follow the wizard to complete the "Basic configuration", "Network configuration", and "Custom configuration" steps in that order. For more information on the other parameters, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

6. After verifying the configuration on the "Confirm" page, check the box that says "I have read and agree with Elastic Compute Service Terms of Service", and click "Buy Now" to submit your order.


<span id=".5Zyo5LqR55uY5YiX6KGo5Yib5bu65LqR55uY"></span>
## Creating a volume from the Volumes page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the snapshot resides.

4. On the "Volumes" tab, click "Create volume".

5. On the "Create volume" page, configure the following parameters:



|Parameter |Description |
|---|---|
|Whether to attach |Select whether to attach your volume to an instance at the time of creation.<br><br><br>* Do not attach for now: This option creates a volume separately and does not attach it to an instance. Currently, only pay\-as\-you\-go volumes are supported.<br><br>* Attach to ECS instance: This option creates a volume and attaches it to the specified instance. After selecting this option, specify the corresponding availability zone and instance under "ECS instance".<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To create a subscription volume, select "Attach to ECS instance" and choose the corresponding subscription instance under "ECS instance". The feature for creating subscription volumes is in closed beta. Please contact your account manager for access.</div><br> |
|Region and availability zone |After selecting "Do not attach for now", choose the region and availability zone where you want to create the volume.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The new volume must be created in the same region as the snapshot.</div><br> |
|ECS instance |After selecting "Attach to ECS instance", choose the instance to which you want to attach your volume. In the "Instance details" section, you can view details of the instance, including the region and availability zone, billing type and instance specification. |
|Billing type |Select a billing method for your volume. Options:<br><br><br>* Pay\-as\-you\-go: A post\-paid option. You are charged for the time you actually use, on an hourly basis. You can create or delete pay\-as\-you\-go volumes at any time. After creation, the volume can be attached to a pay\-as\-you\-go or subscription instance.<br><br>* Subscription: A pre\-paid model where you pay first and use resources later. The subscription duration is measured in months. A subscription volume can only be attached to a subscription instance and will expire when the instance expires. |
|Delete with instance |You can select this option when creating a pay\-as\-you\-go volume and attaching it to an instance. The volume will not be deleted with the instance by default. |
|Storage |Select "ESSD" and set the capacity.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating a volume from a snapshot, you cannot select "PTSSD" as the volume type.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The capacity of the new volume must be equal to or greater than that of the snapshot. Specifically:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the two capacities are the same, you can attach and use the new volume directly after creation without taking any extra steps.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the new volume's capacity is larger than the snapshot's, you must repartition it to use the extra space.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">If the snapshot is smaller than 2 TiB but you need a volume larger than 2 TiB, make sure that the volume from which the snapshot was taken uses the GPT partitioning scheme. If it uses MBR, you must repartition and reformat the new volume, which will erase your data. Choose the capacity for the new volume carefully.      </div><br>       |
|Data source |Click "Create from snapshot". Then, select the desired snapshot in the box that appears, and click "OK". |
|Quantity |Select the number of volumes you want to create from the snapshot. The valid range is 1 to 100. |
|Name |Enter a name for your volume. The volume name must:<br><br><br>* Start with a Chinese character, a letter or an underscore (_).<br><br>* Contain only Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating volumes in batches, the system automatically adds an ordered suffix to the name of each volume. For example, if you create two volumes and name them "disk", they will be named "disk\-1" and "disk\-2".</div><br> |
|Description |Provide additional information about your volume. The description must:<br><br><br>* Start with a Chinese character, a letter or an underscore (_).<br><br>* Contain only Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 0 and 255 characters long. |
|Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources by purpose, owner, environment, and other criteria for easy searching and aggregation.<br><br>To add a tag to a volume, click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon and enter the tag key and value. For more information, see [Tag management](https://docs.byteplus.com/docs/ecs/Tag-overview). |
|Project |(Optional) Select the project to which your volume belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that comprises a set of resources, users, and roles. It provides a unified view of and access to resources, as well as control over user and role permissions within the project. </div><br><br><br>* <div data-tips="true" data-tips-type="tip">To create a project, click "Create new projects" on the right. This will take you to the <a href="https://console.byteplus.com/iam/resourcemanage/project">IAM console</a>.</div><br> |



6. Click "Confirm order".

7. After confirming that the volume configuration and number of volumes are correct, as well as the associated costs, check the box that says, "I have read and agree to the Elastic Compute Service Terms of Service". Then, click "Create volume" to submit your order.
