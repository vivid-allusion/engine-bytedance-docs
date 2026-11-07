---
title: "RunPipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/RunPipeline"
---

Run the pipeline.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=RunPipeline&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |RunPipeline |The API name. The name of the current API is `RunPipeline`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |9d3f01e4f7ee4293a7cfc0c2d4d6 |Workspace ID. |
|Id |String |Yes |67d0485e1efb44128f0d990cdad6 |Pipeline ID. |
|Parameters |Array of [TriggerParameter](https://docs.byteplus.com/en/docs/292/73445#triggerparameter) |no |\- |The parameters that need to be provided when triggering the pipeline are currently pipeline dynamic variables.<br><br>If dynamic variables have been set in your pipeline, it is possible to configure their runtime values here. |
|Resources |Array of [TriggerResource](https://docs.byteplus.com/en/docs/292/73445#triggerresource) |no |\- |When triggering a pipeline, you need to provide a resource configuration, which currently refers to the code source configuration. |
|Description |String |no |This is a description. |Operation description. |


<span id="triggerparameter"></span>
### TriggerParameter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key |The dynamic variable key. |
|Value |String |Yes |value |Dynamic variable Value |


<span id="triggerresource"></span>
### TriggerResource


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ResourceId |String |Yes |60cb460122422352a334\*\*\*\* |Code source ID. |
|Reference |String |Yes |master |The code reference used for pipeline execution supports entering a Commit ID, Tag, or Branch. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=RunPipeline&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "9d3f01e4f7ee4293a7cfc0c2d4d6****",
    "Id": "67d0485e1efb44128f0d990cdad6****",
    "Description": "test",
    "Parameters": [
        {
            "key": "key1",
            "value": "value1"
        },
        {
            "key": "key2",
            "value": "value2"
        }
    ],
    "Resources": [
        {
            "ResourceId": "60cb460122422352a334****",
            "Reference": "master"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |0485ca86130647f0b5bbd5b0090a\*\*\*\* |Pipeline run ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "RunPipeline",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "0485ca86130647f0b5bbd5b0090a****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface currently does not have independent error codes. If an exception occurs when calling the interface, you can refer to [public error code](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
