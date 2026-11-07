---
title: "DescribeTraceInstances"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeTraceInstances"
---

Call the DescribeTraceInstances API to obtain a list of Trace instances.

Supports paginated queries, offset queries, and fuzzy searches by Trace instance name and TraceID.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeTraceInstances


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists unique request parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |No |1 |The page number for paginated queries, starting from `1` by default. |
|PageSize |Integer |No |20 |The page size limit specifies the number of `Trace` instances returned per page. The default value is `20` and the maximum value is `100`. |
|TraceInstanceName |String |No |test\-trace |`Trace` instance name, mutually exclusive with `TraceInstanceId`; only one parameter can be provided |
|TraceInstanceId |String |No |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |`Trace` instance `ID`, mutually exclusive with `TraceInstanceName`; only one parameter can be provided |
|ProjectId |String |No |c7e0e442\-19bf\-4fb3\-b547\-5992fb8b\*\*\*\* |ID of the log project to which the Trace instance belongs |
|ProjectName |String |No |my\-log\-project |Name of the project, used to identify which log project the `Trace` instance belongs to |
|Status |String |No |`CREATED` |Status of the Trace instance. |
|IamProjectName |String |No |my\-iam\-log\-project |Name of the IAM project, used to identify which IAM project the `Trace` instance belongs to. |
|CsAccountChannel |String |No |web |CS account channel identifier, used to distinguish different account sources or channels. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The table below lists only the unique return parameters for this API. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Total |Integer |100 |Total number of eligible `Trace` instances, used to calculate the total number of pages for pagination. |
|TraceInstances |Array of [DescribeResp](https://docs.byteplus.com/en/docs/38/83199#describeresp) |\- |Returns a list of `Trace` instances that meet the criteria. Each instance includes project ID, creation time, modification time, description, and project name. |


<span id="describeresp"></span>
### DescribeResp


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ProjectId |String |c7e0e442\-19bf\-4fb3\-b547\-5992fb8b\*\*\*\* |The project ID that the Trace instance belongs to. |
|CreateTime |String |2023\-01\-15T10:30:00Z |Creation time of the `Trace` instance, representing when the instance was created in the system |
|ModifyTime |String |2023\-01\-15T14:45:00Z |`Trace` instance last modified time, indicating the latest update time in the system for this instance. |
|Description |String |This is a test trace ins. |Description of the trace instance |
|ProjectName |String |my\-log\-project |The name of the log project identifies which `Trace` instance belongs to which project. |
|TraceTopicId |String |ca0c7da2\-313e\-4729\-a66f\-85f40380\*\*\*\* |Log topic ID associated with the `Trace` instance, identifying the log topic for the instance. |
|BackendConfig |Object of [BackendConfig](https://docs.byteplus.com/en/docs/38/83199#backendconfig) |{"Ttl":97,"EnableHotTtl":true,"HotTtl":7,"ColdTtl":30,"ArchiveTtl":60,"AutoSplit":true,"MaxSplitPartitions":10} |Trace instance backend configuration for setting log storage tiering strategies, auto split, and more |
|TraceTopicName |String |my\-trace\-topic |Name of the log topic associated with `Trace` instances, used to identify the corresponding log topic for the instance. |
|TraceInstanceId |String |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID. |
|CsAccountChannel |String |cs\-channel\-1234567890ab\*\*\*\* |`The customer service account channel for the Trace instance`, which identifies the channel to which the instance belongs. |
|DependencyTopicId |String |c1c28228\-627a\-476b\-98b4\-2914225d\*\*\*\* |`The Trace` instance relies on the log topic ID, which identifies other log topics required by this instance. |
|TraceInstanceName |String |my\-trace\-instance |`Trace` instance name. |
|TraceInstanceStatus |String |CREATED |Status of `Trace` instance. |
|DependencyTopicTopicName |String |dependency\-topic\-name |The name of the log topic that `Trace` instances depend on, used to identify other log topics referenced by the instance. |


<span id="backendconfig"></span>
### BackendConfig


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Ttl |Integer |97 |The total retention period of logs in TLS. When logs in the topic exceed the specified Log storage period, expired logs will be automatically deleted. The unit is days. The default value is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After setting <code>EnableHotTtl</code> to true, the Ttl duration must equal the total value of HotTtl, ColdTtl, and ArchiveTtl</div><br> |
|EnableHotTtl |Boolean |true |Enable tiered storage Once enabled, TLS supports standard storage, infrequent access storage, and archive storage<br><br>When HotTtl, ArchiveTtl, and ColdTtl are configured, if the data storage time exceeds the set duration, the data will automatically migrate to infrequent access and archive storage for further retention. Data will be automatically deleted by the backend service when the total log collection duration reaches Ttl<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must equal the total value of HotTtl, ColdTtl, and ArchiveTtl</div><br> |
|HotTtl |Integer |7 |Standard storage duration. The default duration is 30 days, and the valid range is 7 to 3650 days.<br><br>This parameter is only effective when EnableHotTtl is set to true. |
|ColdTtl |Integer |30 |Low\-frequency storage duration. The valid range for this duration is 30 to 3650.<br><br>Low\-frequency storage can be enabled when the standard storage period is 7 days or longer.<br><br>This parameter takes effect only when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |60 |Archive storage period. The period must range from 60 to 3650.<br><br>Archive storage is available when any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter is only effective when EnableHotTtl is set to true |
|AutoSplit |Boolean |true |Automatic sharding can be enabled or disabled.<br><br>Once enabled, if data volume exceeds existing shard capacity for 5 consecutive minutes, TLS will automatically split shards based on data volume to meet business needs. The number of shards after splitting cannot exceed the maximum split count. New shard created within the last 15 minutes will not split automatically.<br><br><br>* true: enable.<br><br>* false: disable. |
|MaxSplitPartitions |Integer |`10` |Maximum number of shard splits |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeTraceInstances?&PageNumber=1&PageSize=20&TraceInstanceName=test-trace&TraceInstanceId=0fdaa6b6-3c9f-424c-8664-fc0d222c****&ProjectId=c7e0e442-19bf-4fb3-b547-5992fb8b****&ProjectName=my-log-project&Status=CREATED&IamProjectName=my-iam-log-project&CsAccountChannel=web HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "Total": 100,
    "TraceInstances": [
        {
            "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****",
            "CreateTime": "2023-01-15T10:30:00Z",
            "ModifyTime": "2023-01-15T14:45:00Z",
            "Description": "This is a test trace ins.",
            "ProjectName": "my-log-project",
            "TraceTopicId": "ca0c7da2-313e-4729-a66f-85f40380****",
            "BackendConfig": {
                "Ttl": 97,
                "EnableHotTtl": true,
                "HotTtl": 7,
                "ColdTtl": 30,
                "ArchiveTtl": 60,
                "AutoSplit": true,
                "MaxSplitPartitions": 10
            },
            "TraceTopicName": "my-trace-topic",
            "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****",
            "CsAccountChannel": "cs-channel-1234567890ab****",
            "DependencyTopicId": "c1c28228-627a-476b-98b4-2914225d****",
            "TraceInstanceName": "my-trace-instance",
            "TraceInstanceStatus": "CREATED",
            "DependencyTopicTopicName": "dependency-topic-name"
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more information.
