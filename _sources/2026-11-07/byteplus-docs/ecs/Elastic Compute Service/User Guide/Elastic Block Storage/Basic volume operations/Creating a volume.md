---
title: "Creating a volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create-a-volume"
---

You can create volumes for ECS instances on either a pay\-as\-you\-go or subscription basis. This topic explains how to create a volume.

<span id="pR7YYmXx"></span>
## Prerequisites

Before creating a volume, make sure that you have made the necessary [preparations](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances#).

<span id="IQPBf9ZW"></span>
## Restrictions on subscription volumes


* When creating a subscription volume, you must attach it to an instance that uses the same billing method. Additionally, the volume's expiration date matches that of the instance. Before you begin, make sure that you have created a subscription instance. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* If the instance expires in less than one month, the subscription volume is billed at a daily rate (monthly price ÷ 365 ÷ 12) multiplied by the number of remaining days, rather than using pay\-as\-you\-go pricing. For example, if the subscription instance to which the volume is attached will expire in seven days, the subscription volume billing is calculated as follows: Monthly price ÷ (365 ÷ 12) × 7 days.


<span id="RVhgHfTh"></span>
## Notes


* The volumes discussed in this topic are all data volumes. System volumes are automatically created and attached when instances are created, and cannot be created independently.

* You can only attach a volume to an instance within the same availability zone. After creating a volume, you cannot change its zone. Make sure you select the correct zone when creating the volume.

* After creating a volume, you cannot change its type. Select the appropriate volume type based on your needs and instance type. For more information, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).

* When creating a pay\-as\-you\-go volume, you have the option of leaving it unattached or attaching it directly to an instance. You can attach pay\-as\-you\-go volumes to pay\-as\-you\-go or subscription instances.

* When creating a pay\-as\-you\-go volume, you can choose to attach it to a pay\-as\-you\-go or subscription instance. You can also select an option to delete the volume when the instance is deleted. By default, the volume will not be deleted with the instance.


<span id="9LsaS2nI"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region in which you want to create a volume.

4. Click "Create volume". On the "Create volume" page, configure the following parameters.

&nbsp;

   
   |Parameter |Description |
   |---|---|
   |Whether to attach |Select whether to attach your volume to an instance at the time of creation.<br><br><br>* Do not attach for now: This option creates a volume separately and does not attach it to an instance. Currently, only pay\-as\-you\-go volumes are supported.<br><br>* Attach to ECS instance: This option creates a volume and attaches it to the specified instance. After selecting this option, specify the corresponding availability zone and instance under "ECS instance".<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To create a subscription volume, select "Attach to ECS instance" and choose the corresponding subscription instance under "ECS instance".</div><br> |
   |Region and availability zone |After selecting "Do not attach for now", choose the region and availability zone where you want to create the volume.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After you create a volume, you cannot change its region and availability zone. Select the same region and availability zone as the instance to which you want to attach the volume.</div><br> |
   |ECS instance |After selecting "Attach to ECS instance", choose the instance to which you want to attach your volume. In the "Instance details" section, you can view details of the instance, including the region and availability zone, billing type and instance specification. |
   |Billing type |Select a billing method for your volume. Options:<br><br><br>* Pay\-as\-you\-go: A post\-paid option. You are charged for the time you actually use, on an hourly basis. You can create or delete pay\-as\-you\-go volumes at any time. After creation, the volume can be attached to a pay\-as\-you\-go or subscription instance.<br><br>* Subscription: A pre\-paid model where you pay first and use resources later. The subscription duration is measured in months. A subscription volume can only be attached to a subscription instance and will expire when the instance expires. |
   |Delete with instance |You can select this option when creating a pay\-as\-you\-go volume and attaching it to an instance. The volume will not be deleted with the instance by default. |
   |Storage |Specify the type and size of your volume. For a list of supported volume types and their specifications, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications). |
   |Data source |To create a volume from a snapshot, click "Create from snapshot". Then, select the target snapshot in the box that appears, and click "OK". |
   |Quantity |Select the number of volumes that you want to create. The valid range is 1 to 100.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For pay\-as\-you\-go volumes, the total capacity is limited. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Limits#.5LqR55uY">Volume limits</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For subscription volumes, the number of volumes that can be attached to different instance types is limited. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div><br> |
   |Name |(Optional) Enter a name for your volume. The volume name must:<br><br><br>* Start with a Chinese character, a letter or an underscore (_).<br><br>* Contain only Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
   |Description |(Optional) Provide additional information about your volume. The description must:<br><br><br>* Start with a Chinese character, a letter or an underscore (_).<br><br>* Contain only Chinese characters, letters, numbers, underscores (_), or hyphens (\-).<br><br>* Be between 0 and 255 characters long.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating volumes in batches, the system automatically adds an ordered suffix to the name of each volume. For example, if you create two volumes and name them "disk", they will be named "disk\-1" and "disk\-2".</div><br> |
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources by purpose, owner, environment, and other criteria for easy searching and aggregation.<br><br>To add a tag to a volume, click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon and enter the tag key and value. For more information, see [Tag overview](https://docs.byteplus.com/docs/ecs/Tag-overview). |
   |Project |(Optional) Select the project to which your volume belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that comprises a set of resources, users, and roles. It provides a unified view of and access to resources, as well as control over user and role permissions within the project. </div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is no suitable project, click "Create new projects" on the right to go to the <a href="https://console.byteplus.com/iam/resourcemanage/project">IAM console</a> and create a new one.</div><br> |
   |Delete protection |By default, snapshot data with delete protection is retained permanently. However, you can set a retention period ranging from 1 to 65,536 days. The default period is 30 days. After this period, snapshots are automatically deleted. For more information, see [Deleting a volume](https://docs.byteplus.com/en/docs/ecs/Delete-volume?lang=zh).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When a protected volume is deleted, the system automatically creates a snapshot within seconds. During the snapshot dump process, which takes minutes or hours, the volume will remain in the "Deleting" state and stop billing. You can check the status of the volume by its ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Delete protection is only available for volumes that support snapshots. It is not available for elastic remote volumes, PTSSD volumes, or volumes attached to multiple instances.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A snapshot is automatically created to back up the data when a protected volume is deleted, and <a href="https://docs.byteplus.com/en/docs/ecs/Snapshot_billing">snapshot charges</a> will be incurred.</div><br> |
   |Placement group |Select a storage placement group.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For an introduction to storage placement groups, see <a href="https://docs.byteplus.com/en/docs/ecs/Manage-placement-group">Managing placement groups</a>.</div><br> |
   |Child placement group |Select a child placement group number. The system deploys volumes with different child placement group numbers across different clusters, depending on metrics such as cluster health and load.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each child placement group can host up to 200 volumes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Once a volume is bound to a child placement group, the binding cannot be changed.</div><br> |
   

5. After you have finished configuring, click "Confirm order".

6. After confirming that everything is correct, check the box that says, "I have read and agree to the Elastic Compute Service Terms of Service".

7. Click "Create volume" to submit your order. You will then be redirected to a page where you can check if the volume was created successfully.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the creation is complete, you can click "Go to console". The page will automatically redirect to the volume list page, where you can view information about the newly created volumes, including the volume ID, status, and <a href="https://docs.byteplus.com/en/docs/ecs/Tag-overview#.5qCH562-57G75Z6L">tags</a>.   </div>
   

<span id="W1UYQO0S"></span>
## Next steps

After creating a volume, perform the following operations before using the volume.


* If you select "Do not attach for now" when creating the volume: Afterwards, you must attach the volume to an instance and format its partitions. For more information, see [Attaching a volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume) and [Partitioning and formatting a volume](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview).

* If you select "Attach to ECS instance" when creating the volume: Afterwards, you must format the volume partitions. For more information, see [Partitioning and formatting a volume](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview).


<span id="bEWajksW"></span>
## Related documentation

You can also create and attach a volume when creating an instance, or create a volume from a snapshot.


* [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances)

* [Creating a volume from a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-volume-through-snapshot)
