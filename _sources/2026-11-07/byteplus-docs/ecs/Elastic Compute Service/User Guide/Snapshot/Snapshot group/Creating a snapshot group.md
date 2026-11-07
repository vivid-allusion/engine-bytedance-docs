---
title: "Creating a snapshot group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot-consistency-group"
---

A snapshot group is a collection of snapshots from multiple volumes. Snapshot groups are useful for preserving the write order and ensuring crash consistency in business systems that use multiple volumes.

<span id=".5b-r54Wn5Y6f55CG"></span>
## How snapshots work

A snapshot is a backup of a volume taken at a specific point in time. For more information, see [How snapshots work](https://docs.byteplus.com/en/docs/ecs/How_snapshots_work).

<span id=".5L2_55So5Zy65pmv"></span>
## Use cases

Snapshot groups are ideal for cluster\-based workloads. Typical use cases include:


* Business systems deployed on cluster file systems that require sequential and crash consistency, such as databases and enterprise applications. Examples include self\-built MySQL clusters on ECS, LVM built on multiple volumes, and Oracle and SAP HANA cloud deployment.

* Distributed application systems, such as large websites and multi\-application collaborative systems, that require unified snapshot creation.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Only ESSD volumes support snapshot groups. PTSSD volumes do not support this feature.

* The volumes must be in the "Attached" status, and the ECS instances to which they are attached must be in the "Running" or "Stopped" status.

* The number of snapshots for each volume cannot exceed the limit. Each volume can have up to 256 manual snapshots. If the total number of group and manual snapshots exceeds 256, you cannot create additional snapshots.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* If creating a snapshot for any volume fails, the snapshot group will not be created. Its status will read "Failed to create". Delete the failed group and try again.

* Currently, when creating a snapshot group, you must select all the volumes attached to the same instance. Selecting volumes from different instances, or selecting a subset of volumes attached to the same instance, is not supported.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region for which you want to create a snapshot group.

4. On the "Snapshots" page, click the "Snapshot Groups" tab.

5. Click "Create snapshot group".

6. On the "Create snapshot group" page, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Select a data source |Select the data source for which you want to create the snapshot group, that is, the ECS instance. |
   |Volumes |Once you have selected the data source, the "Volumes" section will automatically display a list of all the volumes that are attached to that instance. |
   |Snapshot group name |(Required) Enter a name for the snapshot group. Requirements:<br><br><br>* The name must start with a Chinese character, a letter or an underscore (_).<br><br>* The name can only contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* The name must be between 1 and 128 characters long. |
   |Tag |A tag is a key\-value pair that is used to identify cloud resources. Tags help you categorize cloud resources by purpose, owner, environment and other criteria, making them easier to filter and manage.<br><br>To add a tag to a snapshot group, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b793a137640334ed4a417ac55505141a.png) </span> icon and enter the tag key and value. For more information, see [Tag management](https://docs.byteplus.com/docs/ecs/Tag-overview). |
   |Description |(Optional) Provide additional information about the snapshot group. Requirements:<br><br><br>* The description must start with a Chinese character, a letter or an underscore (_).<br><br>* The description can contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* The length must be between 0 and 255 characters. |
   |Project |Select the project to which the snapshot group belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that comprises a set of resources, users, and roles. It provides a unified view of and access to resources, as well as control over user and role permissions within the project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is no suitable project, click "Create new projects" on the right to go to the <a href="https://console.byteplus.com/iam/resourcemanage/project">IAM console</a> and create a new one.</div><br> |
   

7. Once you have finished configuring, click "Create snapshot group".


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps


* When creating an instance, you can select a snapshot group to copy the corresponding volume data. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* For other operations on snapshot groups, see the following documents:

   * [Viewing snapshot group details](https://docs.byteplus.com/en/docs/ecs/View-details-about-snapshot-consistency-group)

   * [Modifying snapshot group attributes](https://docs.byteplus.com/en/docs/ecs/Modify-property-of-snapshot-consistency-group)

   * [Rolling back a volume using a snapshot group](https://docs.byteplus.com/en/docs/ecs/Rollback-volumes-through-snapshot-consistency-group)

   * [Deleting a snapshot group](https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot-consistency-group)
