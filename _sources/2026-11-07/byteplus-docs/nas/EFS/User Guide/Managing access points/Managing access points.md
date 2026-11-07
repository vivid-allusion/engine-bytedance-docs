---
title: "Managing access points"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_managing_access_points"
---

This topic explains how to create and view access points and perform related operations.

<span id="i8Jl0s5O"></span>
## Notes

When you create an access point, an Elastic Network Interface (ENI) is automatically generated and assigned to the Layer 4 Load Balancer (PLB). This ENI is assigned to the `default` security group by default. However, the settings of the `default` security group do not apply to the access point that has been created. For more information, see [Security Group Overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

<span id="8GyvmYse"></span>
## Prerequisites

You have created a file system. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

<span id="8DplUcqW"></span>
## Creating an access point


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access Point**.

6. On the **Access** **Point** page, click **Create Access Point**.

7. In the **Create Access Point** panel, configure the following parameters.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |File System ID |The ID of the file system to which the access point belongs. It is displayed automatically and cannot be changed. |
      |Access Point Name |Specify the name of the access point. The access point names must:<br><br><br>* Start with English letters or Chinese characters.<br><br>* Contain only Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
      |Access point root directory |Specify the root directory for the access point within the file system. Once the root directory is specified, users accessing EFS file systems through this access point will only be able to access the resources within that directory. Constraints:<br><br><br>* The directory path must start with a forward slash (/).<br><br>* The directory path can only contain letters, numbers, underscores (_), hyphens (\-), forward slashes (/), or periods (.).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the access point root directory does not exist, click <strong>Create directory</strong> to create a new one. The system will automatically create the root directory in the file system based on the configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the access point root directory does not exist, and you did not create one using the <strong>Create directory</strong> option, the creation of the access point will fail.</div><br> |
      |Create directory |If the **Access point root directory** does not exist, click **Create directory** to create a new one. The following parameters are required:<br><br><br>* **File System ID**: Displayed automatically and cannot be changed.<br><br>* **Directory path**: Set the root directory for the access point. Constraints:<br><br>   * The directory path must start with a forward slash (/).<br><br>   * The directory path can only contain letters, numbers, underscores (_), hyphens (\-), forward slashes (/), or periods (.).<br><br>* **Owner user ID**: Set the owner user ID for the access point root directory to any integer ranging from 0 to 2147483647.<br><br>* **Owner** **Group** **ID**: Set the primary user group ID for the access point root directory to any integer ranging from 0 to 2147483647.<br><br>* **POSIX permission**: Set the POSIX permissions for the access point root directory. Enter a valid octal value, such as 0755. |
      |Private network |Select the virtual private cloud (VPC) currently used by the file system and the Elastic Compute Service (ECS) instance or create a new one. |
      |Subnet |Select or create a subnet under the **VPC**. |
      |Permission groups |Select the desired permission group. For more information, see [Managing permission groups](https://docs.byteplus.com/en/docs/nas/efs_Managing_permission_groups). |
      

   * **POSIX user** (Optional)

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When you configure a POSIX user, all client\-side operations are replaced with the operations of this POSIX user. Access permissions for the access point depend on this POSIX user, not the local user.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If a user ID is entered, a user group ID must also be provided.      </div>
      

      
      |Parameter |Description |
      |---|---|
      |User ID |Set the POSIX user ID to any integer ranging from 0 to 2147483647. |
      |Group ID |Set the POSIX user group ID to any integer ranging from 0 to 2147483647. |
      |Second user group ID list |Set the secondary POSIX user group ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter supports batch input. Use commas (,) to separate multiple entries.</div><br> |
      

8. Click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The access point has been created successfully if its <strong>State</strong> is <strong>Running</strong>.   </div>
   

<span id="1YLRe7NU"></span>
## Viewing access point details


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access** **Point**.

6. On the **Access** **Point** page, click the access point you want to manage.

7. In the access point details panel, view the following information:

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Access Point ID |ID of the access point. |
      |Access Point Name |Name of the access point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To change the name of an access point, click the edit icon next to it.</div><br> |
      |Private network |The private network configured for the access point. ECS instances within the same private network can access this access point. |
      |Subnet |The subnet configured for the access point. |
      |Permission groups |The permission group associated with the access point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To modify the permission group, click the edit icon next to it.</div><br> |
      |Access Point Domain Name |The domain name of the access point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To copy the access point domain name, click the copy icon next to it.</div><br> |
      |TRN |TRN for the access point.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click the copy icon next to the TRN to copy it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TRN (The Resource Name) is a globally unique identifier for resources on BytePlus, composed of service, region, account, resource path, and other information. This information is required when configuring Identity and Access Management (IAM) policies for the access point. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Configuring_access_point_policies">Configuring access point policies</a>.</div><br> |
      |Access point root directory |The root directory of the access point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To copy the access point root directory, click the copy icon next to it.</div><br> |
      

   * **POSIX user**

      
      |Parameter |Description |
      |---|---|
      |User ID |The POSIX user ID used for performing I/O operations on all file systems through this access point. |
      |Group ID |The POSIX user group ID used for performing I/O operations on all file systems through this access point. |
      |Second Group IDs |The secondary POSIX user group ID used for performing I/O operations on all file systems through this access point. |
      

   * **Access point policy**

      
      |Parameter |Description |
      |---|---|
      |Access point policy |Disabled by default, where anonymous accounts are allowed to mount and access the access point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">You can enable the access point policy to set permissions that limit access to certain accounts. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Configuring_access_point_policies">Configuring access point policies</a>.</div><br> |
      

   * **Mount command**

      
      |Parameter |Description |
      |---|---|
      |Mount command |The command to mount the access point via FSX. The command format is `mount -t fsx /efs/<access point ID>.<access point domain name>:/ <local mount directory>`. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX). |
      


<span id="Rz6DTfyU"></span>
## Related operations


<Tabs>
<Tab zoneid="kEe7JDqN" title="Set directory quota">
<TabTitle>Set directory quota</TabTitle>

The directory quota feature tracks and limits file count and storage usage in the root directory of the EFS access point. To modify or create a directory quota for an access point, click  **...**  \> **Directory quota** in the **Actions** column of the access point. For more information, see [Managing directory quotas](https://docs.byteplus.com/en/docs/nas/efs_Managing_directory_quotas).


</Tab>
<Tab zoneid="c38s7c3M" title="Edit access points">
<TabTitle>Edit access points</TabTitle>

1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access** **point**.

6. On the **Access** **point** page, click an access point. This will take you to the details panel.

7. In the access point details panel, modify the **Access Point Name**, **Permission groups**, and **Access point policy** based on your needs.


</Tab>
<Tab zoneid="3byKfe0X" title="Delete access points">
<TabTitle>Delete access points</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">Deleting an access point terminates all ongoing I/O operations immediately.</div>



1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access** **point**.

6. On the **Access** **point** page, click  **...**  \> **Delete** in the **Actions** column of the access point you wish to remove.

7. In the box that appears, click **Delete**.


</Tab>
<Tab zoneid="joWBPNNR" title="View access point monitoring data">
<TabTitle>View access point monitoring data</TabTitle>

EFS synchronizes related monitoring metrics from Cloud Monitor to the EFS console, making it easier to access monitoring data. You can view the access point's monitoring data, including read IOPS and read bandwidth, on the EFS console. For instructions, see [Viewing performance monitoring](https://docs.byteplus.com/en/docs/nas/efs_Viewing_performance_monitoring).


</Tab>
</Tabs>
