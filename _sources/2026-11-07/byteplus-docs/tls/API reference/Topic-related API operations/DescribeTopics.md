---
title: "DescribeTopics"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describetopics"
---

Call the DescribeTopics API to obtain all log topic information for the project.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API is used to view the list of log topics under the specified project. Supports paginated queries, offset\-based queries, and fuzzy queries by log topic name and ID.

The call frequency limit for this API is 20 times per second. If the frequency limit is exceeded, the error ExceedQPSLimit will be returned.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeTopics


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |NOT |`1` |Page number for paginated queries. The default is 1, which means data is returned starting from the first page. |
|PageSize |Integer |NOT |`10` |Page size for paginated queries. The default is 20, and the maximum is 100. |
|TopicName |String |NOT |`test` |Log topic name, supports fuzzy matching. |
|TopicId |String |NOT |`77` |Log topic ID, supports fuzzy matching. |
|ProjectId |String |NOT |`6622a14b-770f-4171-a385-3b68486f****` |Project ID. Fuzzy matching is supported. |
|ProjectName |String |NOT |`test-tls` |Project name. Fuzzy matching is supported. |
|Tags |String |NOT |`[{\"key\":\"key2\",\"Value\":\"value1\"}]` |Filter by log topic tags. For supported filtering methods, see [Filter resources by tag](https://docs.byteplus.com/docs/tls/Filter_resources_by_tag). |
|IsFullName |Boolean |NOT |false |Whether to perform an exact match query by full name. The default is `false`, which supports fuzzy matching. If set to `true`, only projects or log topics with exactly the same name will be matched. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table lists only the unique response parameters for this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Total |Integer |`2` |Number of log topics. |
|Topics |Array of [DescribeResp](https://docs.byteplus.com/en/docs/38/16751#describeresp) |`/` |Log topic list. |


<span id="describeresp"></span>
### DescribeResp


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Ttl |Integer |`3650` |The total retention period of logs in TLS. When the specified Log storage period is exceeded, expired logs in this log topic will be automatically deleted. The unit is days, and the default is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After setting <code>EnableHotTtl</code> to true, the Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/38/16751#tag) |`[{"Key":"key1","Value":"value1"}]` |Project tag information.<br><br>&nbsp;<br><br>Tags are used for identification and classification of cloud resources. You can categorize projects and log topics using tags, which facilitates resource search and aggregation. For detailed instructions, see [Tag management](https://docs.byteplus.com/docs/tls/tag_overview). |
|HotTtl |Integer |`30` |Standard storage period. The default period is 30 days, and the value range is 7–3650.<br><br>This parameter takes effect only when EnableHotTtl is true. |
|TopicId |String |`faf6d529-e75e-457f-a23a-9c4203a6dff3` |Log topic ID. |
|AutoSplit |Boolean |`true` |Automatic sharding can be enabled or disabled.<br><br>After this feature is enabled, when the amount of data written continuously exceeds the existing shard service capacity for 5 minutes, TLS will auto split shards based on the data volume to meet business requirements. However, the number of shards after splitting cannot exceed the maximum split limit. New shard created within the last 15 minutes will not split automatically.<br><br><br>* true: Enabled.<br><br>* false: Disabled. |
|ProjectId |String |`f**********` |Project ID to which the log topic belongs. |
|TopicName |String |`test-project` |Name of the log topic. |
|CreateTime |String |`2021-08-19 11:41:29` |Log topic creation time. |
|ModifyTime |String |`2021-08-19 11:41:32` |Log topic modification time. |
|ShardCount |Integer |`2` |Number of log topic shards. |
|Description |String |`This is a test topic` |Description of the log topic. |
|LogPublicIP |Boolean |`false` |Whether the external IP recording feature is enabled.<br><br><br>* true: Enabled.<br><br>* false: Disabled. |
|EnableHotTtl |Boolean |`true` |Whether tiered storage is enabled. When this feature is enabled, TLS supports standard storage, infrequent access storage, and archive storage.<br><br>After HotTtl, ArchiveTtl, and ColdTtl are set, if the data storage duration exceeds the corresponding period, the data will automatically migrate to infrequent access storage or archive storage for subsequent retention, until the total time since the logs were collected to the server reaches Ttl, at which point the backend service will automatically clean up the data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must be equal to the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|MaxSplitShard |Integer |`50` |The maximum number of shard splits, that is, the maximum number of all shards after splitting. |
|EnableTracking |Boolean |`false` |Indicates whether the WebTracking feature is enabled. Once enabled, you can quickly collect frontend tracking data through WebTracking.<br><br><br>* true: Enabled<br><br>* false: Disabled |
|ColdTtl |Integer |`30` |Infrequent access storage period. The value range is 1–3650.<br><br>Infrequent access storage is available when the standard storage period is 7 days or more.<br><br>This parameter takes effect only when EnableHotTtl is true. |
|ArchiveTtl |Integer |`60` |Archive storage period. The value range is 60–3650.<br><br>Archive storage is available when any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter is effective only when EnableHotTtl is set to true. |
|EncryptConf |Object of [EncryptConf](https://docs.byteplus.com/en/docs/38/16751#encryptconf) |\- |Data encryption configuration. |
|MeteringMode |String |`ChargeByFunction` |Billing mode of the log topic.<br><br><br>* ChargeByFunction (default): Function\-based billing mode.<br><br>* ChargeByDataIngest: Billing mode based on data ingestion volume. |
|BindProcessor |Object of [BindProcessor](https://docs.byteplus.com/en/docs/38/16751#bindprocessor) |\- |Information about the data processor bound to the log topic. |


<span id="tag"></span>
### Tag


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |`owner` |Value of the tag Key. For setting rules, see [Tag setting rules](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ). |
|Value |String |`zhangsan` |Value of the tag Value. For configuration rules, refer to [Tag configuration rules](https://docs.byteplus.com/docs/tls/Add_tags#.5qCH562-6K6-572u6KeE5YiZ). |


<span id="encryptconf"></span>
### EncryptConf


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|enable |Boolean |false |Whether data encryption is enabled.<br><br><br>* true: Yes<br><br>* false: No |
|encrypt_type |String |default |Encryption algorithm, only default is supported. |
|user_cmk_info |Object of [EncryptUserCmkConfApi](https://docs.byteplus.com/en/docs/38/16751#encryptusercmkconfapi) |{"trn": "trn:iam::123456789:role/service_role_for_tls", "region_id": "cn\-hongkong", "user_cmk_id": "fc227edb\-3682\-4577\-a3b5\-xxxxxxxxx"} |Key information. |


<span id="bindprocessor"></span>
### BindProcessor


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ProcessorID |String |bfc2c7e4\-ce04\-4c20\-b7cf\-515604xxxx |Data processor ID bound to the log topic. |
|ProcessorName |String |log_processor_1 |Name of the data processor. |


<span id="encryptusercmkconfapi"></span>
### EncryptUserCmkConfApi


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|trn |String |trn:iam::123456789:role/service_role_for_tls |TRN of the IAM role. |
|region_id |String |cn\-hongkong |The region ID where the primary key is located. |
|user_cmk_id |String |fc227edb\-3682\-4577\-a3b5\-XXXXXXXXX |Primary key ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET https://{tls-endpoint}/DescribeTopics?ProjectId=662***&PageNumber=1&PageSize=10&TopicName=tes&IsFullName=false&Tags=[{"Key":"key1","Value":"value1"}] HTTP/1.1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
...
{
    "Total": 2,
    "Topics": [
        {
            "TopicName": "test****",
            "ProjectId": "c7e0****",
            "ProjectName": "test****",
            "TopicId": "b80f****",
            "Ttl": 1023,
            "CreateTime": "2023-12-19 11:41:29",
            "ModifyTime": "2023-12-19 11:41:32",
            "ShardCount": 2,
            "Description": "test that this is a test s",
            "AutoSplit":true,
            "MaxSplitShard":50,
            "EnableTracking":false,
            "LogPublicIP": false,
            "Tags":[
                {
                    "Key":"key1",
                    "Value":"value1"
                }
            ]
        },
        {
            "TopicName": "test17-2",
            "ProjectId": "c7e0*********",
            "ProjectName": "test****",
            "TopicId": "bcb2*********",
            "Ttl": 1023,
            "CreateTime": "2021-08-19 10:43:13",
            "ModifyTime": "2021-08-19 10:43:16",
            "ShardCount": 2,
            "Description": "test that this is a test s",
            "AutoSplit":true,
            "MaxSplitShard":50,
            "EnableTracking":false,
            "Tags":[
                {
                    "Key":"key1",
                    "Value":"value1"
                }
            ]
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The following table lists the error codes related to business logic for this API. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Notice** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|404 |TopicNotExist |topic %s does not exist. |Log topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
