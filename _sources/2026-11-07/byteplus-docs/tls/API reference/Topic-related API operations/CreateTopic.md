---
title: "CreateTopic"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-createtopic"
---

Call the CreateTopic API to create a log topic.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Before creating a log topic, ensure that a project has been created. For more details, see [CreateProject](https://docs.byteplus.com/docs/tls/api-createproject).

* This API has a rate limit of 20 requests per second. If the rate limit is exceeded, an ExceedQPSLimit error will be returned.


<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: https://{tls\-endpoint}/CreateTopic


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TopicName |String |Yes |`test-topic` |Name of the log topic. For naming rules, see [Resource naming rules](https://docs.byteplus.com/en/docs/tls/Limits#2c1ff6c3). |
|ProjectId |String |Yes |`c7***********` |The project ID to which the log topic belongs. |
|Ttl |Integer |Yes |`1300` |Total retention period of logs in TLS. When the Log storage period is exceeded, expired logs in this log topic will be automatically deleted. The unit is days, and the default is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After setting <code>EnableHotTtl</code> to true, the Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|ShardCount |Integer |Yes |`2` |The number of shards for the log topic. By default, 1 shard is created. The value range is 1–10. Each shard provides a write capacity of 5 MiB/s and 500 times/s, and a read capacity of 20 MiB/s and 100 times/s. Plan your shards appropriately when creating a log topic. After creation, the number of shards can not be changed. |
|AutoSplit |Boolean |NOT |`true` |Automatic sharding can be enabled or disabled.<br><br><br>* True: If the amount of data written exceeds the existing shard capacity for 5 consecutive minutes, TLS will automatically split shards based on data volume to meet business needs. However, the number of shards after splitting can not exceed the maximum split count. New shard created within the last 15 minutes will not split automatically.<br><br>* false: Auto split for shards is not enabled. |
|MaxSplitShard |Integer |NOT |`50` |The maximum split count of shards, that is, the maximum number of shards after splitting. The value range is 1 to 256, and the default value is 256.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required only when <strong>Automatic sharding</strong> is enabled, that is, when AutoSplit is true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">MaxSplitShard must be greater than the specified ShardCount; otherwise, TLS cannot auto split shards.</div><br> |
|EnableTracking |Boolean |NOT |`false` |WebTracking can be enabled or disabled. If enabled, you can quickly collect frontend tracking data through it.<br><br><br>* true: Enable the WebTracking feature.<br><br>* false: (default) Disable the WebTracking feature.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After enabling WebTracking for a log topic, data written through the WebTracks API no longer needs authentication. This grants anonymous write access over the public network, but it may result in dirty data. For details, see <a href="https://docs.byteplus.com/en/docs/tls/Use_web_tracking_to_collect_logs">Collect logs using WebTracking</a>.</div><br> |
|Description |String |NOT |`This is a test topic.` |Description of the log topic.<br><br><br>* `<>`, `'`, `\`, `\`, and all emoji characters are not supported.<br><br>* The length is 0–64 characters. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/16747#tag) |NOT |`[{"Key":"key1", "Value":"value1"}]` |Log topic tag information.<br><br>&nbsp;<br><br>Tags are used for identifying and categorizing cloud resources. You can categorize projects and log topics using tags, which facilitates resource search and aggregation. For more details, see [Tag management](https://docs.byteplus.com/docs/tls/tag_overview). |
|LogPublicIP |Boolean |NOT |`false` |Record extranet IP, can be enabled or disabled. By default, it is enabled. Once enabled, TLS automatically adds the following metadata fields to the log content.<br><br><br>* `__tag____client_ip__`: the public IP address of the device where the log originates. When writing log data using the TLS private domain name, the private IP address is recorded.<br><br>* `__tag____receive_time__`: the time the log reaches the server, formatted as a 10\-digit Unix timestamp.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When logs are written via WebTracking, TLS records public IP address of source device through clientAddr.</div><br> |
|EnableHotTtl |Boolean |NOT |`false` |Whether to enable tiered storage. Once enabled, TLS supports standard storage, Infrequent Access storage, and archive storage.<br><br>After setting HotTtl, ArchiveTtl, and ColdTtl, if the data storage time exceeds the corresponding duration, the data will automatically migrate to Infrequent Access storage or archive storage for subsequent retention, until the retention time on the server reaches Ttl, at which point it will be automatically cleaned by the backend service.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|HotTtl |Integer |NOT |`30` |Standard storage duration. The default duration is 30 days, and the value range is 7–3650.<br><br>This parameter takes effect only when EnableHotTtl is set to true. |
|ColdTtl |Integer |NOT |`30` |Infrequent storage duration. The valid range for this duration is 1 to 3650.<br><br>Infrequent storage can be enabled when the standard storage duration is 7 days or more.<br><br>This parameter is only effective when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |NOT |`60` |Archive storage duration. The valid range for this duration is 60 to 3650.<br><br>Archive storage can be enabled if any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter is only effective when EnableHotTtl is set to true. |
|MeteringMode |String |NOT |`ChargeByFunction` |The billing mode of the log topic.<br><br><br>* ChargeByFunction (default): Function\-based billing mode.<br><br>* ChargeByDataIngest: Data ingestion\-based billing mode. |
|EncryptConf |Object of [EncryptConf](https://docs.byteplus.com/en/docs/38/16747#encryptconf) |NOT |`-` |Data encryption configuration. |


<span id="tag"></span>
### Tag


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Key |String |NOT |`owner` |Value of the tag Key. For configuration rules, see [Tag configuration rules](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ). |
|Value |String |NOT |`zhangsan` |The value of the tag Value. For configuration rules, see [Tag configuration rules](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ). |


<span id="encryptconf"></span>
### EncryptConf


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|enable |Boolean |NOT |`false` |Whether to enable data encryption.<br><br><br>* true: Yes<br><br>* false: No |
|encrypt_type |String |NOT |`default` |Encryption algorithm. Only default is supported. |
|user_cmk_info |Object of [EncryptUserCmkConf](https://docs.byteplus.com/en/docs/38/16747#encryptusercmkconf) |NOT |`{"trn": "trn:iam::123456789:role/service_role_for_tls", "region_id": "cn-hongkong", "user_cmk_id": "fc227edb-3682-4577-a3b5-xxxxxxxxx"}` |Key information. |


<span id="encryptusercmkconf"></span>
### EncryptUserCmkConf


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|trn |String |NOT |trn:iam::123456789:role/service_role_for_tls |TRN of the IAM role. |
|region_id |String |NOT |cn\-hongkong |The region ID where the primary key is located. |
|user_cmk_id |String |NOT |fc227edb\-3682\-4577\-a3b5\-XXXXXXXXX |Primary key ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table lists only the parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TopicId |String |`b***********` |Log topic ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST https://{tls-endpoint}/CreateTopic HTTP/1.1
Content-Type: application/json
{
    "ProjectId": "c7************",
    "TopicName": "test-topic",
    "Ttl": 30,
    "Description": "xxxxxx",
    "ShardCount": 1,
    "AutoSplit": true,
    "MaxSplitShard": 50,
    "EnableTracking": false,
    "Tags": [
        {
            "Key": "key1",
            "Value": "value1"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "TopicId": "bcb************"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The following table lists the error codes related to this API and its business logic. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Notice** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|400 |TopicQuotaExceed |Topic Quota Exceed. |Log topic quota exceeded. |
|409 |TopicAlreadyExist |Topic xxx already exist. |The log topic already exists. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
