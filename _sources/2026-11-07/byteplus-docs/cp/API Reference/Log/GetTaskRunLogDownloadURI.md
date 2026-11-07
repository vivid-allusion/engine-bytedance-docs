---
title: "GetTaskRunLogDownloadURI"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/GetTaskRunLogDownloadURI"
---

Get the download link for task run logs

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, select the service address for the Region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=GetTaskRunLogDownloadURI&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetTaskRunLogDownloadURI |The API name. The name of the current API is `GetTaskRunLogDownloadURI`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7815d4783edc47c5bbd7df024ab9\*\*\*\* |The workspace ID. |
|PipelineId |String |Yes |1b91935cdd9c49cdacd0cba229b1\*\*\*\* |Pipeline ID. |
|PipelineRunId |String |Yes |9c7219420b004cccb337224fa57\*\*\*\* |Pipeline run ID |
|TaskId |String |Yes |94f98a65d0854daab1da06c473d5\*\*\*\* |Task ID. |
|TaskRunId |String |Yes |68a359ebddac482599cdf23e90ba\*\*\*\* |Task run ID. |
|StepName |String |Yes |exec\-cmd |The step name. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=GetTaskRunLogDownloadURI&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7815d4783edc47c5bbd7df024ab9****",
    "PipelineId": "1b91935cdd9c49cdacd0cba229b1****",
    "PipelineRunId": "9c7219420b004cccb337224fa57****",
    "TaskRunId": "68a359ebddac482599cdf23e90ba****",
    "TaskId": "94f98a65d0854daab1da06c473d5****",
    "StepName": "exec-cmd"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Url |String |https://cp\-v2.tos\-ap\-southeast\-1.volces.com/v2/log/7815d4783edc47\*\*\*\* |Log download link. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202401292131402BA77414F8F67D9E****",
        "Action": "GetTaskRunLogDownloadURI",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Url": "https://cp-v2.tos-ap-southeast-1.volces.com/v2/log/7815d4783edc47****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have dedicated error codes. If an exception occurs when calling the API, you can refer to [the public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
