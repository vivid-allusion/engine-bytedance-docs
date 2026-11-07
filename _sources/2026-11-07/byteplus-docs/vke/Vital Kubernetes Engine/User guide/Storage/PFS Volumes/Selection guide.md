---
title: "Selection guide"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Model_selection_description"
---

PFS supports three access methods: FSX, PFS Client, and NFS. The recommended scenarios and performance differ among these access methods. This topic provides guidance on selecting among three access methods. Based on the following information, you can choose the most suitable method for your actual scenario.


|**Type** |**FSX** |**PFS Client** |**NFS** |
|---|---|---|---|
|Recommended scenario |* Scenarios where business operations depend on directory\-level permission management.<br><br>* The scenario where the client cache acceleration feature needs to be used.<br><br>* Scenarios where domestic operating systems are used (adapted as needed).<br><br>* The scenario where newly added nodes need to be mounted within seconds. |In scenarios where performance and availability can meet your business requirements, you can use the vePFS Client. |* The server\-side cache is expected to accelerate access to extremely hot data.<br><br>* In other scenarios where both the FSX and PFS clients cannot meet your business requirements, you can use NFS. |
|Operating system |Only Linux is supported.  |Only Linux is supported. For supported Linux operating system versions and Kernel versions, see [Constraints](https://docs.byteplus.com/en/docs/pfs/Limits). |Linux and Windows are supported (Windows is not recommended).  |
|Access protocol |Self\-developed high performance file storage protocol |Self\-developed high\-performance file storage protocol |NFSv3 |
|POSIX compatibility |Fully compatible |Fully compatible |Partially compatible |
|Single\-client performance |30 GB/s |45 GB/s |2\-3 GB/s |
|Single\-client cache performance |45 GB/s (beta) |Not supported |Not supported |
|Mount entry |Access point |Mount service |NFS protocol service |
|Client hot upgrades |Supported |Not supported |Not supported |
|Enterprise features |* Directory\-level user permissions management based on IAM<br><br>* Client cache |* Audit log<br><br>* Data insights |Server\-side cache: 8 to 128 GB/s<br><br> |
