---
title: "Failure in recognizing local data volumes​ after creating Big Data ECS instances with Windows images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Local_data_volume_cannot_be_recognized_after_creating_a_Big_Data_ECS_instance_using_a_Windows_image"
---

&nbsp;

After creating a Big Data ECS instance using a Windows custom image, if local data volumes can not be recognized, you can upgrade the Virtio driver for solution.

<span id=".6Zeu6aKY56S65L6L"></span>
## Issue description


1. After you log in to the ECS instance, right\-click the Windows icon and select "Computer Management".

2. In the left navigation pane, select "Device Manager \> Other devices". An unrecognized SCSI controller is then displayed.

3. In the left navigation pane, after selecting "Disk Management", you can see only the system disk, while the local data disk is not visible.


<span id=".5aSE55CG5pa55qGI"></span>
## Solution


1. Download and install the Virtio driver on the instance. For details, follow the guide in [Step 4: Install the Virtio driver on the virtual machine](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo).

2. Restart the instance to check whether the local data volumes are recognized successfully.
