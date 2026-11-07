---
title: "GetTaskRunLog"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/GetTaskRunLog"
---

Obtain task run logs.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the appropriate service address based on the region where your resources are located. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=GetTaskRunLog&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetTaskRunLog |The API name. The name of the current API is `GetTaskRunLog`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7815d4783edc47c5bbd7df024ab9\*\*\*\* |Workspace ID. |
|PipelineId |String |Yes |1b91935cdd9c49cdacd0cba229b1\*\*\*\* |Pipeline ID. |
|PipelineRunId |String |Yes |9c7219420b004cccb337224fa57\*\*\*\* |Pipeline run ID. |
|TaskId |String |Yes |94f98a65d0854daab1da06c473d5\*\*\*\* |Task ID. |
|TaskRunId |String |Yes |68a359ebddac482599cdf23e90ba\*\*\*\* |Task run ID. |
|StepName |String |Yes |exec\-cmd |Step name. |
|Offset |Long |no |0 |Initial position for log reading. The default is 0, which means starting from the beginning. |
|Limit |Long |no |100 |Maximum offset for log reading, in bytes. The default value is 20,000 bytes; if the value exceeds 256 KB, 256 KB will be used. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=GetTaskRunLog&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7815d4783edc47c5bbd7df024ab9****",
    "PipelineId": "1b91935cdd9c49cdacd0cba229b1****",
    "PipelineRunId": "9c7219420b004cccb337224fa57****",
    "TaskRunId": "68a359ebddac482599cdf23e90ba****",
    "TaskId": "94f98a65d0854daab1da06c473d5****",
    "StepName": "exec-cmd",
    "Limit": 100,
    "Offset": 0
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|LogLines |Array of String |["hello worldxxxx\n"] |Contents of the logs. |
|NextOffset |Long |41 |Initial position for next log read. |
|NextLimit |Long |0 |The offset for the next log read. |
|More |Boolean |false |Are there more logs? |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20240129211401F21234D64B780E8E****",
        "Action": "GetTaskRunLog",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "LogLines": [
            "hello worldxxxx",
            "\n",
            "\n",
            "--- End of CP Log ---",
            "\n"
        ],
        "NextOffset": 41,
        "NextLimit": 0,
        "More": false
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not provide dedicated error codes. If an error occurs during API calls, please refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
