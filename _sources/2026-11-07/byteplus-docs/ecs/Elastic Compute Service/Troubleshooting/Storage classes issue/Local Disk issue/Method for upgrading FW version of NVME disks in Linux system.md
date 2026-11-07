---
title: "Method for upgrading FW version of NVME disks in Linux system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_upgrading_the_firmware_version_of_NVME_drives_in_Linux_systems"
---

This topic mainly describes how to resolve the issue of probabilistic disk drop for NVMe disks in misaligned business scenarios by upgrading the NVMe disk firmware (FW) version online.

> FW version of NVMe disk refers to the firmware version of an NVMe (Non\-Volatile Memory Express) disk. It is the core program version for interaction between disk hardware and the system, affecting disk stability, performance, and other aspects. Firmware serves as the "operating system" of NVMe disks, and its version determines the disk's key capabilities.


<span id="RaDt6YVD"></span>
## Problem description

For [Local SSD](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#8IH6RHiz) instances mounted with certain models of NVME disks, probabilistic disk drop may occur due to defects in the disk firmware version. As a result, the Linux operating system cannot recognize the corresponding local volume, and the instance cannot perform read or write operations on this local volume.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">During the upgrade for non\-specific models of NVME disks, a prompt appears indicating that the local volume firmware version is already the latest and no upgrade is needed.</div>


<span id="boxhSCer"></span>
## Causes

When two 512 B unaligned I/O operations (initiated separately by the primary CPU and the secondary CPU) access the same 4 KB physical unit (IU), data is retrieved from different locations within the IU that may overlap. As a result, this forms a cross\-access region within the IU.

Specifically, disk physical space is divided into multiple 4 KB IUs, and the size of the I/O that is actually written to the disk is 512 B logical sectors. When a write I/O falls into a certain IU, if another write I/O also sequentially falls into the same IU, the disk adopts a per\-IU queuing mechanism for logical I/O processing. During the simultaneous processing of these two I/Os, timing errors may cause queue abnormalities, causing disk status exceptions and I/O timeouts. At this time, the kernel tries to recover via a reset. However, the reset fails due to the disk in an abnormal status, resulting in a disk drop.

<span id="lPIvnWrd"></span>
## Usage note


* Time of upgrading firmware version for one disk  **< ** 5s

* Maximum I/O latency during firmware version upgrade for one disk **<**  5s


<span id="jgO4DaYX"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Disk I/O latency may increase during the upgrade. We recommend performing the upgrade during off\-peak business hours or when the business is idle.</div>



1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to upgrade the firmware version of a local volume online.

   ```Plain Text
   region=$(wget -q -O - http://100.96.0.96/volcstack/latest/region_id);bash -c "$(wget -q -O - http://nvme-tools-${region}.tos-${region}.ivolces.com/update_nvme_firmware.sh)"
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can directly execute the above command without modifying any information.   </div>
   

3. Check the upgrade result:

   * If `Update INTEL disk firmware success` is prompted, ** ** this indicates the upgrade succeeds.

   * If `INTEL disk firmware is 9CV10501, no update is needed` ** **  or `There is no INTEL NVMe disk, so no update is needed` is prompted, ** **  this indicates the firmware version of the local volume firmware version is already the latest, and no upgrade is needed.

   * To obtain support when other messages are prompted, contact your account manager.


<span id="WDUfw1tB"></span>
## Suggestion after upgrade

We recommend observing the stability of disk\-dependent services within 24 hours after the upgrade. For example, check if the database has read/write latency and if the file storage response speed is normal to confirm no new exceptions.
