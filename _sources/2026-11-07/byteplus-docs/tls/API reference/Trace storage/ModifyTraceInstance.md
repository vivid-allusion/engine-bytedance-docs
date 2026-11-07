---
title: "ModifyTraceInstance"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ModifyTraceInstance"
---

Call the ModifyTraceInstance API to update Trace instance information.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: PUT

* Request URL: https://{tls\-endpoint}/ModifyTraceInstance


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists unique request parameters for this API and several common parameters. For more details, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TraceInstanceId |String |Yes |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID. |
|Description |String |No |This is a test trace ins. |Description of the trace instance Characters `<>`, `'`, `\`, and `\\` are not supported. The length must be between 0 and 64 characters. |
|BackendConfig |Object of [BackendConfig](https://docs.byteplus.com/en/docs/38/83197#backendconfig) |No |{"Ttl":97,"EnableHotTtl":true,"HotTtl":7,"ColdTtl":30,"ArchiveTtl":60,"AutoSplit":true,"MaxSplitPartitions":10} |Backend configuration for Trace instances, used to set log storage tiering strategy, auto split, and more. |


<span id="backendconfig"></span>
### BackendConfig


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Ttl |Integer |No |97 |The total time logs are retained in TLS. Expired logs in the topic will be automatically deleted after the specified log storage period. The unit is days. The default value is 30 days. The value ranges from 1 to 3650. If it is set to 3650, the storage time becomes permanent storage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you set <code>EnableHotTtl</code> to true, the Ttl duration must be the same as the total value of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|EnableHotTtl |Boolean |No |true |Enable tiered storage. When enabled, TLS supports standard, infrequent, and archive storage.<br><br>After setting HotTtl, ArchiveTtl, and ColdTtl, if data is stored beyond the specified duration, it is automatically moved to infrequent or archive storage for preservation, until the total log storage period reaches Ttl and is then deleted by backend services.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Ttl duration must equal the total of HotTtl, ColdTtl, and ArchiveTtl.</div><br> |
|HotTtl |Integer |No |7 |Standard storage duration The default duration is 30 days, with a range of 7–3650 days<br><br>This parameter takes effect only when EnableHotTtl is set to true |
|ColdTtl |Integer |No |30 |Low\-frequency storage duration. The range for this duration is 30–3650.<br><br>Low\-frequency storage is available for standard storage durations of 7 days or longer.<br><br>This parameter only applies when EnableHotTtl is set to true. |
|ArchiveTtl |Integer |No |60 |Archive storage duration. The valid range is 60–3650.<br><br>Archive storage is available when any of the following conditions are met.<br><br><br>* Standard storage period of 30 days or longer.<br><br>* Standard storage period of 7 days or longer and IAS storage period of 30 days or longer.<br><br><br>This parameter takes effect only when EnableHotTtl is set to true. |
|AutoSplit |Boolean |No |true |Automatic sharding can be enabled or disabled.<br><br>When enabled, if the amount of data written exceeds the capacity of an existing shard for five consecutive minutes, TLS automatically splits shards based on data volume to meet business needs. However, the number of shards cannot exceed the maximum split limit. New shard created within the last 15 minutes will not split automatically.<br><br><br>* true: enabled.<br><br>* false: disabled. |
|MaxSplitPartitions |Integer |No |`10` |Maximum number of shard splits |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

This API does not have specific return parameters. For more information, see [return structure](https://docs.byteplus.com/en/docs/tls/response-message).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
PUT https://{tls-endpoint}/ModifyTraceInstance HTTP/1.1
Content-Type: application/json
{
    "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****",
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
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more details about error codes.
