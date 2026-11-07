---
title: "Recovering Windows instance data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Restoring-data-on-a-Windows-instance"
---

This topic describes how to use the built\-in Disk Management tool of Windows to resolve common data volume partition loss issues on a Windows ECS instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

Before you repair the data, back up the data volume with lost partitions first. We recommend that you regularly back up your data to improve data security.

<span id=".56OB55uY5aSE5LqO6ISx5py654q25oCB77yM5LiN5pi-56S65pWw5o2u55uY"></span>
## Data disk not displayed because the disk is offline

In Windows, the data disk is not displayed. In Disk Management, the disk is offline and no partitions are shown.

**Solution:** 

Right\-click the offline disk area (for example, Disk 1), and select "Online" from the shortcut menu.

<span id=".56OB55uY5pyq5YiG6YWN55uY56ym77yM5LiN5pi-56S65pWw5o2u55uY"></span>
## Data volume not displayed due to missing drive letters

In a Windows system, the data volume is not displayed. When you check the volume status in Disk Management, the data volume information is displayed. However, the data volume does not have a drive letter.

**Solution:** 

Right\-click the primary partition area of the volume, select "Change Drive Letter and Paths..." in the displayed menu, and add a drive letter as prompted.

<span id=".56OB55uY5paH5Lu257O757uf5peg5rOV6K-G5Yir77yM5LiN5pi-56S65pWw5o2u55uY"></span>
## Data volume not displayed due to the failure in recognizing the disk file system

In a Windows system, the data volume is not displayed. When you check the volume status in Disk Management, the data volume information is displayed. However, the file system cannot be recognized.

**Solution:** 

The issue described above is most likely caused by reinstalling Windows on your Linux instance. After the system is reinstalled, the file system may become incompatible, causing the disk to be hidden. If the disk is not displayed, you can reinitialize the disk and create partitions again.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Formatting the volume will result in data loss. Back up the data in the data volume in advance to prevent data loss.</div>
