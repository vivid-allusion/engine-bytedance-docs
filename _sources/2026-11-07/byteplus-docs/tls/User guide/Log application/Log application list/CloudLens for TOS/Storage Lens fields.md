---
title: "Storage Lens fields"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Data-pivot-fields"
---

This topic describes the log fields for the storage lens feature.

The following are detailed descriptions of the log fields generated after creating a storage lens task. For details on configuring the storage lens dashboard, please see  [Configure pivot dashboard](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard).

<span id="c3adf3bc"></span>
## tos\-lens\-topic (log topic) field description

Stores the result metrics of basic summary statistics and prefix statistics tasks.


|Name |Type |Description |
|---|---|---|
|Accountld |text |Account ID. |
|AdditionalFilter |long |Reserved field, not currently used. |
|Bucket |text |Bucket name of the object storage bucket. |
|Configld |text |Storage Lens dashboard ID. |
|Date |long |Metric date, in seconds as a timestamp. |
|Dimension |text |Grouped statistics by the following dimensions.<br><br><br>* Bucket: bucket dimension<br><br>* Prefix: prefix dimension |
|DimensionValue |text |Value of the grouped statistics.<br><br><br>* When Dimension is Bucket: empty.<br><br>* When Dimension is Prefix: prefix value. |
|LogType |text |Reserved field, not currently used. |
|Metric |text |Metric type.<br><br><br>* Total storage: StorageBytes<br><br>* Total object count: ObjectCount<br><br>* Current version bytes: CurrentVersionStorageBytes<br><br>* Current version object count: CurrentVersionObjectCount<br><br>* Historical version bytes: NonCurrentVersionStorageBytes<br><br>* Historical version object count: NonCurrentVersionObjectCount<br><br>* Unmerged multipart upload bytes: IncompleteMultipartUploadStorageBytes<br><br>* Unmerged multipart upload object count: IncompleteMultipartUploadObjectCount<br><br>* Deleted bytes *: * DeleteStorageBytes<br><br>* Uploaded bytes: AddStorageBytes |
|MetricValue |double |Statistical value of the metric.<br><br>If Metric is StorageBytes, then MetricValue is the storage capacity of the bucket. |
|Region |text |Region information where the bucket is located. |
|StorageClass |text |Object storage type.<br><br><br>* Deep cold archive: DEEP_COLD_ARCHIVE<br><br>* Infrequent access storage: STANDARD_IA<br><br>* Standard storage: STANDARD<br><br>* Archive flash recovery: ARCHIVE_FR<br><br>* Cold archive: COLD_ARCHIVE<br><br>* Archive: ARCHIVE<br><br>* Intelligent tiering: INTELLIGENT_TIERING |


<span id="ddacd3a4"></span>
## Object storage bucket name (table topic) field description

Stores process data metrics for prefix statistics tasks.


|Name |Type |Description |
|---|---|---|
|Region |String |Region information where the bucket is located. |
|BucketName |String |Bucket name of the object storage bucket. |
|Accountld |String |Account ID. |
|ObjectName |String |Object name. |
|StorageClass |String |Object storage type.<br><br><br>* Deep cold archive: DEEP_COLD_ARCHIVE<br><br>* Infrequent access storage: STANDARD_IA<br><br>* Standard storage: STANDARD<br><br>* Archive flash recovery *: * ARCHIVE_FR<br><br>* Cold archive: COLD_ARCHIVE<br><br>* Archive: ARCHIVE<br><br>* Intelligent tiering: INTELLIGENT_TIERING |
|Versionld |String |Version number of the requested object. |
|StorageBytes |Int64 |Object size. |
|CurrentVersion |Int64 |Version information of the object.<br><br><br>* 0: historical version<br><br>* 1: current version |
|LastModified Time |Int64 |Last modification time of the object. |
