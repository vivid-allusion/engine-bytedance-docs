---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DevMind-log-Overview"
---

Log analysis is a visual analytics module of DevMind. Based on TOS bucket access logs, this module provides insights into resource usage, access behavior, request sources, and security posture. This topic describes the entry point, visualization dimensions, filter conditions, and meaning of each metric.

<span id="cfXZZAMM"></span>
## Prerequisites

Before using log analysis, make sure you have completed the following:


* You have activated Torch Log Service (TLS).

* You have authorized TOS to access TLS. If your account is authorized, no additional authorization requests are needed.


<span id="BCPz3lSo"></span>
## Notes


* Once log analysis is enabled, TLS automatically creates projects and topics to store TOS\-related logs.

* In the TLS console, you can modify the configurations for projects, topics, and indexes created via the logging feature of TOS. However, please note that such modifications may cause abnormalities in the logging feature and are therefore not recommended.


<span id="9V8IjuN9"></span>
## Billing notes


|Scenario |Billable items |Billed by |Related documentation |
|---|---|---|---|
|Enabling log analysis |Log storage, index storage, write traffic, index traffic, service requests, and log shards. |TLS |[Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce) |
|Operations such as processing, shipping, or consuming data in TOS\-related topics |Network read traffic, public network read traffic, data processing traffic, and data shipping traffic. |||


<span id="AcmPhCIX"></span>
## Introduction

Log analysis provides the following capabilities. Switch between them using the tabs at the top of the page. All tabs support filtering by region and bucket. You can flexibly combine filter conditions based on your needs to view analysis results for the corresponding dimensions.


|Capability |Description |
|---|---|
|Resource Usage |Resource Usage displays real\-time trends in reads, writes, traffic, and total traffic and requests. It also provides the top 1,000 buckets, which are ranked by traffic and requests. This helps you understand your overall bandwidth and resource consumption, as well as hotspot distribution. For more information, see [Resource usage](https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard). |
|Heat Statistics |Heat Statistics analyzes access hotness from multiple dimensions, including operation type, object size distribution, queries per second (QPS), read/write ratio, directory, and prefix. This helps you identify hot operations, buckets, directories, and prefixes, allowing you to optimize capacity and performance. For more information, see [Heat statistics](https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard). |
|Access Analysis |Access Analysis is based on five core metrics: uploaded data volume, downloaded data volume, deleted data volume, page views (PV), and unique visitors (UV). It displays totals and period\-over\-period change changes, as well as details on the top 1,000 by bucket and referrer. These features help you quickly identify hotspots and request source distribution. For more information, see [Access analysis](https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard). |
|Security Analysis |Security Analysis focuses on object\-level operations. It visualizes trends and details of object deletion operations, such as HeadObject, DeleteObject, and UploadPart, organized by bucket and request IP address. This helps you identify security risks, such as abnormal deletions and batch operations. For more information, see [Security analysis](https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard). |
|Query and Analysis |Query and Analysis lets you filter log data using SQL statements. Three views are provided: a time\-series histogram, raw logs, and log clustering and chart analysis. You can also filter by index fields, export data, and use the log interpretation assistant to quickly examine the details of individual requests and troubleshoot abnormal access. For more information, see [Query and analysis](https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard). |


<span id="ZrwxNxll"></span>
## Log fields


|**Field name** |**Example value** |**Description** |
|---|---|---|
|LogType |tos_access_log |The log type for TOS is `tos_access_log`. |
|Time |2022\-05\-14T16:15:09+08:00 |The time when TOS received the request. |
|RequestId |xxxxxxxxxxxx\-xxxxxxxx\-xxxxxx\-LB\-cb\-1AZ\-F\-LFRZ\-B\-K2\-1 |The request ID. |
|Bucket |test |The name of the bucket. |
|Object |object1 |The key of the requested object. |
|ObjectSize |1164596 |The size of the requested object, measured in bytes. |
|VersionId |102332212244 |The version ID of the requested object. |
|Operation |PutObject |The type of the operation. |
|RemoteIp |192.168.0.1 |The source IP address of the request. |
|BucketLocation |cn\-beijing |The region where the bucket is located. |
|StorageClass |STANDARD |The storage type of the bucket. The details are as follows:<br><br><br>* STANDARD: Standard Storage.<br><br>* IA: Infrequent Access Storage.<br><br>* ARCHIVE_FR: Flashback Archive.<br><br>* ARCHIVE: Archive.<br><br>* COLD_ARCHIVE: Cold Archive.<br><br>* DEEP_COLD_ARCHIVE: Deep Cold Archive. |
|Host |test.tos\-cn\-beijing.volces.com |The domain name accessed by the request. |
|HTTPMethod |PUT |The HTTP request method. |
|HTTPStatus |200 |The HTTP status code returned for the request. |
|HTTPSchema |https |The protocol of the HTTP request, including HTTP and HTTPS. |
|RequestSize |1164596 |The value of `Content-Length` in request header, measured in bytes. |
|ResponseSize |0 |The value of `Content-Length` in response header, measured in bytes. |
|DeltaDataSize |1164596 |Indicates changes in the total data size in bytes caused by the request. The details are as follows:<br><br><br>* A positive value means the request increased the total data size. Operations such as uploading objects increase the total data size.<br><br>* A negative value means the request reduced the total data size. Operations such as permanently deleting an object reduce the total data size. |
|HistoricalVersionDeltaSize |209351 |Indicates changes in size of historical object versions in bytes caused by the request. The details are as follows:<br><br><br>* A positive value means the request increased the size of historical object versions. In a versioning\-enabled bucket, overwriting objects during upload or adding deletion marks increases the size of historical object versions.<br><br>* A negative value means the request reduced the size of historical object versions. Operations that reduce the size of historical version objects include deleting a delete marker when no latest version of the object exists and permanently deleting a historical object version.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can calculate the changes in size of latest object versions using the formula below:</div><br><br><br><div data-tips="true" data-tips-type="tip">Changes in size of latest object versions = DeltaDataSize \- HistoricalVersionDeltaSize</div><br> |
|RequestUri |/fdgfdgsf?acl |The URI of the HTTP request, including the `query-string`. |
|CostTime |12 |The time it takes the TOS server to process the request, measured in milliseconds. |
|UserAgent |curl/7.15.5 |The HTTP `User-Agent` header. |
|Referer |x.example.com |The `HTTP Referer` of the request. |
|OwnerId |200000xxxx |The account ID of the bucket owner. |
|RequesterId |200000xxxx |The account ID of the requester. For anonymous access, this is displayed as a hyphen (\-). |
|AccessKeyId |AKTP07cMTfZg0nvA3R1I194IY8SVyUjl5Yxxxx |The access key ID of the requester. |
|RequesterUserName |user1 |The username of the requester. |
|RequestSourceType |cdn |The type of the synchronous request. The details are as follows:<br><br><br>* Hyphen (\-): Regular request.<br><br>* cdn: CDN back\-to\-origin request.<br><br>* crr\-sync: Cross\-region replication request.<br><br>* lifecycle: Lifecycle request.<br><br>* accelerate: Transfer acceleration request. |
|ErrorCode |NoSuchBucket |The error code returned by TOS. |
|ReservedFiled |`-` |Reserved field, displayed as "\-". |
|MirrorSourceStatus |0 |The status code returned by the origin server in back\-to\-origin scenarios. |
|ECCode |0010\-00000021 |The EC error code. |
|RespTime |35 |Response time, which refers to the time it takes to respond with the first byte after receiving a request, measured in milliseconds. |
|TrashPath |.Trash/20250912023000/tree.png |The path of a deleted object in Recycle Bin if the Recycle Bin feature is enabled for an HNS bucket. |
|MRAPAlias |m941ea886xxxx\-mrap |The alias of a multi\-region access point. |
|MRAPDstEndpoint |arctic.tos\-cn\-beijing.volces.com |The endpoint of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MRAPDstRegion |cn\-beijing |The region of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MRAPDstBucket |DstBucket |The name of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MRAPSrcRegion |cn\-shanghai |The source region to which the request was routed when a user accessed TOS via a multi\-region access point. |
|MRAPSrcBucket |SrcBucket |The source bucket to which the request was routed when a user accessed TOS via a multi\-region access point. |
|StorageTier |INFREQUENT |The access tier of Intelligent Tiering in which the object is stored. The details are as follows:<br><br><br>* FREQUENT: Intelligent Tiering frequent access tier.<br><br>* INFREQUENT: Intelligent Tiering infrequent access tier.<br><br>* ARCHIVEFR: Intelligent Tiering flashback archive tier. |
|Payer |BucketOwner |The payer for the request. The details are as follows:<br><br><br>* BucketOwner: The bucket owner paid.<br><br>* Requester: The requester paid. |
|TargetStorageClass |ARCHIVE_FR |The storage type of the target object. This field is only returned when the Operation value is TransferObject or CopyObject. The details are as follows:<br><br><br>* If the Operation value is TransferObject, the TargetStorageClass value indicates the storage type to which the object transitioned under a lifecycle rule.<br><br>* If the Operation value is CopyObject, the TargetStorageClass value specifies the storage type of the new object after it is copied. |


<span id="xciGiyCM"></span>
## Kanban configuration

The Kanban configuration tab lets you enable and manage log analysis for all buckets under your account. With it, you can enable or disable log collection for buckets in batches, configure authorization, and view the status. The following table describes the fields and operations on the Kanban configuration tab.


|Field/Operation |Description |
|---|---|
|Top information bar |Displays the total number of buckets under your account.<br><br>Once log analysis is enabled for a bucket, its access logs are collected in real time. This provides capabilities for usage analytics, request analytics, security analytics, and querying. However, log collection, storage, and querying incur charges from TLS. For more information, see [Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce). |
|Search box |Allows you to search for buckets by name to quickly locate a specific one. |
|Bucket name |The unique identifier of the bucket. |
|Region |The region where the bucket resides. |
|Log analysis switch |The switch is per bucket. When it is turned on, access logs are collected and TLS charges apply. When the switch is turned off, no new logs are generated, but historical logs are retained according to TLS lifecycle rules. |
|To analyze |A bucket with log analysis enabled has a **To analyze** link that leads to the Query and Analysis tab. |
