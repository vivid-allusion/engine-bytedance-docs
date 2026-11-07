---
title: "Detaching a volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Detach-volume"
---

You can detach a data volume from one ECS instance and attach it to another. Detaching a volume does not erase the data on it. Detaching system volumes is not supported. This topic explains how to detach a data volume from an instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Detach operations are only available for pay\-as\-you\-go data volumes.

* You can detach data volumes either online or offline. The target instance's status can be either "Running" or "Stopped".

* Make sure you have deleted the automatic mount configuration for the data volume partitions in the /etc/fstab file. Otherwise, the instance will not start properly when you restart it after detaching the data volume in the console.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Detaching a volume from a running instance may disrupt business operations. Proceed with caution.

* To ensure data integrity, we recommend stopping all read and write operations to your data volume before detaching it. Otherwise, any incomplete operations may be lost.

* Before detaching a data volume with a mounted file system from the console, connect to the instance remotely and unmount it in the operating system.

   * For a Windows instance, set the volume offline in Windows before detaching it. For more information, see [Unmounting a data volume in Windows](https://docs.byteplus.com/en/docs/ecs/Detach-volume?lang=en&TagIDs=2,288,70,69#.5ZyoTGludXjns7vnu5_kuIrljbjovb3mlbDmja7nm5g=).

   * For a Linux instance, use the `umount` command to disassociate the volume from its file system before detaching the volume. For more information, see [Unmounting a data volume in Linux](https://docs.byteplus.com/en/docs/ecs/Detach-volume?lang=en&TagIDs=2,288,70,69#.5ZyoV2luZG93c-ezu-e7n-S4iuWNuOi9veaVsOaNruebmA==).


<span id=".5q2l6aqk5LiA77ya5Zyo5pON5L2c57O757uf5LiK5Y246L295pWw5o2u55uY"></span>
## Step 1: Unmount a data volume in the operating system

<span id=".5ZyoTGludXjns7vnu5_kuIrljbjovb3mlbDmja7nm5g="></span>
### Unmounting a data volume in Linux

This section explains how to unmount a data volume in CentOS 7.6. Note that these steps may differ depending on the operating system, so use this guide as a reference only.


1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the `df -h` command to view mount details.

   The output will resemble the following, where `/dev/vdc1` represents the data volume partition.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ccac8f690061949d212347f5c2ef1e9d.png) </span>

3. Run the `umount` command to unmount the file system.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use the operating system monitoring feature to find the volume ID associated with a specific device. This will help you identify the file system when you unmount the volume. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/View-a-volume-serial-number">Viewing the mapping between volume IDs and device names</a>.   </div>
   

   The following command unmounts the file system for `/dev/vdc1`.

   ```Plain Text
   umount /dev/vdc1
   ```
   

4. Run the `blkid` command to obtain the UUID of the partition.

   You will see output similar to the following:

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_656b86378c9d485d81ba6fb93a92b440.png) </span>

5. Run this command to see if the partition is configured to mount automatically in `/etc/fstab`.

   ```Plain Text
   cat /etc/fstab
   ```
   

   The output below shows the UUID obtained in the previous step. This indicates that the partition (`/dev/vdc1`) is configured to mount automatically in `/etc/fstab`.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f3a69b4737426b2c13947691a1ee74b7.png) </span>

6. Delete the automatic mounting configuration in `/etc/fstab`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you do not delete the automatic mount configuration for the partition in <code>/etc/fstab</code>, the instance will not start properly when you restart it after detaching the data volume in the console.   </div>
   

   1. Run this command to edit `/etc/fstab`.

      ```Plain Text
      vim /etc/fstab
      ```
      

   2. Press `i` to enter insert mode.

   3. Delete or comment out the line that contains the automatic mounting entry.

      To comment it out, add a `#` at the beginning of the line, as shown below.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d93c97ca1240bcc00d55a993946d73ef.png) </span>

   4. Press Esc, type `:wq`, and press Enter to save and exit.


<span id=".5ZyoV2luZG93c-ezu-e7n-S4iuWNuOi9veaVsOaNruebmA=="></span>
### Unmounting a data volume in Windows

This section explains how to unmount a data volume in Windows 2016. Note that these steps may differ depending on the operating system, so use this guide as a reference only.


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. From the desktop, click the Start button in the lower\-left corner and select "Server Manager".

3. In the upper\-right corner of the "Server Manager" page, select "Tools \> Computer Management".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_309514cf951299bb891ef87db2d641b2.png) </span>



&nbsp;

4. In the "Computer Management" window, select "Storage \> Disk Management".

5. Right‑click the volume you want to unmount and select "Offline".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f479056a890df1daf275d2847868800.png) </span>



&nbsp;

Once the volume is offline, its status changes from "Online" to "Offline".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bcc0f8e3d49f21879fb86d7730d446f6.png) </span>


&nbsp;

<span id=".5q2l6aqk5LqM77ya5ZyoRUNT5o6n5Yi25Y-w5LiK5Y246L295pWw55uY"></span>
## Step 2: Detach a volume in the ECS console


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, click "... \> Detach" in the "Actions" column of the volume.

5. In the box that appears, verify the details and click "Detach".


<span id=".5pON5L2c57uT5p6c"></span>
## Result

Once the data volume has been successfully detached, it will no longer appear on the "Volumes" tab of the instance details page. The status of the volume changes from "Attached" to "Available" on the "Volumes" page.
