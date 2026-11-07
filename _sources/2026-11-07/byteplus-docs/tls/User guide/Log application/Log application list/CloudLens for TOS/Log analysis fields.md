---
title: "Log analysis fields"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Log-analysis-fields"
---

This document describes the access log fields for the log analysis feature.

The following fields are generated during TOS access. Before using the log analysis feature, you need to configure the log analysis dashboard. For details, see [Configure a log analysis dashboard](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard). Alternatively, enable the log analysis feature in the object storage service. For details, see [Log analysis](https://docs.byteplus.com/en/docs/tos/Log-analysis).

<span id="c3adf3bc"></span>
## TOS access log (`tos-log-topic`) field descriptions


|Name |Type |Description |
|---|---|---|
|AccessKeyld |text |Account ID. |
|Bucket |text |Object storage bucket name. |
|BucketLocation |text |The region where the object storage bucket is located. |
|CostTime |long |The time taken by the object storage server to process this request, in milliseconds. |
|DeltaDataSize |long |The change in storage size caused by the request, in bytes. Details are as follows:<br><br><br>* A positive value means the request increased the total data size. Operations such as uploading objects increase the total data size.<br><br>* A negative value means the request reduced the total data size. Operations such as permanently deleting an object reduce the total data size. |
|ECCode |text |The EC error code. |
|ErrorCode |text |Error code returned by object storage. |
|HTTPMethod |text |The HTTP request method. |
|HTTPSchema |text |The protocol of the HTTP request, including HTTP and HTTPS. |
|HTTPStatus |long |The HTTP status code returned for the request. |
|HistoricalVersionDeltaSize |long |The change in storage size for historical version objects (bytes) caused by the request. Details are as follows:<br><br><br>* A positive value means the request increased the size of historical object versions. In a versioning\-enabled bucket, overwriting objects during upload or adding deletion marks increases the size of historical object versions.<br><br>* A negative value means the request reduced the size of historical object versions. Operations that reduce the size of historical version objects include deleting a delete marker when no latest version of the object exists and permanently deleting a historical object version.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">You can calculate the change in storage capacity for the latest version of the object caused by the request using DeltaDataSize and HistoricalVersionDeltaSize. The calculation formula is as follows:</div><br><br><br><div data-tips="true" data-tips-type="default">Change in storage capacity for the latest version of the object = DeltaDataSize \- HistoricalVersionDeltaSize</div><br> |
|Host |text |The domain name accessed by the request. |
|LogType |text |Log type. |
|MRAPAlias |text |The alias of a multi\-region access point. |
|MRAPDstBucket |text |The name of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MirrorSourceStatus |long |The status code returned by the origin server in back\-to\-origin scenarios. |
|Object |text |Key of the requested object. |
|ObjectSize |long |Size of the requested object. measured in bytes. |
|Operation |text |The type of the action. |
|Ownerld |text |Account ID to which the object belongs. |
|Referer |text |The HTTP Referer of the request. |
|Remotelp |text |Client IP of the request. |
|Requestld |text |The request ID. |
|RequestSize |long |The value of Content\-Length in request header, measured in bytes. |
|RequestSourceType |text |Synchronous request type.<br><br><br>* Hyphen (\-): Regular request.<br><br>* cdn: CDN back\-to\-origin request.<br><br>* crr\-sync: Cross\-region replication request.<br><br>* lifecycle: Lifecycle rule.<br><br>* accelerate: Transfer acceleration request. |
|RequestUri |text |The URI of the HTTP request, including query\-string. |
|Requesterld |text |The ID of the requester. |
|RequesterUserName |text |The username of the requester. |
|ReservedFiled |text |Reserved field, displayed as "\-". |
|RespTime |long |Response time, which refers to the time it takes to respond with the first byte after receiving a request, measured in milliseconds. |
|ResponseSize |long |The value of Content\-Length in response header, measured in bytes. |
|StorageClass |text |The storage class of the object storage bucket.<br><br><br>* STANDARD: Standard Storage<br><br>* IA: Infrequent access storage.<br><br>* ARCHIVE_FR: Flashback Archive.<br><br>* ARCHIVE: Archive storage.<br><br>* COLD_ARCHIVE: Cold Archive.<br><br>* DEEP_COLD_ARCHIVE: Deep Cold Archive. |
|Time |text |The time when TOS received the request. |
|UserAgent |text |The HTTP User\-Agent header. |
|Versionld |text |The version number of the requested object. |
