---
title: "CancelPipelineRun"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CancelPipelineRun"
---

Cancel the running pipeline

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CancelPipelineRun&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CancelPipelineRun |The API name. The name of the current API is `CancelPipelineRun`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |60cb460122422352a334\*\*\*\* |The workspace ID. |
|PipelineId |String |Yes |c3afa3f27d754ac8b6052bf3dc0b\*\*\*\* |Pipeline ID. |
|Id |String |Yes |c9020f1a904c41e4bc25afc96316\*\*\*\* |Pipeline run ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CancelPipelineRun&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "60cb460122422352a334****",
    "PipelineId": "c3afa3f27d754ac8b6052bf3dc0b****",
    "Id": "c9020f1a904c41e4bc25afc96316****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have any unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "CancelPipelineRun",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have independent error codes. If an exception occurs when calling the API, you can refer to [common error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
