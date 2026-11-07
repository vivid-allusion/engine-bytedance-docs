---
title: "Product specifications"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Product-specifications"
---

This article introduces the performance indicators of the FileNAS.

<span id="GKUdYmEW"></span>
## Extreme FileNAS


|Attribute |Description |
|---|---|
|Bandwidth |The bandwidth increases with the growth of the file system storage capacity, with a maximum limit of 600MB/s. The specifics are as follows:<br><br><br>* [100 GiB,500 GiB)：150MB/s.<br><br>* [500 GiB,2 TiB)：300MB/s.<br><br>* [2 TiB,64 TiB)：600MB/s. |
|IOPS |The IOPS (Input/Output Operations Per Second) increase with the growth of the file system storage capacity. When the IO size is 4KiB, the specifics are as follows:<br><br>Read/Write: min{3500+30 \* capacity(GiB), 50000} |
|Latency (average latency for reading a 4KiB data block) |Sub\-millisecond level |
|Capacity |100GiB~64TiB |
|Expansion Step Size |1GiB |
|Expansion Methods |Supports manual expansion and automatic expansion |
|File Protocol Type |NFSv3 |


<span id="4uc1hTzf"></span>
## Cache FileNAS


|Category |Attribute |Description |
|---|---|---|
|Baseline performance |Throughput |* Read throughput: Min {600 + 0.1 \* storage capacity (GiB), 30,000} MBps.<br><br>* Write throughput: Capped at 10,000 MB/s. |
||IOPS |Maximum IOPS: 900,000 |
|Provisioned performance |Throughput |* Read throughput: 700 MB/s (base), incrementally scalable by 100 MB/s up to 30,000 MB/s.<br><br>* Write throughput: Capped at 10,000 MB/s. |
||IOPS |Maximum IOPS: 900,000 |
|DataFlow |Throughput |By default, the bandwidth for data flowing between FileNAS and TOS is set to 30% of the file system bandwidth. |
||Eviction |The manual/auto eviction feature has an 8,000 OPS metadata scanning capability. |
||Import |The import feature supports up to 8,000 OPS for incremental synchronization. |
|Latency |Average read latency for 4 KiB data blocks |Sub\-millisecond |
||Average write latency for 4 KiB data blocks |Sub\-millisecond |
|Capacity |Minimum provisioned capacity |0 |
||Maximum capacity |10 PiB |
||Expansion step size |4 KiB |
||Expansion method |Automatic expansion |
||Number of inodes |0 \- 1 billion |
