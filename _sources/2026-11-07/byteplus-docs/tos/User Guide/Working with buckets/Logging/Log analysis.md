---
title: "Log analysis"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Log-analysis"
---

TOS offers log analysis capabilities through BytePlus Torch Log Service (TLS). This feature enables you to search and analyze access logs generated from your interactions with TOS. This topic outlines the prerequisites and steps for using the log analysis feature.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

For more information on TLS, see [What is Torch Log Service](https://docs.byteplus.com/en/docs/tls/What_is_TLS).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before using log analysis, make sure you have completed the following:


* You have activated TLS.

* You have authorized TOS to access TLS. If your account is authorized, no additional authorization requests are needed.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Once log analysis is enabled, TLS automatically creates projects and topics to store TOS\-related logs.

* In the TLS console, you can modify the configurations for projects, topics, and indexes created via the logging feature of TOS. However, please note that such modifications may cause abnormalities in the logging feature and are therefore not recommended.


<span id="7182c390"></span>
## Billing notes


* Enabling log analysis incurs charges for log storage, index storage, write traffic, index traffic, service requests, log shards, etc. TLS bills these charges separately. For billing details, see [TLS Billing overview](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode).

* Operations such as processing, shipping, or consuming logs on TOS\-specific topics incur additional fees. These fees are associated with network read traffic, public network read traffic, data processing traffic, and data shipping traffic, and are billed separately by TLS. For billing details, see [TLS Billing overview](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode).


<span id=".6K6_6Zeu5pel5b-X5a2X5q616K-05piO"></span>
## Log field description


|**Field name** |**Example value** |**Description** |
|---|---|---|
|LogType |tos_access_log |The log type for TOS is `tos_access_log`. |
|Time |2022\-05\-14T16:15:09+08:00 |The time when TOS received the request. |
|RequestId |851301791455779965791455\-ac147c52\-1rDEov\-LB\-cb\-1AZ\-F\-LFRZ\-B\-K2\-1 |The request ID. |
|Bucket |test |The name of the bucket being reported. |
|Object |object1 |The key of the requested object. |
|ObjectSize |1164596 |The size of the requested object, measured in bytes. |
|VersionId |102332212244 |The version ID of the requested object. |
|Operation |PutObject |The type of the operation. |
|RemoteIp |192.168.0.1 |The source IP address of the request. |
|BucketLocation |cn\-beijing |The region where the bucket is located. |
|StorageClass |STANDARD |The storage type of the bucket. The details are as follows:<br><br><br>* STANDARD: Standard Storage<br><br>* IA: Infrequent Access Storage.<br><br>* ARCHIVE_FR: Flashback Archive.<br><br>* ARCHIVE: Archive.<br><br>* COLD_ARCHIVE: Cold Archive.<br><br>* DEEP_COLD_ARCHIVE: Deep Cold Archive. |
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
|Referer |\*.example.com |The `HTTP Referer` of the request. |
|OwnerId |200000\*\*\*\* |The account ID of the bucket owner. |
|RequesterId |200000\*\*\*\* |The account ID of the requester. For anonymous access, this is displayed as a hyphen (\-). |
|AccessKeyId |AKTP07cMTfZg0nvA3R1I194IY8SVyUjl5Y\*\*\*\* |The access key ID of the requester. |
|RequesterUserName |user1 |The username of the requester. |
|RequestSourceType |cdn |The type of the synchronous request. The details are as follows:<br><br><br>* Hyphen (\-): Regular request.<br><br>* cdn: CDN back\-to\-origin request.<br><br>* crr\-sync: Cross\-region replication request.<br><br>* lifecycle: Lifecycle request.<br><br>* accelerate: Transfer acceleration request. |
|ErrorCode |NoSuchBucket |The error code returned by TOS. |
|ReservedFiled |`-` |Reserved field, displayed as "\-". |
|MirrorSourceStatus |0 |The status code returned by the origin server in back\-to\-origin scenarios. |
|ECCode |0010\-00000021 |The EC error code. |
|RespTime |35 |Response time, which refers to the time it takes to respond with the first byte after receiving a request, measured in milliseconds. |
|TrashPath |.Trash/20250912023000/tree.png |The path of a deleted object in Recycle Bin if the Recycle Bin feature is enabled for an HNS bucket. |
|MRAPAlias |m941ea886\*\*\*\*\-mrap |The alias of a multi\-region access point. |
|MRAPDstEndpoint |arctic.tos\-cn\-beijing.volces.com |The endpoint of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MRAPDstRegion |cn\-beijing |The region of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MRAPDstBucket |DstBucket |The name of the bucket from which TOS retrieved an object when a user accessed TOS via a multi\-region access point and requested an object that was not in the source bucket. |
|MRAPSrcRegion |cn\-shanghai |The source region to which the request was routed when a user accessed TOS via a multi\-region access point. |
|MRAPSrcBucket |SrcBucket |The source bucket to which the request was routed when a user accessed TOS via a multi\-region access point. |
|StorageTier |INFREQUENT |The access tier of Intelligent Tiering in which the object is stored. The details are as follows:<br><br><br>* FREQUENT: Intelligent Tiering frequent access tier.<br><br>* INFREQUENT: Intelligent Tiering infrequent access tier.<br><br>* ARCHIVEFR: Intelligent Tiering flashback archive tier. |
|Payer |BucketOwner |The payer for the request. The details are as follows:<br><br><br>* BucketOwner: The bucket owner paid.<br><br>* Requester: The requester paid. |
|TargetStorageClass |ARCHIVE_FR |The storage type of the target object. This field is only returned when the Operation value is TransferObject or CopyObject. The details are as follows:<br><br><br>* If the Operation value is TransferObject, the TargetStorageClass value indicates the storage type to which the object transitioned under a lifecycle rule.<br><br>* If the Operation value is CopyObject, the TargetStorageClass value specifies the storage type of the new object after it is copied. |


<span id=".5byA5ZCv5pel5b-X5YiG5p6Q"></span>
## Enabling log analysis

This section describes how to enable log analysis when creating a bucket or for an existing one.

<span id=".5Yib5bu65a2Y5YKo5qG25pe25byA5ZCv5pel5b-X5YiG5p6Q"></span>
### Enabling log analysis when creating a bucket


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**. Then, in the upper\-left corner of the displayed page, click **Create bucket**.

3. On the **Create bucket** page, expand **Advanced settings**, and turn on the **Log analysis** switch.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on other parameters when creating a bucket, see <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Creating buckets</a>.   </div>
   

4. Click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After enabling log analysis, you can search and analyze TOS access logs on the <strong>Search Analysis</strong> tab of the <strong>Logging</strong> page. Learn more in <a href="https://docs.byteplus.com/en/docs/tls/getting_started_query_and_analyze_logs">Query and analyze logs</a>.   </div>
   

<span id=".5Li65bey5Yib5bu655qE5a2Y5YKo5qG25byA5ZCv5pel5b-X566h55CG"></span>
### Enabling log analysis for an existing bucket


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, click **Logging**. Then, on the **Log analysis** tab, click **Edit**.

6. Turn on the switch and click **Select**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After enabling log analysis, you can search and analyze TOS access logs on the <strong>Search Analysis</strong> tab of the <strong>Logging</strong> page. Learn more in <a href="https://docs.byteplus.com/en/docs/tls/getting_started_query_and_analyze_logs">Query and analyze logs</a>.   </div>
   

<span id=".5YWz6Zet5pel5b-X5YiG5p6Q"></span>
## Disabling log analysis

You can disable the log analysis feature if you no longer need to view TOS log information. This section describes how to disable log analysis.

**Steps**


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, click **Logging**. Then, on the **Log analysis** tab, click **Disable associated logging**.

6. In the box that appears, click **Disable**.


**Related operations**

Disabling log analysis will not automatically delete the associated TLS topic. To avoid continued log\-related charges, delete the topics in the TLS console first.

When you proceed to disable log analysis on the Logging page, a box will appear with the project and topic IDs corresponding to the bucket. You can use these IDs to locate and delete the topic associated with the bucket. For instructions, see [Delete a topic](https://docs.byteplus.com/en/docs/tls/Managing_topics?lang=en#delete-a-topic) and [Delete project](https://docs.byteplus.com/en/docs/tls/Managing_projects#delete-a-project).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since all buckets in the same region share one topic, deleting a bucket's topic will also delete the historical log records of other buckets in that region. For more information, see <a href="https://docs.byteplus.com/docs/tos/Why-cant-the-logging-function-be-used">Why does deleting a bucket's topic cause other buckets' log functions to stop working?</a>.</div>


<span id=".6K6-572u5pel5b-X5L-d5a2Y5pe26Ze0"></span>
## Setting the log retention period

For billing details, see [Billing notes](https://docs.byteplus.com/docs/tos/Log-analysis#7182c390). Follow the steps below to configure the log retention period.


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, click **Logging**. Then, on the **Log analysis** tab, click **Set log retention time**.

6. In the box that appears, specify the days and click **Set**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The data retention period can be set anywhere from one day to 3,650 days.   </div>
   

<span id="70066aec"></span>
## **Walkthrough**

You can use logs to track the daily changes in the size of both the latest and historical versions of objects, as well as total data size within a bucket.


1. Configure key\-value indexes for DeltaDataSize and HistoricalVersionDeltaSize, and set the **Field type** to **long**. For instructions, see [Configure indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Index configurations only apply to newly written logs. Therefore, query results will only include logs written after the configuration and will not include logs that existed before the configuration.   </div>
   

2. Log in to the [TOS console](https://console.byteplus.com/tos).

3. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to configure.

4. In the left navigation pane, click **Logging**. Then, click the **Search Analysis** tab and set the time range to **Last 1 day**.

5. Query the changes in storage usage of the bucket within one day.

   * **Changes in total data size**

      On the **Search Analysis** tab, enter the following query: `Bucket: <bucket name> AND NOT Operation: "BatchDeleteDetails" | SELECT SUM(DeltaDataSize)`. Then, click **Search**. The **Chart analysis** tab will then display changes in the total storage space occupied by all objects within the bucket over the last day.

   * **Changes in size of historical object versions**

      On the **Search Analysis** tab, enter the following query: `Bucket: <bucket name> | SELECT SUM(HistoricalVersionDeltaSize)`. Then, click **Search**. The **Chart analysis** tab will then display the changes in storage space occupied by historical object versions over the last day.

   * **Changes in size of latest object versions**

      You can calculate the changes in storage space occupied by latest object versions using the following formula:

      Changes in size of latest object versions = Changes in total data size \- Changes in size of historical object versions
