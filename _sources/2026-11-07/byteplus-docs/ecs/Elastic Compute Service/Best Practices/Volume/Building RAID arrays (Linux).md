---
title: "Building RAID arrays (Linux)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Build_RAID_Arrays_Linux"
---

This article takes building a RAID 10 disk array as an example to introduce the procedure for building RAID arrays on Linux instances.

<span id="6ZpqOCF4"></span>
## Background

RAID (Redundant Array of Independent Disks) is a technology that combines multiple disks into a disk array group in a specific way. This technology enables the entire system to provide higher performance, better data reliability, and availability. The working principle of RAID technology is based on different RAID levels, each utilizing distinct data distribution and redundancy policies. Common RAID levels include RAID 0 (improves read and write performance), RAID 1 (mirroring backup), RAID 5 (balances performance and data redundancy), and RAID 10 (combines the advantages of RAID 1 and RAID 0).


|RAID level |Description |Minimum number of EBS volumes required |
|---|---|---|
|RAID 0 |Data is striped across multiple disks, For example, with two disks forming RAID 0, the data will be divided into several small blocks alternately stored on these two disks.<br><br>> Striping refers to dividing data into fixed\-sized blocks (stripes) and then sequentially allocating these blocks to different disk drives.<br><br><br><br>* Advantage: High read and write performance.<br><br>* Disadvantage: Does not provide data redundancy. If one of the disks fails, all data will be lost, resulting in low reliability.<br><br>* Scenario: Applicable to scenarios requiring high data read and write speeds but with low data security requirements, such as video editing, temporary data storage, cache, etc. |2 |
|RAID 1 |By means of an image, data is simultaneously written to two or more disks, forming identical copies.<br><br><br>* Advantages: High data security; as long as one disk is functioning normally, data will not be lost. At the same time, read operations can be performed in parallel on multiple disks, improving read performance.<br><br>* Disadvantages: Low disk space utilization, only 50% (with two disks), and relatively high cost.<br><br>* Scenarios: Scenarios with extremely high requirements for data security, such as critical data storage in industries like finance or healthcare. |2 |
|RAID 5 |Distribute data and parity information across multiple disks, with parity information used to recover data in case of disk failure.<br><br><br>* Advantages: Balances performance and data redundancy. Read performance is high, while write performance decreases compared to RAID 0 but remains acceptable. At the same time, it allows a disk failure without losing data.<br><br>* Disadvantage: When writing data, checksum information needs to be calculated and updated, which incurs some performance overhead. When there is a disk failure, the data recovery process is relatively complex.<br><br>* Scenario: Suitable for most enterprise\-level applications such as database servers and file servers, with certain requirements for performance and data security. |3 |
|RAID 6 |Similar to RAID 5, but uses dual parity information, allowing two disks to fail simultaneously without data loss.<br><br><br>* Advantages: Higher data security, capable of tolerating two disk failures.<br><br>* Disadvantages: Write performance is worse than RAID 5 as it requires calculating and updating dual parity information. Disk space utilization is relatively low, and costs are higher.<br><br>* Scenarios: Critical business systems requiring extremely high data security, where data loss due to disk failures is unacceptable, such as large\-scale data centers and core banking systems. |4 |
|RAID 10 |First, pair the disks to form RAID 1 image sets, and then combine these image sets into a RAID 0 array.<br><br><br>* Advantage: Combines the strengths of RAID 0 and RAID 1, offering high read/write performance and high data security.<br><br>* Disadvantage: Low disk space utilization and higher costs.<br><br>* Scenario: Suitable for scenarios with high demands on performance and reliability, such as high\-end database applications and virtualization servers. |4 |


<span id="3fEPu66m"></span>
## Usage notes


* Before constructing RAID, be sure to perform [data backup](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration). The construction process may perform operations such as disk initialization, resulting in data loss.

* The system volume contains the operating system and critical system files, which are essential for system startup and operation. Therefore, it is not recommended to use the system volume to construct RAID.

* It is recommended to use data volumes with the same capacity and model to construct RAID to ensure optimal performance and compatibility.


<span id="4yKxi0rr"></span>
## Prerequisites

[Create an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances), with the basic configuration as follows:


* Image: This article uses CentOS Stream9 64\-bit as an example.

* Storage: Mount four 20GiB ultra\-fast data volumes.

* Network: An Elastic IP (EIP) has been associated.


<span id="Q8kzQIM0"></span>
## Procedure


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to view the disk status.

   ```JSON
   lsblk
   ```
   

   The response is as follows, indicating that this instance has mounted four data volumes, with device names dev/vdb, dev/vdc, dev/vdd, and dev/vde.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6be88b66438c87bdba134610d4c87326.png) </span>

3. Use mdadm to create RAID arrays.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">mdadm (short for multiple devices admin) is a standard software RAID management tool for Linux systems. It is a simple yet powerful application that can be used for almost any level of RAID.   </div>
   

   1. Run the following command to install the mdadm tool.

      ```JSON
      sudo yum install mdadm
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ad65f499b9f3ee557ab7dd1f277a6766.png) </span>

   2. Run the following command to create a RAID disk array (e.g., /dev/md0).

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The array creation process will take a relatively long time. The actual duration depends on the disk size. The entire creation process does not require manual actions, but the instance cannot be Disabled or restarted. Recovering the array is much more complex than creating it for the first time.      </div>
      

      ```JSON
      sudo mdadm --create /dev/md0 --level=10 --raid-devices=4 --chunk=512 /dev/vdb /dev/vdc /dev/vdd /dev/vde
      ```
      

      > * \-\-create /dev/md0``: RAID array device name. This article uses /dev/md0 as an example.

      > * \-\-level=10``: RAID level. This article uses as an example to create RAID 10.

      > * `--raid-devices=4`: The number of EBS volumes in the RAID array. This article uses 4 EBS volumes as an example.

      > * `/dev/vd[bcde]`: Names of the disk devices participating in the creation of the array. Separate different device names with spaces.

      > * `--chunk=512`: Indicates the stripe size of the RAID array is 512 KB. Based on the workload type, the following stripe sizes are recommended:

      >    * For general\-purpose workloads, 64KB or 128KB are recommended, which in most cases can provide balanced read/write performance.

      >    * For sequential reading (such as video editing, large file transfers, etc.) workloads, larger stripe sizes such as 256KB or 512KB are recommended, which may provide better performance.

      >    * For random reading (such as database applications) workloads, smaller stripe sizes such as 32KB are recommended, which may provide better performance.

      The following output is displayed, indicating that the RAID 10 array has been successfully started.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48b7d8c1a5b1be2c05bbb0ee6f19dc78.png) </span>

         3. Execute the following command to view the RAID status.

      ```JSON
      sudo mdadm --detail /dev/md0
      ```
      

      The following output is displayed.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d23916a08cc1dce93c14ddcf3e47fec.png) </span>

4. Mount the RAID array's file system.

   1. Execute the following command to create a file system on the RAID array. In this document, the ext4 file system is used as an example. You can also create other Types of file systems.

      ```JSON
      md0
      sudo mkfs -t ext4 /dev/md0
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d32998a8d060268d3d49d9ae6312faae.png) </span>

   2. Run the following command to create a new mount directory (e.g., /mnt/raid10).

      ```JSON
      sudo mkdir /mnt/raid10
      ```
      

   3. Run the following command to mount the RAID array to the /mnt/raid10 directory.

      ```JSON
      d10
      sudo mount /dev/md0 /mnt/raid10
      ```
      

   4. View the mount results of the RAID array.

      ```JSON
      df -h
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d2c0f2f7b7c5577bd7ccaeb5716039c.png) </span>

      If the output is as shown above, it indicates a successful mount.

5. If you need to configure RAID arrays to mount automatically upon startup, refer to [Configuring Automatic Disk Partition Mount on Startup](https://docs.byteplus.com/en/docs/ecs/Allowing-disk-partitions-to-be-automatically-mounted-during-restarts).
