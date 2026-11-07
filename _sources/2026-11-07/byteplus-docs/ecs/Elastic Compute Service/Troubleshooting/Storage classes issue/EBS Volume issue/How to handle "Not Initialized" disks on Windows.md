---
title: "How to handle \"Not Initialized\" disks on Windows"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Windows_disk_showing_Not_initialized"
---

<span id="LZ2OMKhq"></span>
## Issue description

When multiple volumes are mounted to a Windows instance, a disk with a "Not Initialized" error is displayed in disk management settings.

<span id="0zdqdZkj"></span>
## Causes

In the Windows operating system, each disk is identified by a unique DiskID. When multiple volumes are created from the same snapshot, these volumes inherit the same DiskID. If multiple volumes with the same DiskID are mounted to the same instance at the same time, and you perform operations on them, such as modifying disk status or formatting, the Windows operating system may fail to correctly identify target disks.

<span id="LnyhkFjK"></span>
## Solutions


1. Log in to the target instance.

2. Click the Windows icon.

3. Expand "Windows PowerShell", right\-click "Windows PowerShell", and then select "More \> Run as administrator".

4. In PowerShell, execute the following command to open DiskPart.

   ```PowerShell
   diskpart
   ```
   

5. Execute the following command to select the faulty disk.

   ```PowerShell
   sel disk 2
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, Disk 2 is the faulty disk. Replace <code>2</code> with the actual serial number of the faulty disk.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you cannot select the faulty disk, <a href="https://docs.byteplus.com/en/docs/ecs/Restarting-instances">restart the instance</a> and then try again.   </div>
   

6. Execute the following command to clear the read\-only attribute of the faulty disk.

   ```Prolog
   attr disk clear readonly
   ```
   

7. Click the Windows icon.

8. Select "Windows System \> Run".

9. Enter `diskmgmt.msc` and click the "OK" button.

10. In "Disk Management", right\-click the target disk, and then click the "Online" button.

11. Then, the disk identification exception is successfully fixed.
