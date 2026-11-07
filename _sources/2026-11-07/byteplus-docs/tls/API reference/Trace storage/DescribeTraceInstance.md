---
title: "DescribeTraceInstance"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeTraceInstance"
---

Call the DescribeTraceInstance API to get Trace instance information.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeTraceInstance


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TraceInstanceId |String |Yes |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters unique to this API. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|BackendConfig |Object of [BackendConfig](https://docs.byteplus.com/en/docs/38/83200#backendconfig) |/ |The backend configuration of the Trace instance, which sets the log storage tiering strategy, auto split, and other features. |
|CreateTime |String |2023\-01\-15T10:30:00Z |The creation time of the `Trace` instance, which indicates when the instance was created in the system. |
|CsAccountChannel |String |cs\-channel\-1234567890ab\*\*\*\* |`The customer service account channel for the Trace instance, used to identify the channel to which the instance belongs.` |
|DependencyTopicId |String |c1c28228\-627a\-476b\-98b4\-2914225d\*\*\*\* |ID of the log topic that the `Trace` instance depends on, used to identify other log topics it relies on. |
|DependencyTopicTopicName |String |dependency\-topic\-name |The log topic name that the `Trace` instance depends on, used to identify other log topics this instance relies on. |
|Description |String |This is a test trace ins. |Description of the trace instance |
|ModifyTime |String |2023\-01\-15T14:45:00Z |Last modification time of the `Trace` instance, indicating the most recent update in the system for this instance. |
|ProjectId |String |c7e0e442\-19bf\-4fb3\-b547\-5992fb8b\*\*\*\* |The project ID of the log project to which the Trace instance belongs. |
|ProjectName |String |my\-log\-project |The name of the project is used to identify which project the `Trace` instance belongs to. |
|TraceInstanceId |String |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID. |
|TraceInstanceName |String |my\-trace\-instance |`Name of the Trace` instance. |
|TraceInstanceStatus |String |CREATED |Status of the `Trace` instance. |
|TraceTopicId |String |ca0c7da2\-313e\-4729\-a66f\-85f40380\*\*\*\* |The log topic ID associated with the `Trace` instance, which identifies the corresponding log topic for this instance. |
|TraceTopicName |String |my\-trace\-topic |`The name of the log topic associated with the Trace instance, used to identify the corresponding log topic.` |


<span id="backendconfig"></span>
### BackendConfig


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Ttl |Integer |97 |Total retention period of logs in TLS. When logs in this log topic have exceeded the specified log storage period, expired logs will be automatically cleared. The unit is days. The default value is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After setting <code>EnableHotTtl</code> to true, the value of Ttl must be the same as the combined values of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|EnableHotTtl |Boolean |true |Enable tiered storage. When enabled, TLS supports standard storage, infrequent access storage, and archive storage.<br><br>After setting HotTtl, ArchiveTtl, and ColdTtl, if data storage exceeds the specified duration, the data automatically transitions to infrequent access storage or archive storage for continued retention, until the total server\-side data retention reaches the Ttl period, at which point the backend service automatically deletes it.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl period must equal the total of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|HotTtl |Integer |7 |Standard storage duration. The default duration is 30 days, and the value can range from 7 to 3650.<br><br>This parameter takes effect only when EnableHotTtl is set to true. |
|ColdTtl |Integer |30 |Low\-frequency storage duration. The valid duration range is 30 to 3650.<br><br>Low\-frequency storage is available when the standard storage period is 7 days or longer.<br><br>This parameter is valid only when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |60 |Archive storage period. The valid range for this period is 60–3650.<br><br>Archive storage is available when any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter is only effective when EnableHotTtl is set to true. |
|AutoSplit |Boolean |true |Automatic sharding can be enabled or disabled.<br><br>After enabled, if the amount of written data exceeds the existing shard service capacity for 5 consecutive minutes, TLS automatically splits shards based on data volume to meet business needs. However, the number of shards after splitting cannot exceed the maximum split count. New shard created within the last 15 minutes will not split automatically.<br><br><br>* true: enabled.<br><br>* false: disabled. |
|MaxSplitPartitions |Integer |`10` |Maximum number of shard splits. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeTraceInstance?&TraceInstanceId=0fdaa6b6-3c9f-424c-8664-fc0d222c**** HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "BackendConfig": {
        "Ttl": 97,
        "EnableHotTtl": true,
        "HotTtl": 7,
        "ColdTtl": 30,
        "ArchiveTtl": 60,
        "AutoSplit": true,
        "MaxSplitPartitions": 10
    },
    "CreateTime": "2023-01-15T10:30:00Z",
    "CsAccountChannel": "cs-channel-1234567890ab****",
    "DependencyTopicId": "c1c28228-627a-476b-98b4-2914225d****",
    "DependencyTopicTopicName": "dependency-topic-name",
    "Description": "This is a test trace ins.",
    "ModifyTime": "2023-01-15T14:45:00Z",
    "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****",
    "ProjectName": "my-log-project",
    "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****",
    "TraceInstanceName": "my-trace-instance",
    "TraceInstanceStatus": "CREATED",
    "TraceTopicId": "ca0c7da2-313e-4729-a66f-85f40380****",
    "TraceTopicName": "my-trace-topic"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Public Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more details on error codes.
