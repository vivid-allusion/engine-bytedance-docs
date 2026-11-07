---
title: "Method for checking residual items of disk drivers in Windows ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Check_method_for_residual_items_of_disk_drives_on_Windows_ECS_instances"
---

This topic describes how to troubleshoot the issue where a newly mounted volume fails to be recognized or a disk device can not be accessed due to residual disk driver items in a Windows instance.

In the example provided in this topic, Windows Server 2019 is used. The operating system may differ slightly depending on the version.

> This topic may contain information about third\-party products. Related information is for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Enter the Registry Editor.

   1. In the search box at the lower left corner of the desktop, enter "Registry Editor".

   2. In the pop\-up pane, click "Registry Editor".

3. Whether residual items exist in UpperFilters.

   1. Enter the "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\{4d36e967\-e325\-11ce\-bfc1\-08002be10318}" directory.

   2. Select and right\-click "UpperFilters", and choose "Modify..." to search for any residual items.

      * If only the "partmgr" field exists, this indicates no residual items.

      * If other fields also exist, this indicates that residual items exist. Continue the following operations.

4. Check for residual disk driver items in the registry entry of each disk.

   1. Enter the "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\SCSI" directory.

   2. Check whether "UpperFilters" exists in disk registry entries.

      * If disk registry entries do not contain "UpperFilters", this indicates no residual items of disk drivers in the Windows system.

      * If "UpperFilters" exists in a disk registry entry, this indicates there are residual disk driver items in the Windows system. And in Windows "Disk Management", the corresponding disk drive is in **exception** status, which means the disk can not be accessed.

5. Clear residual disk driver items.

   1. Enter the "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\{4d36e967\-e325\-11ce\-bfc1\-08002be10318}" path.

   2. Select and right\-click "UpperFilters", and choose "Modify...".

   3. In "Value data", delete the fields corresponding to residual items. For example, delete the "test_filter" field.

      <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="2">danger      </div>
      

      <div data-tips="true" data-tips-type="danger" data-wrapper-indent="2">Make sure that the driver corresponding to the field to be deleted has already been removed. Otherwise, deleting residual files by mistake disables drivers that reference them. You can check the directory where you installed drivers (such as C:\Windows\System32\drivers) to see if the driver corresponding to "test_filter" exists. If it does not exist, the driver is removed.      </div>
      

   4. Click "Create" to complete the operation.

6. Restart the Windows instance.

   > Since restarting the instance may stop the instance or your business, proceed with caution.
