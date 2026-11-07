---
title: "ModifyTopic"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifytopic"
---

Call the ModifyTopic API to modify log topic information.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API is used to modify the log topic name, log retention period, and topic description. Modification of the log topic ID is not supported. The call frequency limit is 20 times per second. If the limit is exceeded, the error ExceedQPSLimit will be returned.

<span id=".6K-35rGC6K-05piO"></span>
## Request notes


* Request method: PUT

* Request URL: https://{tls\-endpoint}/ModifyTopic


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TopicId |String |Yes |`0***********` |Log topic ID. |
|TopicName |String |NOT |`test-topic` |Name of the log topic. For naming rules, see [Resource naming rules](https://docs.byteplus.com/en/docs/tls/Limits#2c1ff6c3). |
|Ttl |Integer |NOT |`1300` |The total retention period of logs in TLS. After the specified Log storage period is exceeded, expired logs in this topic will be automatically deleted. The unit is days, with a default of 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If <code>EnableHotTtl</code> is set to true, the Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|AutoSplit |Boolean |NOT |`true` |Automatic sharding can be enabled or disabled.<br><br><br>* True: If the amount of data written exceeds the existing shard capacity for 5 consecutive minutes, TLS will automatically split shards based on data volume to meet business needs. However, the number of shards after splitting can not exceed the maximum split count. New shards split within the last 15 minutes will not be auto split.<br><br>* false: Auto split for shards is not enabled. |
|MaxSplitShard |Integer |NOT |`50` |The maximum number of shard splits, that is, the maximum number of shards after splitting. The value range is 1 to 256, and the default value is 256.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required only when <strong>Automatic sharding</strong> is enabled, that is, when AutoSplit is set to true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">MaxSplitShard must be greater than the current number of shards; otherwise, TLS cannot auto split shards.</div><br> |
|EnableTracking |Boolean |NOT |`false` |WebTracking can be enabled or disabled. If enabled, you can quickly collect frontend tracking data through it.<br><br><br>* true: WebTracking feature is enabled.<br><br>* false: WebTracking feature is disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After enabling WebTracking for a log topic, data written through the WebTracks API no longer needs authentication. This grants anonymous write access over the public network, but it may result in dirty data. For details, see <a href="https://docs.byteplus.com/en/docs/tls/Use_web_tracking_to_collect_logs">Collect logs via WebTracking</a>.</div><br> |
|Description |String |NOT |`This is a test topic.` |Log topic description.<br><br><br>* Does not support `<>`, `'`, `\`, `\\`, or any emoji characters.<br><br>* Length: 0–64 characters. |
|LogPublicIP |Boolean |NOT |`false` |Record extranet IP, can be enabled or disabled. By default, it is enabled. After enabling, TLS automatically adds the following metadata fields to the log content.<br><br><br>* `__tag____client_ip__`: the public IP address of the device where the log originates. When log data is written using the TLS private domain name, the private IP address is recorded.<br><br>* `__tag____receive_time__`: the time the log reaches the server, formatted as a 10\-digit Unix timestamp. |
|EnableHotTtl |Boolean |NOT |`false` |Whether to enable tiered storage. Once enabled, TLS supports standard storage, infrequent access storage, and archive storage.<br><br>When HotTtl, ArchiveTtl, and ColdTtl are set, if the data retention period exceeds the corresponding duration, the data will automatically migrate to infrequent access storage or archive storage for subsequent retention, until the total time the log has been stored on the server reaches Ttl, at which point it will be automatically deleted by the backend service.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|HotTtl |Integer |NOT |`30` |Standard storage duration. The default duration is 30 days, and the value range is 7–3650.<br><br>This parameter is only effective when EnableHotTtl is set to true. |
|ColdTtl |Integer |NOT |`30` |Cold storage retention period. The value range is 1–3650.<br><br>Standard storage retention of 7 days or more enables cold storage.<br><br>This parameter takes effect only when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |NOT |`60` |Archive storage duration. The value range for this duration is 60 to 3650.<br><br>Archive storage can be enabled when any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter takes effect only when EnableHotTtl is set to true. |
|MeteringMode |String |NOT |`ChargeByFunction` |The billing mode of the log topic.<br><br><br>* ChargeByFunction (default): Function\-based billing mode.<br><br>* ChargeByDataIngest: Data ingestion\-based billing mode. |
|EncryptConf |Object of [EncryptConf](https://docs.byteplus.com/en/docs/38/16749#encryptconf) |NOT |\- |Data encryption configuration. |


<span id="encryptconf"></span>
### EncryptConf


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|enable |Boolean |NOT |`false` |Whether to enable data encryption.<br><br><br>* true: Yes<br><br>* false: No |
|encrypt_type |String |NOT |`default` |Encryption algorithm. Only default is supported. |
|user_cmk_info |Object of [EncryptUserCmkConf](https://docs.byteplus.com/en/docs/38/16749#encryptusercmkconf) |NOT |`{"trn": "trn:iam::123456789:role/service_role_for_tls", "region_id": "cn-hongkong", "user_cmk_id": "fc227edb-3682-4577-a3b5-xxxxxxxxx"}` |Key information. |


<span id="encryptusercmkconf"></span>
### EncryptUserCmkConf


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|trn |String |NOT |trn:iam::123456789:role/service_role_for_tls |TRN of the IAM role. |
|region_id |String |NOT |cn\-hongkong |Region ID where the primary key is located. |
|user_cmk_id |String |NOT |fc227edb\-3682\-4577\-a3b5\-XXXXXXXXX |Primary key ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/tls/response-message).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
PUT https://{tls-endpoint}/ModifyTopic HTTP/1.1
Content-Type: application/json
{
    "TopicId": "66********",
    "TopicName": "test-topic",
    "Ttl": 30,
    "Description": "xxxxxx",
    "AutoSplit": true,
    "MaxSplitShard": 50,
    "EnableTracking": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The following table lists error codes related to this API and business logic. For common error codes, refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Notice** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|404 |TopicNotExist |topic %s does not exist. |Log topic does not exist. |
|409 |TopicAlreadyExist |Topic %s already exist |The log topic already exists. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
