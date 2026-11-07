---
title: "Product Selection"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Product_Selection"
---

BytePlus offers multiple file storage products: Elastic File Storage (EFS), FileNAS, and PFS. Each file storage product suits different scenarios and has unique features. You can choose the appropriate file storage solution based on your needs.

<span id="qrtV1UTB"></span>
## Specification comparison

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">File systems across different storage types are not interoperable. For comprehensive usage restrictions regarding file systems, see the following documentation:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/nas/Usage_limits">Limits \- Elastic File Storage EFS</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/nas/Limits">Limits \- Extreme FileNAS</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/pfs/Limits">Limits \- PFS</a></div>




|**Product** |Elastic File Storage EFS ||**FileNAS** |**PFS** |||
|---|---|---|---|---|---|---|
|Specifications |Premium Tier |Basic Tier |Extreme FileNAS |100 MB/s/TiB |Performance_Edition |Intelligent_Computing_Edition |
|Applicable scenarios |* Suitable for AI training and inference scenarios, such as autonomous driving and large language model training and inference; supports file numbers up to hundreds of billions, 10 PiB storage capacity and flexible configuration performance; meets the flexible and high\-performance file storage needs of such scenarios.<br><br>* Suitable for scenarios that require high\-performance and large\-capacity elastic file storage.<br><br>* For more information, see [EFS application scenarios](https://docs.byteplus.com/en/docs/nas/Application-scenarios). ||Suitable for latency\-sensitive scenarios such as web services, file sharing, and DevOps code storage. For more information, see [FileNAS application scenarios](https://docs.byteplus.com/en/docs/nas/Application-scenarios). |Suitable for AIGC, high\-performance computing (HPC), AI training/inference, energy exploration, industrial simulation, film and television rendering, life sciences, meteorological analysis, and other scenarios. For more information, see [PFS application scenarios](https://docs.byteplus.com/en/docs/pfs/Application-scenarios). |||
|Maximum capacity of a single file system |10 PiB |10 PiB |64 TiB |200 TiB |960 TiB |19760 TiB |
|Maximum number of files/directories |* Default: 1 billion<br><br>* Maximum: 100 billion |1 billion |1 billion |The number of files and directories increases as the file system's capacity grows. Each TiB capacity supports approximately 15 million files or directories. One single file system can support up to hundreds of billions of files or directories. |||
|Maximum read throughput |min {max(125 \* storage capacity (TiB), 3), 30,000} MBps<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supports up to 2,000 GB/s.</div><br> |min {max(50 \* storage capacity (TiB), 3), 10,000} MB/s |* The maximum throughput (read/write) for the instance created on or before September 20, 2022 is 180 MB/s.<br><br>* The maximum throughput (read/write) for the instance created after September 20, 2022 is 600 MB/s. |min{100 \* storage capacity (TiB), 20,000} MBps |min{300 \* storage capacity (TiB), 230,000} MBps |* RDMA mode: min {220 \* storage capacity (TiB), 3,000,000} MB/s<br><br>* VPC mode: min {150 \* storage capacity (TiB), 2,000,000} MB/s |
|Maximum write throughput |min{max(42 \* storage capacity (TiB), 1), 10,000} MBps<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supports up to 667 GB/s.</div><br> |min {max(16.7 \* storage capacity (TiB), 1), 3,333} MB/s |||min {150 \* storage capacity (TiB), 115,000} MB/s |* RDMA mode: min{100 \* storage capacity (TiB), 1,400,000} MBps<br><br>* VPC mode: min{100 \* storage capacity (TiB), 1,400,000} MBps |
|Maximum read IOPS |min {max(3750 \* storage capacity (TiB), 90), 900,000}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 30 million supported.</div><br> |min {max (1500 \* storage capacity (TiB), 90), 15,000} |* The maximum IOPS (read/write) for the instance created on or before September 20, 2022 is 10,000.<br><br>* The maximum IOPS (read/write) for the instance created after September 20, 2022 is 50,000. |min {10,000 \* storage capacity (TiB), 1,800,000} |min {4,500 \* storage capacity (TiB), 4,000,000} |min {3,000 \* storage capacity (TiB), 45,000,000} |
|Maximum write IOPS |min {max(1250 \* storage capacity (TiB), 30), 300,000}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supports up to 10 million.</div><br> |min{max(500 \* storage capacity (TiB), 30), 5000} |||min{2000 \* storage capacity (TiB), 1,770,000} |min {1500 \* storage capacity (TiB), 22,500,000} |
|Average single\-stream 4k read latency |Sub\-millisecond |10 ms |Sub\-millisecond |Sub\-millisecond |Sub\-millisecond |Sub\-millisecond |
|Average single\-stream 4k write latency |Sub\-millisecond |10 ms |Sub\-millisecond |Sub\-millisecond |Sub\-millisecond |Sub\-millisecond |
|Client operating systems and supported protocols |Linux: FSX, NFSv4.1, NFSv3 |Linux: FSX, NFSv4.1, NFSv3 |Linux: NFSv3 |* Linux: PFS Client, FSX, NFSv3<br><br>* Windows: SMB 2.1 or later version |||


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Capacity FileNAS will be discontinued soon. As a product with similar positioning, EFS Basic type offers higher specifications and more enterprise features. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/Product_specifications">EFS Product specifications</a>.</div>


<span id="VhiWRNI5"></span>
## **Supported features**


|**Product** |<div style="text-align: center"><br>Elastic File Storage EFS</div><br> ||**FileNAS** |**PFS** |||
|---|---|---|---|---|---|---|
|Specifications |Premium Tier |Basic Tier |Extreme FileNAS |100 MB/s/TiB |Performance_Edition |Intelligent_Computing_Edition |
|**Elasticity** |||||||
|Elastic scale\-down |Supported |Supported |Not supported |Not supported |Not supported |Not supported |
|Elastic scale\-out |Supported<br><br>(step size: 4 KiB) |Supported<br><br>(step size: 4 KiB) |Supported<br><br>(step size: 1 GiB) |Supported<br><br>(step size: 2 TiB) |Supported<br><br>(step size: 8 TiB) |Supported<br><br>(step size: 80 TiB) |
|**Enterprise\-level features** |||||||
|DataFlow |Supported |Supported |Not supported |Supported |Supported |Supported |
|Baseline bandwidth mode |Supported<br><br>Based on used capacity |Supported<br><br>Based on used capacity |Not supported<br><br>Based on configured capacity range |Supported<br><br>Based on configured capacity |Supported<br><br>Based on configured capacity |Supported<br><br>Based on configured capacity |
|Provisioned bandwidth mode |Supported |Supported |Not supported |Not supported |Not supported |Not supported |
|Burst bandwidth |Supported |Supported |Not supported |Not supported |Not supported |Not supported |
|Directory quotas |Supported |Supported |Not supported |Supported |Supported |Supported |
|Directory QoS |Not supported |Not supported |Not supported |Supported |Supported |Supported |
|Access point |Supported |Supported |Not supported |Supported |Supported |Supported |
|Mount targets |Supported |Supported |Supported |Supported |Supported |Supported |
|Snapshot |Not supported |Not supported |Supported |Not supported |Not supported |Not supported |
|Data insight |Coming soon |Coming soon |Not supported |Supported |Supported |Supported |
|Audit log |Not supported |Not supported |Not supported |Supported |Supported |Supported |
