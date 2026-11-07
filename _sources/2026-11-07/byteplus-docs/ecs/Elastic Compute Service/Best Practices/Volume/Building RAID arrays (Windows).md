---
title: "Building RAID arrays (Windows)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Build_RAID_array_Windows"
---

This topic introduces the procedure for constructing a RAID array in Windows operating system. In the example provided in this topic, Windows Server 2022 is used to build a RAID 5 disk array.

<span id="rPhbubDI"></span>
## Background

For a basic introduction to RAID, including RAID levels, advantages and disadvantages, and the minimum number of disks required to build an array, refer to [Build RAID array (Linux)](https://docs.byteplus.com/en/docs/ecs/Build_RAID_Arrays_Linux).

<span id="qnM7ADLd"></span>
## Usage notes


* Before constructing RAID, be sure to perform [data backup](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration). The construction process may perform operations such as disk initialization, resulting in data loss.

* The system volume contains the operating system and critical system files, which are essential for system startup and operation. Therefore, it is not recommended to use the system volume to construct RAID.

* It is recommended to use data volumes with the same capacity and model to construct RAID to ensure optimal performance and compatibility.


<span id="4YtF4tkD"></span>
## Prerequisites

Already own an ECS instance, with the following basic configuration:


* Image: In the example provided in this topic, Windows Server 2022 is used.

* Storage: Mount 3 high\-speed data volumes, each sized 20 GiB.

* Network: Associate an Elastic IP (EIP).


<span id="vWCyhQ5O"></span>
## Procedure


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Select "Start \> Windows Administrative Tools \> Computer Management \> Disk Management".

3. If the disk has not yet been initialized, click the "OK" button to perform the initialization.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a287846598143d7e95b1569ad7351330.png) </span>

4. Right\-click any unallocated disk space and select "New RAID\-5 Volume".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84cfd6db02562f3372c3f212ce8d9f62.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   


&nbsp;

* <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Simple volume: A simple volume is a zone on a basic disk that can only use the space of one disk. It lacks fault\-tolerance features and performance enhancements. Mainly used to divide disk space into manageable logical units for formatting the file system and data storage.</div>


   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Cross\-zone volume: Allows unallocated space on multiple disks to be combined into a single logical volume, which can be used to expand storage capacity and merge multiple smaller disk spaces into a larger volume for unified management and usage.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Striped volume: Also known as RAID 0, it does not provide data redundancy, cannot be expanded, and does not offer fault tolerance, but significantly improves I/O performance.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Mirrored volume: That is, RAID 1, requires at least two disks, one for data storage and the other for mirroring (50% utilization). If one disk fails, the other can continue to operate completely normally, with no significant I/O improvement.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">RAID\-5 volume: Requires at least three disks, essentially balancing the advantages of RAID 1 and RAID 0. The usable capacity is equal to the capacity of a single disk ×(n\-1), where n is the number of disks.   </div>
   

5. Go to the volume wizard page and click the "Next step" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26884af5b9d26ebca4ae8a659aae398f.png) </span>

6. Add all the free space that you want to include in the RAID 5 volume to the selected area on the right side (BuildingRAID 5 requires at least three disks), then click the "Next step" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_05a9767c8a1396dc93fe8ec1d770ee07.png) </span>

7. Assign a drive letter to the newly created volume and click the "Next step" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36d6b4d1a7752cfc98618d076e4fa651.png) </span>

8. Set the volume label (in this text set as RAID 5) and file system arguments, then click the "Next step" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a31e2f40a5c3fa043564b3885fcbb03.png) </span>

9. Finally, review the settings and click the "Finish" button. Then in the dialog box that appears, click "Yes".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f166209f49c89deb53c580496c1da1b.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_437dfbc63c11c208d730b4362974f31e.png) </span>

10. Open "This PC". If you can see "RAID 5 (D:)", it indicates that the disk initialization was successful, and the task is complete.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_af6a7e1d28e51ca3a2c302f6565b1cc4.png) </span>


&nbsp;

&nbsp;
