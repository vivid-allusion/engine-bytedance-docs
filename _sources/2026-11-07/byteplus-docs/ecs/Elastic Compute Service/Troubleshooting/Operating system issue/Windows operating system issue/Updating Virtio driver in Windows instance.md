---
title: "Updating Virtio driver in Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Updating_Virtio_Drivers_in_Windows_Instances"
---

This topic describes how to troubleshoot and resolve the issue of duplicate disk unique IDs in instances caused by an outdated VirtIO driver.

> If the VirtIO driver version of an instance is outdated, performing a disk reset operation may result in data loss on the instance disk.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5qOA5p-l5a6e5L6L55qEdmlydGlv6amx5Yqo54mI5pys"></span>
## Step 1: Check the Virtio driver version of the instance


1. Log in to the target instance. For more information, see [Login overview.](https://docs.byteplus.com/en/docs/ecs/Overview-1)

2. Go to the "C:\Windows\System32\drivers" directory.

3. Right\-click the "viostor.sys" file and select "Properties".

4. Click the "Details" tab, check the file version number, and verify if the VirtIO driver version is lower than the required version (100.93.104.24000). If it is lower, we recommend that you update the VirtIO driver of the instance.


<span id=".5q2l6aqk5LqM77ya5pu05paw5a6e5L6L55qEdmlydGlv6amx5Yqo56iL5bqP"></span>
## Step 2: Update the Virtio driver of the instance

If your VirtIO driver version is outdated, we recommend that you update the VirtIO driver for your instance. For more information, see [Installing VirtIO Driver](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo).
