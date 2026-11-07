---
title: "DescribeTopic"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describetopic"
---

Call the DescribeTopic API to obtain basic information about the log topic.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

The call frequency limit for this API is 20 times per second. If the frequency limit is exceeded, an ExceedQPSLimit error will be returned.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeTopic


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TopicId |String |Yes |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |Log topic ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table lists only the unique response parameters for this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TopicName |String |`test-project` |Name of the log topic. |
|ProjectId |String |`f**********` |ID of the project to which the log topic belongs. |
|TopicId |String |`faf**********` |Log topic ID. |
|Ttl |Integer |`3650` |Total retention period of logs in TLS. After the specified Log storage period, expired logs in this log topic will be automatically deleted. Unit: days. Default is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After <code>EnableHotTtl</code> is set to true, the Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|CreateTime |String |`2021-08-19 11:41:29` |Log topic creation time. |
|ModifyTime |String |`2021-08-19 11:41:32` |Log topic modification time. |
|ShardCount |Integer |`2` |Number of shards in the log topic. |
|Description |String |`This is a test topic` |Description of the log topic. |
|AutoSplit |Boolean |`true` |Automatic sharding can be enabled or disabled.<br><br><br>* true: Enabled<br><br>* false: Disabled |
|MaxSplitShard |Integer |`50` |Maximum split count of shards. |
|EnableTracking |Boolean |`false` |Whether the WebTracking feature is enabled.<br><br><br>* true: Enabled<br><br>* false: Disabled |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/16750#tag) |`[{"Key":"key1", "Value":"value1"}]` |Log topic tag information.<br><br>&nbsp;<br><br>Tags are used for identifying and categorizing cloud resources. You can categorize projects and log topics by tags to facilitate resource search and aggregation. For details, see [Tag management](https://docs.byteplus.com/docs/tls/tag_overview). |
|LogPublicIP |Boolean |`false` |Whether the external IP recording feature is enabled.<br><br><br>* true: Enabled<br><br>* false: Disabled |
|EnableHotTtl |Boolean |`true` |Whether to enable tiered storage. After this feature is enabled, TLS supports standard storage, infrequent storage, and archive storage.<br><br>After configuring HotTtl, ArchiveTtl, and ColdTtl, if the data storage duration exceeds the corresponding period, the data will automatically migrate to infrequent storage or archive storage for subsequent retention, until the total duration of log collection to the server reaches Ttl, at which point the backend service will automatically clean up the data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|HotTtl |Integer |`7` |Standard storage duration. The default duration is 30 days, and the value range is 7 to 3650.<br><br>This parameter is effective only when EnableHotTtl is set to true. |
|ColdTtl |Integer |`10` |Infrequent storage duration. The value range is 1 to 3650.<br><br>Infrequent storage can be enabled when the standard storage duration is 7 days or more.<br><br>This parameter is effective only when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |`10` |Archive storage duration. The value range is 60 to 3650.<br><br>Archive storage can be enabled if any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter is effective only when EnableHotTtl is set to true. |
|BindProcessor |Object of [BindProcessor](https://docs.byteplus.com/en/docs/38/16750#bindprocessor) |\- |Information about the data processor bound to the log topic. |
|EncryptConf |Object of [EncryptConf](https://docs.byteplus.com/en/docs/38/16750#encryptconf) |\- |Data encryption configuration. |
|MeteringMode |String |`ChargeByFunction` |Billing mode of the log topic.<br><br><br>* ChargeByFunction (default): Feature\-based billing mode.<br><br>* ChargeByDataIngest: Data ingestion\-based billing mode. |


<span id="tag"></span>
### Tag


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |`owner` |Value of the tag Key. For configuration rules, refer to [Tag configuration rules](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ). |
|Value |String |`zhangsan` |The value of the tag Value. For configuration rules, see [Tag configuration rules](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ). |


<span id="bindprocessor"></span>
### BindProcessor


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ProcessorID |String |bfc2c7e4\-ce04\-4c20\-b7cf\-515604xxxx |ID of the data processor bound to the log topic. |
|ProcessorName |String |log_processor_1 |Name of the data processor. |


<span id="encryptconf"></span>
### EncryptConf


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|enable |Boolean |false |Whether data encryption is enabled.<br><br><br>* true: Yes<br><br>* false: No |
|encrypt_type |String |default |Encryption algorithm; only default is supported. |
|user_cmk_info |Object of [EncryptUserCmkConfApi](https://docs.byteplus.com/en/docs/38/16750#encryptusercmkconfapi) |{"trn": "trn:iam::123456789:role/service_role_for_tls", "region_id": "cn\-hongkong", "user_cmk_id": "fc227edb\-3682\-4577\-a3b5\-xxxxxxxxx"} |Key information. |


<span id="encryptusercmkconfapi"></span>
### EncryptUserCmkConfApi


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|trn |String |trn:iam::123456789:role/service_role_for_tls |TRN of the IAM role. |
|region_id |String |cn\-hongkong |Region ID where the primary key is located. |
|user_cmk_id |String |fc227edb\-3682\-4577\-a3b5\-XXXXXXXXX |Master key ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET https://{tls-endpoint}/DescribeTopic?TopicId=fa******** HTTP/1.1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "TopicName": "test17-2",
    "ProjectId": "c7e***********",
    "TopicId": "bc***********",
    "Ttl": 1023,
    "CreateTime": "2021-08-19 10:43:13",
    "ModifyTime": "2021-08-19 10:43:16",
    "ShardCount": 2,
    "Description": "test that this is a test s",
    "AutoSplit": true,
    "MaxSplitShard": 50,
    "EnableTracking": false,
    "LogPublicIP": false,
    "Tags": [
        {
            "Key": "key1",
            "Value": "value1"
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The following table lists the error codes related to the business logic of this API. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Notice** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|404 |TopicNotExist |topic %s does not exist. |The log topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
