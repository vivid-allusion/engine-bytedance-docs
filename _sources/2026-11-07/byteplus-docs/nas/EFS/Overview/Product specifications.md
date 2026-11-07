---
title: "Product specifications"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Product_specifications"
---

This topic describes the product specifications of Elastic File Storage (EFS).

<span id="ofVWyky0"></span>
## Features

To meet different file storage needs, EFS offers two types of file system specifications: Premium Tier and Basic Tier.


|Specifications |Features |Application scenarios |
|---|---|---|
|Premium Tier |Premium Tier features ultra\-large capacity and file count limits, ultra\-high bandwidth and IOPS, as well as ultra\-low latency, delivering robust support for AI training & inference and enterprise\-critical services. |* It is primarily tailored for AI training and inference scenarios, such as autonomous driving and large language model training & inference. With support for hundreds of billions of files, up to 10 PiB of storage capacity, and flexibly configurable performance, it satisfies the diverse and high\-performance file storage demands of such scenarios.<br><br>* It supports standard NFSv4.1 and NFSv3 protocols, meeting the needs of traditional businesses for high\-performance shared file storage (e.g., performance\-optimized NAS). |
|Basic Tier |The Base Tier offers ultra\-large capacity, providing ultimate cost\-effectiveness for massive file storage requirements. |It adopts standard NFSv4.1 and NFSv3 protocols to fulfill traditional business demands for large\-capacity shared file storage (e.g., capacity\-optimized NAS). |


<span id="98XtnYsW"></span>
## Specifications


|Category |Type |Premium Tier |**Basic ** Tier |
|---|---|---|---|
|Scenarios |Recommended scenarios |AI training and inference; general high\-performance file storage (such as performance\-optimized NAS) |General large\-scale file storage (such as capacity\-optimized NAS) |
|Specifications |Features |Ultra\-large capacity and file counts; ultra\-high performance |Ultra\-large capacity; high cost\-effectiveness |
|Capacity |Storage capacity |0 ~ 10PiB |0 ~ 10PiB |
||Scaling granularity |Elastic scaling |Elastic scaling |
||Scaling granularity |4 KiB |4 KiB |
||Maximum number of files |Defaults to 1 billion; supports up to 100 billion |1 billion |
|Basic performance |Performance density |125MB/s/TiB |50 MB/s/TiB |
||Average latency of 4 KiB data blocks |Sub\-millisecond |10 ms |
|Baseline bandwidth mode |Throughput |* 100% read limit: 30 GB/s<br><br>* 100% write limit: 10 GB/s |* 100% read limit: 10 GB/s<br><br>* 100% write limit: 3.3 GB/s |
||IOPS |* 100% read limit: 900,000<br><br>* 100% write limit: 300,000 |* 100% read limit: 15,000<br><br>* 100% write limit: 5,000 |
|Provisioned bandwidth mode |Throughput |* 100% read limit: defaults to 60 GB/s; supports up to 2 TB/s.<br><br>* 100% write limit: defaults to 20 GB/s; supports up to 667 GB/s. |* 100% read limit: 10 GB/s<br><br>* 100% write limit: 3.3 GB/s |
||IOPS |* 100% read limit: defaults to 1,800,000; supports up to 30 million<br><br>* 100% write limit: defaults to 600,000; supports up to 10 million |* 100% read limit: 15,000<br><br>* 100% write limit: 5,000 |
|Burst bandwidth |Throughput |* 100% read limit: defaults to 60 GB/s; supports up to 200 GB/s<br><br>* 100% write limit: defaults to 20 GB/s; supports up to 67 GB/s |* 100% read limit: 10 GB/s<br><br>* 100% write limit: 3.3 GB/s |
||IOPS |* 100% read limit: defaults to 1,800,000; supports up to 6,000,000<br><br>* 100% write limit: defaults to 600,000; supports up to 2,000,000 |* 100% read limit: 15,000<br><br>* 100% write limit: 5,000 |


<span id="9scxJ4ka"></span>
## Supported access methods


|Client |Protocol type |Premium Tier |**Basic ** Tier |Application scenarios |
|---|---|---|---|---|
|FSX |Proprietary high\-performance access protocol |Supported |Supported |FSX is the recommended access method for AI training and inference scenarios. When accessing EFS file system instances, the single\-client throughput of FSX can reach up to 8 GB/s, scaling to 45 GB/s with client\-side caching enabled.<br><br>MLP (Machine Learning Platform) and VKE (Container Service) have already integrated FSX. EFS’s deep integration with MLP and VKE enables end\-to\-end solutions for AI training and inference scenarios, accelerating business deployment. For usage limits of the FSX client, see [Usage limits](https://docs.byteplus.com/en/docs/nas/efs_FSX_overview#K0WB9pCP). |
|NFS |NFSv4.1 |Supported |Supported |As the default access method for traditional workloads, NFS offers broad compatibility. When accessing an EFS file system instance, NFS provides single\-client throughput of approximately 2 GB/s, with no support for client\-side caching.<br><br>MLP and VKE have already integrated NFS, allowing EFS to seamlessly work with both services. |
||NFSv3 |Supported |Supported ||


<span id="XkPQJYpE"></span>
## Supported features


|Features |Premium Tier |**Basic ** Tier |
|---|---|---|
|Baseline bandwidth mode |Supported |Supported |
|Provisioned bandwidth mode |Supported |Supported |
|Burst bandwidth |Supported |Supported |
|Access point |Supported |Supported |
|Mount target |Supported |Supported |
|Directory quota |Supported |Supported |
|Monitoring alarm |Supported |Supported |
|Permission group |Supported |Supported |
