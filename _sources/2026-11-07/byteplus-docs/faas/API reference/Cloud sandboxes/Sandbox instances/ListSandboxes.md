---
title: "ListSandboxes"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListSandboxes"
---

Obtain an instance list of sandbox applications.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://open.volcengineapi.com/?Action=ListSandboxes&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSandboxes |Interface name. The name of the current API is `ListSandboxes`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |e8m6\*\*\*\* |Filter sandbox instances by the ID of the sandbox application.<br><br>Obtain the sandbox application ID on the sandbox application page. For login methods for sandbox applications, see [Sandbox Application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications?lang=en). |
|SandboxId |String |No |faas\-e8m6xarn\-p2zamuv2fr\-\*\*\*\*\* |Filter sandbox instances by sandbox instance ID or name.<br><br>Obtain the sandbox instance ID or name under the **Sandbox Instance** tab on the sandbox application page. For login methods for sandbox applications, see [Sandbox Application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications?lang=en).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When multiple query conditions are specified, the sandbox instance ID and name are prioritized to return a single instance, or to indicate that the instance does not exist.</div><br> |
|Metadata |JSON Map |No |{"app":"test"} |Filter sandbox instances using sandbox instance metadata. |
|PageNumber |Integer |No |1 |The starting page number for paginated queries. The default value is 1. |
|PageSize |Integer |No |10 |Number of records displayed per page in paginated queries. Value range: 1–100. Default value: 10. |
|ImageUrl |String |No |cr\-basic\-faas\-ap\-southeast\-1.cr.volces.com/\*\*\*\*:latest |Query the sandbox instance list by image address. |
|Status |String |No |Ready |Query the sandbox instance list by sandbox instance status. Values:<br><br><br>* Pending: waiting for scheduling.<br><br>* Starting: startup in progress.<br><br>* Ready: startup completed.<br><br>* Failed: startup failed.<br><br>* Terminating: terminating. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/192/69673#filter) |No |\- |Filter condition used to filter sandbox instances. |


<span id="filter"></span>
### Filter


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |status |Filter key (Key) for the query. Available values:<br><br><br>* revision: version of the sandbox instance.<br><br>* status: status of the sandbox instance. Available values:<br><br>   * Pending: waiting for scheduling.<br><br>   * Starting: startup in progress.<br><br>   * Ready: startup completed.<br><br>   * Failed: startup failed.<br><br>   * Terminating: terminating.<br><br>* session_id: session ID of the sandbox instance. |
|Values |Array of String |No |["Ready","Starting"] |Filter values for the query. Separate multiple values with a half\-width comma (`,`). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=ListSandboxes&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "e8m6****",
    "SandboxId": "faas-e8m6xarn-p2zamuv2fr-*****",
    "Metadata": {
        "app": "test"
    },
    "PageNumber": 1,
    "PageSize": 10,
    "ImageUrl": "cr-basic-faas-ap-southeast-1.cr.volces.com/****:latest",
    "Status": "Ready"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Sandboxes |Array of [SandboxInfo](https://docs.byteplus.com/en/docs/192/69673#sandboxinfo) |\- |Sandbox instance list. |
|Total |Integer |100 |Total number of sandbox instances. |
|StatusCount |JSON Map |{"Ready":100} |The number of sandbox instances in different statuses. |
|RevisionCount |JSON Map |{"1":50,"2":30} |Mapping of the number of sandbox instances corresponding to different version numbers. The key is the version number, and the value is the number of sandbox instances for that version. |


<span id="sandboxinfo"></span>
### SandboxInfo


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |faas\-e8m6xarn\-p2zamuv2fr\-\*\*\*\* |ID or name of the sandbox instance. |
|Image |String |\*\*\-ap\-southeast\-1.cr.volces.com/faas\-\*\*/sandbox\-fusion:\*\*.python |The image address of the sandbox instance. |
|Status |String |Ready |Sandbox instance status: Values:<br><br><br>* Starting: startup in progress.<br><br>* Ready: startup completed.<br><br>* Failed: startup failed.<br><br>* Terminating: terminating. |
|Pending |Boolean |true |Indicates whether the sandbox instance is in the pending scheduling state. When Status has not yet been updated, use this field to determine whether it is in the queue. Available values:<br><br><br>* true: In the scheduling queue.<br><br>* false: Default value, not in the scheduling queue. |
|CpuMilli |Integer |500 |The CPU specification of the sandbox instance, in millicpu. |
|ExpireAt |String |2025\-04\-25 11:31:29.376 +0000 UTC |Expiration time of the sandbox instance. |
|MemoryMB |Integer |1,024 |The specification of sandbox instance memory, in MiB. |
|Metadata |JSON Map |{"app":"test"} |Sandbox instance metadata. |
|CreatedAt |String |2025\-04\-25 11:11:29.376 +0000 UTC |Creation time of the sandbox instance. |
|ErrorCode |String |function_health_check_failed |Error code for sandbox instance start failure. Available values:<br><br><br>* internal_load_request_error: Internal system error.<br><br>* function_initialize_failed: Business process initialization error.<br><br>* function_health_check_failed: Health check error.<br><br>* route_terminating: Route is being deleted.<br><br><br>This field is empty if sandbox instances start normally. |
|SessionId |String |sess\-12345\*\*\*\* |Session ID of the sandbox instance. |
|FunctionId |String |e8m6\*\*\*\* |Sandbox application ID. |
|AssignStatus |String |ready |Assignment status of the sandbox, only applicable when the sandbox pre\-warming pool is turned on. Available values:<br><br><br>* ready: Pre\-warmed and available for assignment.<br><br>* assigned: Assigned. |
|ErrorMessage |String |function_health_check_failed |Error message for sandbox instance startup failure. This field is empty if sandbox instances start normally. |
|InstanceType |String |elastic |Sandbox instance types: Available values:<br><br><br>* elastic: elastic instance.<br><br>* frozen: frozen instance.<br><br>* activated: activated instance.<br><br>* reserved: reserved instance. |
|RevisionNumber |Integer |1 |Version number of the sandbox instance. |
|AvailabilityZone |String |ap\-southeast\-1\-b |Availability zone ID of sandbox instances. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListSandboxes",
        "Version": "2024-06-06",
        "Service": "faas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Sandboxes": [
            {
                "Id": "faas-e8m6xarn-p2zamuv2fr-****",
                "Image": "enterprise-ap-southeast-1.cr.volces.com/faas-public/sandbox-fusion:20250509.python",
                "Status": "Ready",
                "Pending": true,
                "CpuMilli": 500,
                "ExpireAt": "2025-04-25 11:31:29.376 +0000 UTC",
                "MemoryMB": 1024,
                "Metadata": {
                    "app": "test"
                },
                "CreatedAt": "2025-04-25 11:11:29.376 +0000 UTC",
                "ErrorCode": "function_health_check_failed",
                "FunctionId": "e8m6****",
                "ErrorMessage": "function_health_check_failed",
                "InstanceType": "elastic",
                "RevisionNumber": 1,
                "AvailabilityZone": "ap-southeast-1-b"
            }
        ],
        "Total": 100,
        "StatusCount": {
            "Ready": 100
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
