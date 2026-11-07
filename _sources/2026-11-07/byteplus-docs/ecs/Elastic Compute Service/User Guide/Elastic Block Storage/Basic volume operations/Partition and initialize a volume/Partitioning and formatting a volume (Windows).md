---
title: "Partitioning and formatting a volume (Windows)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-larger-than-2-TiB"
---

This topic explains how to partition and format a data volume in the Windows operating system.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created a data volume and attached it to an ECS instance. For more information, see [Creating a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume) and [Attaching a volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Partitioning and formatting a data volume will erase all data. Make sure that there is no important data on the volume, or back up any important data first.

* For partitions of 2 TiB or smaller, use the GPT partitioning scheme.


<span id=".5YiG5Yy65qC85byP5YyW5LqR55uY77yI5bCP5LqO562J5LqOMlRpQu-8iQ=="></span>
## Partitioning and formatting a volume (≤ 2 TiB)

This guide uses Windows Server 2016 to demonstrate how to partition and format a volume using the MBR partitioning scheme. Note that these steps may differ depending on the operating system, so use this guide for reference only.


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. From the desktop, click the Start button in the lower\-left corner and select "Server Manager".

3. In the upper\-right corner of the "Server Manager" page, select "Tools \> Computer Management".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8b6e7e12a1c037c6481187aee766c29.png) </span>



&nbsp;

4. On the "Computer Management" page, select "Storage \> Disk Management".

   If your server has any uninitialized disks, the "Initialize Disk" dialog opens automatically.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b0676e1ce0c0fba1762295e3c1e9681.png) </span>



&nbsp;

5. In the "Initialize Disk" dialog, select the disk that you want to initialize. Then, select "MBR (Master Boot Record)" and click "OK".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MBR is limited to disks of 2 TiB or smaller. For disks larger than 2 TiB, use GPT.   </div>
   

6. Right\-click an unallocated region on your disk (i.e., Disk 2), and select "New Simple Volume".

7. In the "New Simple Volume Wizard", select "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc96f9e10f459beb41bdd29cedea57c8.png) </span>



&nbsp;

8. In the "New Simple Volume Wizard", enter the size of the partition you want to create. The default size is the maximum available. Here, we use the maximum default size and select "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4ef3d1be6a1f34a5feb0b82a5201f80.png) </span>



&nbsp;

9. In the "New Simple Volume Wizard", assign a drive letter or path to your partition. The default drive letter is "D". Here, we use "E" and click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8917b353e125452d03ec34f48bb01c91.png) </span>



&nbsp;

10. In the "New Simple Volume Wizard", format your partition with a new file system. The default file system is NTFS. Adjust other parameters as necessary. Here, we use the default settings and click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_117f255ad88e6b8664a77a98187ae4fc.png) </span>



&nbsp;

11. In the "New Simple Volume Wizard", review your choices and select "Finish".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc6817d41d5beeb2d64d2c1be3ab606c.png) </span>



&nbsp;

The system will take a moment to complete the initialization process. The disk has been successfully initialized when the volume status shows "Healthy".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_035df000750a0f36d80bb58748345814.png) </span>



&nbsp;

12. After creating the new volume, check if it exists in File Explorer. Here, we will check if "New Volume (E:)" exists.

   Click "This PC". If "New Volume (E:)" appears, the disk initialization is successful and the task is complete.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26dbbd3271db7beea4f940f803f4e471.png) </span>


&nbsp;

<span id=".5YiG5Yy65qC85byP5YyW5LqR55uY77yI5aSn5LqOMlRpQu-8iQ=="></span>
## Partitioning and formatting a volume (\> 2 TiB)

This guide uses Windows Server 2016 to demonstrate how to partition and format a volume using the GPT partitioning scheme. Note that these steps may differ depending on the operating system, so use this guide for reference only.


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. From the desktop, click the Start button in the lower\-left corner and select "Server Manager".

3. In the upper\-right corner of the "Server Manager" page, select "Tools \> Computer Management".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f28aa5cf80123aa159a737aa180ba79.png) </span>



&nbsp;

4. On the "Computer Management" page, select "Storage \> Disk Management".

   If your server has any uninitialized disks, the "Initialize Disk" dialog opens automatically.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_87d031714b98f72555df51457dbb9aa8.png) </span>



&nbsp;

5. In the "Initialize Disk" dialog, select the disk that you want to initialize. Then, select "GPT (GUID Partition Table)" and click "OK".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MBR is limited to disks of 2 TiB or smaller. For disks larger than 2 TiB, use GPT.   </div>
   

6. Right\-click an unallocated region on your disk (i.e., Disk 3), and select "New Simple Volume".

7. In the "New Simple Volume Wizard", select "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6e5f51f055ff538cc3fcfdc5284d1d1a.png) </span>



&nbsp;

8. In the "New Simple Volume Wizard", enter the size of the partition you want to create. The default size is the maximum available. Here, we use the maximum default size and select "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b2e9aafa8f8e2d9941bfd0c82cc5852.png) </span>



&nbsp;

9. In the "New Simple Volume Wizard", assign a drive letter or path to your partition. The default drive letter is "D". Here, we use "F" and click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89032c08283c227826c6fd88e6bf7812.png) </span>



&nbsp;

10. In the "New Simple Volume Wizard", format your partition with a new file system. The default file system is NTFS. Adjust other parameters as necessary. Here, we use the default settings and click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c07822ccf7720f5de3f0fae7a021abb.png) </span>



&nbsp;

11. In the "New Simple Volume Wizard", review your choices and select "Finish".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_639ef09e483c82351f9fdc0e9dd0aed3.png) </span>



&nbsp;

The system will take a moment to complete the initialization process. The disk has been successfully initialized when the volume status shows "Healthy".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0f35321d5381694c525f4a0c41731f7c.png) </span>



&nbsp;

12. After creating the new volume, check if it exists in File Explorer. Here, we will check if "New Volume (F:)" exists.

   Click "This PC". If "New Volume (F:)" appears, the disk initialization is successful and the task is complete.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_efc5f000eb518cab609ddf44de68d397.png) </span>


&nbsp;
