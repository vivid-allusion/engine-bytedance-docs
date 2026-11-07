---
title: "Managing mount targets"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Managing_mount_targets"
---

A mount target is the entry point for an ECS instance to access the file system. This topic explains how to create a mount target and perform related operations.

<span id="bZ4bkYSQ"></span>
## Background information


* A file system can have multiple mount targets, and multiple nodes can simultaneously mount the same mount target to share file system access permissions.

* You can create only one mount target per VPC. If you need multiple mount targets, set up an equal number of VPCs. For more information, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id="8iasGt0e"></span>
## Notes

When you create a mount target, an Elastic Network Interface (ENI) is automatically generated and assigned to the Layer 4 Load Balancer (PLB). This ENI is assigned to the `default` security group by default; however, the settings of the `default` security group do not apply to the created mount target. For more information, see [Security Group Overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

<span id="3pURS1Ga"></span>
## Prerequisites

You have created a file system. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

<span id="ZRe0cMNq"></span>
## Creating a mount target


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Mount Target**.

6. On the **Mount Target** page, click **Create Mount Target**.

7. In the **Create Mount Target** dialog, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Mount Target name |Enter the name of the mount target. The mount target must:<br><br><br>* Start with English letters or Chinese characters.<br><br>* Contain only Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
   |Availability Zone |Select the availability zone where the file system is located. |
   |Private network |Select the VPC currently used by the file system and the ECS instance or create a new one. |
   |Subnet |Select or create a subnet under the VPC.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">For optimal performance, deploy your file system, ECS instance and subnet in the same availability zone.</div><br> |
   |Permission groups |Select an existing permission group from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">When you create a file system, the console establishes a default permissions group that allows any IP address within the same VPC to access the file system via this mount target. If you need to manage permission groups based on business needs, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Managing_permission_groups">Managing permission groups</a>.</div><br> |
   

8. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The mount target has been created successfully if its <strong>State</strong> is <strong>Running</strong>.   </div>
   

<span id="MN5RHmok"></span>
## Related operations


|Operation |Description |
|---|---|
|View mount commands |You can view the mount commands on the Mount Target page. Steps:<br><br><br>1. Click the expand icon next to a mount target.<br><br>2. Click the copy icon next to the command to copy it. |
|View mount target details |You can view the details of a mount target on the Mount Target page. These details include **Mount Target name/ID**, **State**, **Mount Target Domain**, and **Creation time**. |
|Modify the basic information |You can change the name of a mount target. Steps:<br><br><br>1. On the **Mount Target** page, move the cursor over the row of the mount target you want to manage.<br><br>2. Click the edit icon next to the name of the mount target.<br><br>3. In the box that appears, enter a new name for the mount target.<br><br>4. Click **OK**. |
|Modify permission groups |You can modify the permission group of a mount target. Steps:<br><br><br>1. On the **Mount Target** page, click **Modify permission groups** in the **operation** column of the mount target you want to manage.<br><br>2. In the **Modify permission groups** dialog, select the desired permission group.<br><br>3. Click **OK**. |
|View mounted clients |You can view information about the client mounted to a mount target. Steps:<br><br><br>1. On the **Mount Target** page, click  **...**  \> **View mounted client** in the **operation** column of the mount target you want to check.<br><br>2. In the **Mounted client** dialog, view details including **IP address**, **Private network**, and **Protocol Type**.<br><br>3. Click **OK** to close the dialog. |
|Disable mount targets |You can disable a mount target. Steps:<br><br><br>1. On the **Mount Target** page, click **Disable** in the **operation** column of the mount target you want to manage.<br><br>2. In the box that appears, click **Disable**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Once a mount target is disabled, it cannot be used to mount new file systems. However, file systems that were previously mounted via this mount target will not be affected.</div><br> |
|Start mount targets |You can start a mount target when the file system is **Running** and the mount target is **Disabled**. Steps:<br><br><br>1. On the **Mount Target** page, click  **...**  \> **Start** in the **operation** column of the mount target you want to manage.<br><br>2. In the box that appears, click **Start**. |
|Delete mount targets |You can delete a mount target. Steps:<br><br><br>1. On the **Mount Target** page, click  **...**  \> **Delete** in the **operation** column of the mount target you want to remove.<br><br>2. In the box that appears, click **Delete**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted mount targets cannot be recovered.</div><br> |
