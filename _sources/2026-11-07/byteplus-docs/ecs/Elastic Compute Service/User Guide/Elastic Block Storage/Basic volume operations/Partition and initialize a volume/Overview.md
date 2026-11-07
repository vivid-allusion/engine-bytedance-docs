---
title: "Overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview"
---

When you create a volume and mount it on an Elastic Compute Service (ECS) instance, you need to partition and format it before you can use it. This topic describes operations that can be used to partition and format a new data volume. If the volume already contains data from a data source, these operations can lead to data loss.

<span id="precautions"></span>
## Precautions

ECS allows you to partition a data volume. Do not partition and format a system volume. When you create an ECS instance, a system volume is automatically generated, partitioned, and formatted. The default partitioning format of a volume is Master Boot Record (MBR). If you forcibly use a third\-party utility to partition a system volume, unexpected issues, such as system crashes or data loss can occur. You can expand a partition on the system volume or add a partition to the volume after you expand the volume.

<span id="operation-scenario"></span>
## Operation scenario


* If your hard disk is displayed as 1 separate partition, do not partition the disk. Build your file system directly on the raw device. For information on the related steps, refer to [Create a file system on raw devices](https://docs.byteplus.com/en/docs/ecs/Create-a-file-system-on-raw-devices).

* If you want to display your hard disk as multiple logical partitions or have multiple logical disks, you can partition the hard disk and then create a file system for each partition.

   
   |Partitioning Format |Description |Utility |Related Document |
   |---|---|---|---|
   |MBR |MBR<br><br>can recognize a partition less than or equal to 2 TiB and allows you to create up to 4 partitions. |* Windows: Disk Management<br><br>* Linux: the fdisk utility and parted utility |[Partition and initialize a volume less than or equal to 2 TiB](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB) |
   |GPT |GUID Partition Table (GPT)<br><br>can recognize a partition larger than 2 TiB and allows you to create partitions as needed. |* Windows: Disk Management<br><br>* Linux: parted utility |[Partition and initialize a volume larger than 2 TiB](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-larger-than-2-TiB) |
