---
title: "CreateTraceInstance"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CreateTraceInstance"
---

Call the CreateTraceInstance API to create a Trace instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: POST

* Request URL: https://{tls\-endpoint}/CreateTraceInstance


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API, along with some common parameters. For more details, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TraceInstanceName |String |Yes |`test-trace` |Trace instance name.<br><br>Instance names must be unique and can only contain lowercase letters, numbers, Chinese characters, and hyphens (\-). Must start and end with a lowercase letter, Chinese character, or number, and contain 3 to 30 characters. |
|ProjectId |String |Yes |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |Trace instance's project ID. |
|Description |String |No |This is a test trace ins. |Description of the trace instance The characters `<>`, `'`, `\`, and `\\` are not supported. Length must be between 0 and 64 characters. |
|BackendConfig |Object of [BackendConfig](https://docs.byteplus.com/en/docs/38/83196#backendconfig) |No |{"Ttl":97,"EnableHotTtl":true,"HotTtl":7,"ColdTtl":30,"ArchiveTtl":60,"AutoSplit":true,"MaxSplitPartitions":10} |Backend configuration for Trace instances, used to set up log storage tiering strategies, auto split features, and more. |


<span id="backendconfig"></span>
### BackendConfig


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Ttl |Integer |No |97 |Total retention period of logs in TLS. When the specified Log storage period is exceeded, expired logs in this log topic are automatically deleted. The unit is days. The default value is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After you set <code>EnableHotTtl</code> to true, the Ttl duration must match the combined value of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|EnableHotTtl |Boolean |No |true |Enable tiered storage. After enabling, TLS supports standard, infrequent access, and archive storage.<br><br>When you set HotTtl, ArchiveTtl, or ColdTtl, data that exceeds the specified duration automatically moves to infrequent access or archive storage for continued retention until the total time on the server reaches Ttl, at which point the backend clears the logs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must match the sum of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|HotTtl |Integer |No |7 |Standard storage duration. The default duration is 30 days, with a range from 7 to 3650 days.<br><br>This parameter only takes effect when EnableHotTtl is set to true. |
|ColdTtl |Integer |No |30 |Infrequent access storage duration. This duration can be set between 30 and 3650.<br><br>Standard storage for seven days or longer enables infrequent access storage.<br><br>This parameter only takes effect when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |No |60 |Archive storage duration. The duration must be between 60 and 3650.<br><br>Archive storage can be enabled when any of the following conditions is met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter is only valid when EnableHotTtl is set to true. |
|AutoSplit |Boolean |No |true |Automatic sharding can be enabled or disabled.<br><br>When enabled, if the data volume continuously exceeds the capacity of existing shards for 5 minutes, TLS will automatically split shards based on the data volume to meet business needs. However, the number of shards after splitting cannot exceed the maximum split limit. New shard created within the last 15 minutes will not split automatically.<br><br><br>* true: Enable.<br><br>* false: Disable. |
|MaxSplitPartitions |Integer |No |`10` |Maximum number of shard splits. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The table below lists only the parameters specific to this API. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TraceInstanceId |String |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://{tls-endpoint}/CreateTraceInstance HTTP/1.1
Content-Type: application/json
{
    "TraceInstanceName": "test-trace",
    "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****",
    "Description": "This is a test trace ins.",
    "BackendConfig": {
        "Ttl": 97,
        "EnableHotTtl": true,
        "HotTtl": 7,
        "ColdTtl": 30,
        "ArchiveTtl": 60,
        "AutoSplit": true,
        "MaxSplitPartitions": 10
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Example response

```JSON
Content-Type: application/json; charset=utf-8
{
    "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Public Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more error code information.
