---
title: "Extending a volume (Windows)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Extend-volume-windows"
---

<span id=".5pON5L2c6K-05piO"></span>
## Scenarios

Suppose you have an ECS\-1 Windows instance with a 50 GiB system volume and a 60 GiB data volume. The data volume has already been partitioned, formatted, and mounted.

This guide will show you how to increase the size of both volumes to 80 GiB.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

There is a risk of data loss if the operation fails. Therefore, ensure your data is backed up before extending the volumes.

<span id=".56ys5LiA5q2l77ya5Zyo5o6n5Yi25Y-w5omp5a655LqR55uY"></span>
## Step 1: Extend a volume in the console

You can extend your volume in the console using one of the following methods.

<span id=".5omp5a655Y2V5Liq5LqR55uY"></span>
### Extending a single volume

**From the Instances page**


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, click "Instances".

3. In the top menu bar, select the project and region where the instance resides.

4. Click the instance you want to manage.

5. Click the "Volumes" tab.

6. Click "... \> Extend volume" in the "Actions" column of the volumn you want to manage.

7. On the "Extend volume" page, verify the current configuration. Then, enter 80 GiB under "New capacity".

8. Confirm your order by clicking "Extend volume".

   After the extension is complete, click "Go to the console to attach". On the "Extend volume" page, click "Return to the volume list". On the "Volumes" page, click the name of the volume to view its capacity in the "Overview" panel.


**From the Volumes page**


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, click "Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, click "... \> Extend volume" in the "Actions" column of the volume you want to manage.

5. On the "Extend volume" page, verify the current configuration. Then, enter 80 GiB under "New capacity".

6. Confirm your order by clicking "Extend volume".

   After the extension is complete, click "Go to the console to attach". On the "Extend volume" page, click "Return to the volume list". On the "Volumes" page, click the name of the volume to view its capacity in the "Overview" panel.


<span id=".5om56YeP5omp5a655LqR55uY"></span>
### Extending volumes in batches

From the "Volumes" page, you can extend multiple volumes at once. You can select multiple volumes across instances, availability zones, billing methods, volume types, and volume specifications.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can extend up to 50 volumes at once.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, click "Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, select the volumes that you want to extend. Then, click "Extend volume" at the bottom of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, navigate to the "Instances" page. Click the name of the instance for which you want to increase the storage capacity, and then click the "Volumes" tab. On this page, select the desired volumes and click "Extend volume". When extending multiple volumes from the "Instances" page, you can only extend volumes attached to that instance.   </div>
   

5. On the "Extending volumes in batches" page, set the capacity for each volume separately in the "Target capacity" column, or set the same capacity for all volumes next to "Set extended capacity in batches".

6. Once you have finished configuring, click "Extend volume".

   On the "Extending volumes in batches" page, click "Next step" and then click "Return to the volume list". On the "Volumes" page, click the name of the volume to view its capacity in the "Overview" panel.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your extension batch includes subscription volumes, pay for them by following the instructions after clicking "Extend volume".   </div>
   

<span id=".56ys5LqM5q2l77ya5p-l55yL5YiG5Yy65ZKM5paH5Lu257O757uf5oOF5Ya1"></span>
## Step 2: View information about volume partitions and file systems

These steps are for Windows Server 2019. They may differ on other operating systems, so use this guide for reference only.


1. Remotely connect to and log in to the ECS instance. For instructions, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the desktop, right\-click the icon in the lower‑left corner and select "Server Manager".

3. Click "Tools" and select "Computer Management".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2c3c1eb82a67b849fb4aa4285e7890e.png) </span>

4. In the left navigation pane, click "Disk Management". The "Disk Management" window opens.

5. In the top menu bar, select "Action \-\> Rescan Disks". The disk information is displayed as follows:

   * The instance has two attached volumes: "Disk 0" and "Disk 1".

   * "Disk 0" is a system volume and has one partition, `C:`.

   * "Disk 1" is a data volume and has one partition, `D:`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_85b1863334c318bb9285d75ecbf31c34.png) </span>


<span id=".5q2l6aqk5LiJ77ya5omp5a655YiG5Yy655qE5paH5Lu257O757uf"></span>
## Step 3: Add the additional space to an existing partition and file system

As shown in Step 2, extending the volume in the console will not automatically expand its partitions and file systems. These steps explain how to add the unallocated space to an existing partition and file system.


1. Right\-click the partition you want to extend and select "Extend Volume".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a5d21aba815b49446fa95d96b8d4472.png) </span>

2. In the "Extend Volume Wizard", enter the amount of space you want to add.

3. After the extension is complete, the unallocated space will be merged into the selected partition and file system.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f92d17c3bb0ab2c8855d4ff50a19290.png) </span>


<span id=".77yI5Y-v6YCJ77yJ5q2l6aqk5Zub77ya5paw5bu65YiG5Yy65ZKM5paH5Lu257O757uf"></span>
## (Optional) Step 4: Create a new partition and file system with the additional space

After expanding the volume in the console, follow these steps to create a partition with the unallocated space.


1. Right\-click the unallocated space and select "New Simple Volume".

2. In the "New Simple Volume Wizard", click "Next".

3. Set the volume size. The default setting uses all the unallocated space. Click "Next".

4. Assign a drive letter and click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_388e86040be5d628a3b175da329e3114.png) </span>



&nbsp;

5. Select "Format this volume with the following settings", configure the necessary parameters, and click "Next" to finish creating the partition.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_563dfc9ffba25e5a6c105011b6648ae0.png) </span>



&nbsp;

6. Click "Finish" to complete the wizard. The system will take a moment to complete the initialization process. The disk has been successfully initialized when the volume status shows "Healthy".


<span id="r0xfyIgV"></span>
## FAQ

**Can I use the capacity of one data volume to extend another data volume or system volume?** 

No, due to how partition management works, you can only add space to the last partition on a volume. You cannot move or reallocate capacity from one volume to another. Therefore, the space on a data volume cannot be used to increase the size of a different data or system volume.
