---
title: "Multi-AZ Redundancy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-az-redundancy"
---

TOS supports multi\-AZ capability. You can use this feature to enable same\-city disaster recovery for your bucket, thereby enhancing data durability and availability. After enabling the multi\-AZ redundancy feature, TOS stores your data across three availability zones within the same region. If one availability zone experiences a failure, the remaining zones continue to provide stable storage services.

<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios

The multi\-AZ redundancy feature provides designed data durability of 99.9999999999% (twelve nines) and service availability of 99.995% for standard storage, making it suitable for scenarios with high requirements for data reliability and stability. Once enabled, if a data center experiences a failure due to extreme circumstances, other data centers can continue to provide stable storage services, thereby ensuring the stability of your business and the reliability of your data.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only the Asia Pacific (Johor) region supports multi\-AZ redundancy.

* The pricing standard for multi\-AZ redundant storage capacity is higher than that for single\-AZ storage. Once enabled, this feature cannot be disabled. Please exercise caution before enabling. For information regarding storage capacity fees for multi\-AZ redundancy, please refer to [Storage Fee](https://docs.byteplus.com/docs/tos/docs-storage-fee).


<span id=".5pSv5oyB55qE5a2Y5YKo57G75Z6L"></span>
## Supported Storage Types


|Project |Standard Storage (Multi\-AZ) |Infrequent Access Storage (Multi\-AZ) |**Intelligent Tiered Storage ** (Multi\-AZ) |**Flashback Archive** **Storage ** (Multi\-AZ) |
|---|---|---|---|---|
|Designed data durability |99.9999999999% (twelve nines) |99.9999999999% (twelve nines) |99.9999999999% (twelve nines) |99.9999999999% (twelve nines) |
|Service Availability |99.995% |99.5% |The access level is identical to that of the conversion object. |99.5% |
|Minimum measurement unit |None |64KiB |None |64KiB |
|Minimum storage duration |None |30 days |None |90 days |
|Storage Fees |Standard |Lower |It is determined by the access frequency of the object. |Lower |
|Request Fees |Standard |Relatively high |The costs are relatively high, and object monitoring fees must also be charged. |Relatively high |
|Data Retrieval Fees |None |Charges are based on the actual amount of data obtained, measured in GiB. |None |Charges are based on the actual amount of data obtained, measured in GiB. |
|Characteristics of Data Access |Real\-time access with millisecond latency. |Real\-time access with millisecond latency. |Real\-time access with millisecond latency. |Real\-time access with millisecond latency. |
|Storage Type Parameter Values |STANDARD |IA |INTELLIGENT_TIERING |ARCHIVE_FR |


<span id=".5L2_55So5aSaLWF6LeWGl-S9mQ=="></span>
## Utilize multi\-Availability Zone redundancy

You can enable the multi\-AZ redundancy feature when creating a storage bucket. Subsequently, when uploading files to this bucket, select the multi\-AZ storage type.


1. Enable the multi\-AZ redundancy feature.

   Currently, TOS only supports enabling multi\-AZ redundancy when creating a bucket. For detailed instructions, see [Creating a Bucket](https://docs.byteplus.com/docs/tos/docs-create-a-bucket).

2. Upload file.

   When uploading files to a bucket with multi\-AZ redundancy enabled, you can choose to inherit the bucket's storage type, or select Standard Storage (multi\-AZ), Intelligent Tiered Storage (multi\-AZ), Infrequent Access Storage (multi\-AZ), or Flashback Archive(multi\-AZ) as the storage type. For detailed instructions, please refer to [Upload File](https://docs.byteplus.com/docs/tos/docs-uploading-a-file).


<span id=".5YW25LuW5pON5L2c"></span>
## Other Operations

After enabling the multi\-AZ redundancy feature, you can perform the following operations in the storage bucket:


|**Operation** |**Description** |
|---|---|
|View the redundancy type of the storage bucket |You can view the redundancy type of a storage bucket on the **Buckets** page. Alternatively, you can check whether the storage bucket has enabled the multi\-AZ redundancy feature in the **Basic information** section of the **Overview** page. For specific operations, see [View Bucket Overview](https://docs.byteplus.com/docs/tos/docs-bucket-overview). |
|View File Storage Types |You can view the storage type of a file in either the File List panel or the Basic Information panel. |
|Modify File Storage Type |When modifying the storage type of a file, you can select from Standard Storage (Multi\-AZ), Intelligent Tiered (Multi\-AZ), Infrequent Access Storage (Multi\-AZ), or Flashback Archive  (Multi\-AZ) storage types. For detailed instructions, see [Modify File Storage Type](https://docs.byteplus.com/docs/tos/docs-changing-the-file-storage-type). |
|Configure Lifecycle Rules |Supports moving and storing both the latest and historical versions of files in Infrequent Access Storage (multi\-AZ), intelligent tiered (multi\-AZ), and Flashback Archive(multi\-AZ) storage types. For specific instructions, please refer to [Set Lifecycle Rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules). |
|Move File |Files in single\-AZ and multi\-AZ storage buckets can be moved between these buckets. After a file is moved to a single\-AZ storage bucket, it becomes a single\-AZ file. After being moved to a multi\-AZ bucket, the file becomes a multi\-AZ file. For detailed instructions, please refer to [Moving Files](https://docs.byteplus.com/docs/tos/docs-moving-files). |
|Intra\-Region File Replication |Files stored in single AZ buckets and multi AZ buckets support mutual replication within the same region. After replication to a single AZ bucket, the file becomes a single AZ file. After replication to a multi AZ bucket, the file becomes a multi AZ file. For detailed instructions, see [Copying Files](https://docs.byteplus.com/docs/tos/docs-copying-files). |
|Cross\-Regional File Replication |Files in single\-AZ buckets and multi\-AZ buckets support mutual cross\-region replication between each other. When a file is replicated to a single\-AZ bucket, it becomes a single\-AZ file; when replicated to a multi\-AZ bucket, it becomes a multi\-AZ file. For detailed instructions, refer to [Cross-Region Replication](https://docs.byteplus.com/docs/tos/Cross-regional-replication-within-the-same-account). |
