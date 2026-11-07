---
title: "Managing mount targets"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_mount_targets"
---

This topic outlines how to manage mount targets through the FileNAS console, including creating, deleting, enabling, and disabling mount targets.

<span id="d959c7cf"></span>
## Background information

A mount target is the entry point for an ECS instance to access the file system. A file system can have multiple mount targets, and multiple nodes can simultaneously mount the same mount target to share file system access permissions.

<span id="7b24fdef"></span>
## Notes


* You can create only one mount target per VPC. If you need multiple mount targets, set up an equal number of VPCs. For more information, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* When you create a mount target, an Elastic Network Interface (ENI) is automatically generated and assigned to the Layer 4 Load Balancer (PLB). This ENI is assigned to the `default` security group by default; however, the settings of the `default` security group do not apply to the created mount target. For more information, see [Security Group Overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).


<span id="992409ff"></span>
## Creating mount targets


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**. On the **File System list** page, click the file system for which you want to create a mount target.

4. On the file system details page, click the **Mount Target** tab, then click **Create Mount Target**.

5. Set the following parameters in the dialog box.

   
   |**Parameters** |**Description** |
   |---|---|
   |Mount Target name |Enter the name of the mount target. Naming rules:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* Length must be between 1 and 128 characters. |
   |Private network |Select the VPC currently used by the file system and the ECS instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can create only one mount target for a VPC in the same file system.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A single mount target can be shared by multiple ECS instances within the same VPC.</div><br> |
   |Subnet |Select the subnet under the VPC.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For optimal performance, deploy your file system, ECS instance and subnet in the same availability zone.</div><br> |
   |Permission groups |Select the appropriate permission group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you create a file system, the console establishes a default permissions group that allows any IP address within the same VPC to access the file system via this mount target. If you need to manage permission groups based on business needs, see <a href="https://docs.byteplus.com/en/docs/nas/Managing_permission_groups">Managing permission groups</a>.</div><br> |
   

6. After completing the settings, click **Create**.

   Creating the mount target may take a few minutes.


<span id="170a8d4c"></span>
## Other actions

You can also perform these actions on the **Mount Target** page:


|**Actions** |**Description** |
|---|---|
|Modify permission groups |Click **Modify permission groups** in the **Actions** column of the target mount target, then select the appropriate permission group in the dialog box. If you want to create a new permission group, see [Managing permission groups](https://docs.byteplus.com/en/docs/6453/1276605). |
|Disable mount targets |Click **Disable** in the **Actions** column of the target mount target to block all access to this mount target. |
|Start mount targets |Click  **...**  \> **Start** in the **Actions** column of the target mount target to activate access. |
|Delete mount targets |Click  **...**  \> **Delete** in the **Actions** column of the target mount target, and confirm by clicking **Delete** in the dialog box.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted mount targets cannot be recovered.</div><br> |


&nbsp;
