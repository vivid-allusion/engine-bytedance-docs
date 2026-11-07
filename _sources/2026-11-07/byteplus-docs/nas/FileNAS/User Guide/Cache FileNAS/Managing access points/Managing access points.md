---
title: "Managing access points"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_access_points"
---

This topic explains how to manage access points in the FileNAS console, including creating, viewing, and editing access points.

<span id="0ca869f8"></span>
## Prerequisites

The Cache FileNAS file system has been created. For detailed steps, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/Creating_file_systems).

<span id="8d20b97a"></span>
## Notes

When you create a mount target, an Elastic Network Interface (ENI) is automatically generated and assigned to the Layer 4 Load Balancer (PLB). This ENI is assigned to the `default` security group by default; however, the settings of the `default` security group do not apply to the created mount target. For more information, see [Security Group Overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

<span id="a4a6cb20"></span>
## Creating access points


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Integrated point** tab, then click **Create integrated points**.

6. Set the following parameters in the pop\-up panel.

   
   |Parameters |Parameter description |
   |---|---|
   |File System ID |The File System ID of the access point. Modification is not allowed. |
   |Integrated Point Name |Set the access point name with the following naming rules:<br><br><br>* Start with English or Chinese characters.<br><br>* Can contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* Length must be between 1 and 128 characters. |
   |Private network |Select the VPC of the ECS instance that needs to be mounted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Make sure the selected VPC is the same as the one where the ECS instance is.</div><br> |
   |Permission groups |Select the permission group according to your needs. |
   |Access point root directory |Enter the root directory of the access point in the file system. You can specify a subdirectory within the file system as the access point root directory. Users accessing through this point will be restricted to this directory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the access point root directory does not exist, set the <strong>Directory creation information</strong>. The system will automatically create the root directory in the file system based on the configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the access point root directory exists, there's no need to set the <strong>directory creation information</strong> and the system will ignore it.</div><br> |
   |**Directory creation information (required only if the access point root directory does not exist)**  ||
   |Owner user ID |Set the owner user ID of the access point root directory, with a value range of [0, 2147483647]. |
   |Primary user group ID |Set the owner user group ID of the access point root directory, with a value range of [0, 2147483647]. |
   |POSIX permission |Set POSIX permission for the access point root directory using 4\-digit octal mode (e.g., `0755`). |
   | **(Optional) POSIX user**<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Once the POSIX user is configured for the access point, all I/O operations will enforce this identity, overriding the client's original POSIX identity to prevent file permission conflicts.</div><br> ||
   |User ID |POSIX user ID. |
   |User group ID |POSIX user group ID. |
   |Second group user IDs |Secondary POSIX user group ID. |
   

7. After completing the settings, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once you have successfully created the access point, you can mount the file system through it. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/nas/Mounting_file_systems">Mounting file systems</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The access point feature enables you to customize policies for precise control over permissions. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/Configuring_access_point_policies">Configuring access point policies</a>.   </div>
   


<span id="4402af07"></span>
## Viewing access points


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Integrated point** tab, then click the target access point.

6. In the popped\-up panel, view the following information.

   
   |**Category** |**Parameters** |**Description** |
   |---|---|---|
   |Basic information |Access point ID |Access point ID. |
   ||Integrated Point Name |Name of the access point. |
   ||Private network |The private network to which the access point belongs. ECS instances within the same private network can access this access point. |
   ||Subnet |The subnet to which the access point belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The access point must use an IP address within the VPC. The system automatically assigns an IP address from the subnet in the VPC with the most available IPs when creating the access point.</div><br> |
   ||Permission groups |The permission group to which the access point belongs. |
   ||Access point domain name |The domain name of the access point. |
   ||TRN |TRN for the access point. |
   |Access point root directory |Root directory |The root directory of the access point. |
   ||Owner user ID |The owner user ID of the access point root directory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The owner user ID entered when creating an access point or the owner user ID configured for the root directory. Changing the owner user ID with the chown command won't update this information here.</div><br> |
   ||Primary user group ID |The owner user group ID for the access point root directory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The owner user group ID entered when creating an access point or the owner user group ID configured for the root directory. Changing the owner user group ID with the chgrp command won't update this information here.</div><br> |
   ||POSIX permission |Displays POSIX permission information of the access point root directory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The POSIX permission entered when creating an access point or the POSIX permission configured by the root directory. Changing the POSIX permission with the chmod command won't update this information here.</div><br> |
   |POSIX user |User ID |The POSIX user ID used for performing I/O operations on all file systems through this access point. |
   ||User group ID |The POSIX user group ID used for performing I/O operations on all file systems through this access point. |
   ||Second group user IDs |The secondary POSIX user group ID used for performing I/O operations on all file systems through this access point. |
   |Access point policy |IAM policy |Access point policy is off by default. Once you enable the access point policy, you can set permissions to limit access to certain accounts only. For more information, see [Configuring access point policies](https://docs.byteplus.com/en/docs/nas/Configuring_access_point_policies). |
   |Mount command |Mount command |The command to mount access points via FSX. The command format is `mount -t fsx /nas/<access point ID>.<access point domain name>:/ <local mount directory>`. For more information on mounting file systems via FSX, refer to [Mounting file systems](https://docs.byteplus.com/en/docs/nas/Mounting_file_systems). |
   


<span id="cb25235e"></span>
## Other actions


<Tabs>
<Tab zoneid="LslBdenpWq" title="Set directory quota">
<TabTitle>Set directory quota</TabTitle>

The directory quota feature tracks and limits file count and storage usage in the root directory of the Cache FileNAS access point.

**Creating a statistical directory quota**


1. Create a directory quota.

   1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

   2. In the top menu bar, select the region where the target file system is located.

   3. In the left navigation pane, select **File System** \> **File System list**.

   4. On the **File System list** page, click the target file system.

   5. On the file system details page, click the **Integrated point** tab.

   6. On the access point list page, click **Directory quota** under the **Actions** column.

   7. In the **Create directory quota** dialog, click **Confirm**.

2. View data statistics results.

   1. On the **Directory quota** tab, click **Quota management** under the **Actions** column of the target directory path.

   2. In the **Manage quota** panel, view information such as **Quota type**, **Current capacity**, and **Current No. of files**.


**Creating a restricted directory quota**


1. Create a directory quota.

   1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

   2. In the top menu bar, select the region where the target file system is located.

   3. In the left navigation pane, select **File System** \> **File System list**.

   4. On the **File System list** page, click the target file system.

   5. On the file system details page, click the **Integrated point** tab.

   6. On the access point list page, click **Directory quota** under the **Actions** column.

   7. In the **Create directory quota** dialog, click **Confirm**.

2. Set the directory quota type to restricted.

   1. On the **Directory quota** tab, click **Quota management** under the **Actions** column of the target directory path.

   2. In the **Manage quota** panel, click **Edit** under the **Actions** column.

   3. In the **Edit user quota** dialog, set **Quota type** to **Restricted**, and configure **File amount limitation** and **Capacity constraints**.

   4. After completing the settings, click **OK**.


</Tab>
<Tab zoneid="zQL9EC25ms" title="Edit access points">
<TabTitle>Edit access points</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Integrated point** tab, then click the target access point.

6. In the access point details panel, modify the access point name, permission group, and access point policy.


</Tab>
<Tab zoneid="yjxSaJ3SEp" title="Delete access points">
<TabTitle>Delete access points</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting an access point terminates all ongoing I/O operations immediately.</div>



1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Integrated point** tab.

6. On the access point list page, click **Delete** under the **Actions** column of the access point you wish to remove.

7. In the dialog box, click **OK**.


</Tab>
<Tab zoneid="CMAr8TMuVY" title="View access point monitoring data">
<TabTitle>View access point monitoring data</TabTitle>

FileNAS syncs related monitoring metrics from the Cloud Monitor service to the FileNAS console, making it easier to access monitoring data. You can view the access point's monitoring data, including read IOPS and read bandwidth, on the FileNAS console. For detailed steps, refer to [Viewing performance monitor](https://docs.byteplus.com/en/docs/nas/Viewing_performance_monitoring).


</Tab>
</Tabs>
