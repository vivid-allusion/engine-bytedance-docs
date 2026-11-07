---
title: "Data Migration"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Data-migration2"
---

This article introduces common issues during data migration for your reference.

<span id=".dG9zLeaUr-aMgeWTquS6m-i_geenu-aWueW8j--8nw=="></span>
### What migration methods does TOS support?

TOS supports migrating data to TOS through [Data Migration Service](https://docs.byteplus.com/docs/dms/What-is-data-migration-service),  tools, APIs, and SDKs.

<span id=".5LiN5ZCM6L-B56e75pa55byP6YCC55So5LuA5LmI5Zy65pmv77yf6L-B56e76LS555So5aaC5L2V6K6h566X77yf"></span>
### Which scenarios are suitable for different migration methods? How is the migration cost calculated?

The migration methods supported by TOS and their suitable data volumes are shown in the following table.


|Migration method |Recommended data volume for migration |Applicable scenario |Migration duration |Migration cost |
|---|---|---|---|---|
|API or SDK |No limit, depends on business conditions |For scenarios where new data is added daily and needs to be uploaded and migrated to TOS, integrating the API or SDK is recommended. For example, scenarios requiring regular backups of local data. |* 1 Gbps bandwidth migrates about 8 TB of data per day. The exact migration time depends on bandwidth and data volume.<br><br>* For small files (for example, less than 1 MB), calculate migration time by dividing the total number of files by the number of objects processed per second. |* **Public network migration**: Public network outbound fees from third\-party cloud providers or IDCs apply; inbound public network traffic is free.<br><br>* **ECS intranet migration**: Free of charge.<br><br>* **TOS fees**: Storage capacity and request count fees apply; refer to [request count fees](https://docs.byteplus.com/docs/tos/docs-request-fee) and [traffic fees](https://docs.byteplus.com/docs/tos/docs-traffic-fee).<br><br>* **Dedicated line migration**: No extra fees except for dedicated line charges. |
|tosutil or Rclone tools |0~100TB |* If the data to migrate is not supported by storage migration services from third\-party cloud providers, you can use Rclone for migration.<br><br>* If data is located in an IDC or file storage system, using the tosutil tool for migration is recommended to ensure better performance. |* 1 Gbps bandwidth migrates about 8 TB of data per day. The exact migration time depends on bandwidth and data volume.<br><br>* For small files (e.g., less than 1MB), migration time is recommended to be calculated by dividing the total number of files by the number of objects processed per second. |* **Public Network Migration**: Public outbound fees from third\-party cloud providers or IDC; inbound public traffic fees are free.<br><br>* **ECS Internal Network Migration**: Free.<br><br>* **TOS fees**: storage capacity and request fees. See [request count fees](https://docs.byteplus.com/docs/tos/docs-request-fee) and [traffic fees](https://docs.byteplus.com/docs/tos/docs-traffic-fee).<br><br>* **Dedicated line migration**: no additional fees except for the dedicated line charges. |
|Storage migration service or TOS Import |* Public Network Line: 0~500TB<br><br>* Dedicated Line: No limit |* Public network: Data is stored at a third\-party cloud service provider or IDC. When stored at an IDC, a public bandwidth of over 1 Gbps is available for data migration.<br><br>   If the data volume is large, it is recommended to use dedicated line migration to avoid high public network traffic costs.<br><br>* Dedicated line: When data is stored at a third\-party cloud service provider or IDC and a dedicated line is available, using the storage migration service results in the lowest cost and highest efficiency. |* With 1 Gbps bandwidth, approximately 8 TB of data can be migrated daily. Actual migration time depends on bandwidth and data volume.<br><br>* For small files (for example, smaller than 1 MB), migration time is recommended to be calculated by dividing the total number of files by the number of objects processed per second. |During data migration, API requests and data uploads/downloads incur TOS usage fees (see [request count fees](https://docs.byteplus.com/docs/tos/docs-request-fee) and [traffic fees](https://docs.byteplus.com/docs/tos/docs-traffic-fee) for details). No additional migration service fees apply. |


<span id=".5a2Y5YKo6L-B56e75pyN5Yqh5pSv5oyB6L-B56e75ZOq5Lqb5LqR5Y6C5ZWG55qE5pWw5o2u77yf"></span>
### Which cloud providers' data does Storage Migration Service support for migration?

The third\-party cloud providers supported by Storage Migration Service are listed below:


* **Alibaba Cloud**

* **Tencent Cloud**

* **Huawei Cloud**

* **Qiniu Cloud**

* **Kingsoft Cloud**

* **Other S3 Protocol Storage**: Object storage compatible with the S3 protocol and supporting AWS Signature V4 authentication.

* **Object Storage \- BytePlus**: Migrate BytePlus object storage data to TOS in the same region of BytePlus object storage.
