---
title: "ListCozeloopWorkspaces"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ListCozeloopWorkspaces"
---

Obtains the list of workspaces accessible to the current account under CozeLoop.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=ListCozeloopWorkspaces&Version=2024\-07\-30


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListCozeloopWorkspaces |The API name. The current API name is `ListCozeloopWorkspaces`. |
|Version |String |Yes |2024\-07\-30 |The API version. The current API version is `2024-07-30`. |
|CozeToken |String |Yes |pat_xxx |Authorization token for accessing CozeLoop. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=ListCozeloopWorkspaces&Version=2024-07-30
{
    "CozeToken": "pat_xxx"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [EvaluationWorkspace](https://docs.byteplus.com/en/docs/299/115800#evaluationworkspace) |[{"Id":"ws\-12345","Name":"Default Workspace"}] |CozeLoop workspace list. |


<span id="evaluationworkspace"></span>
### EvaluationWorkspace


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |ws\-12345 |Workspace ID. |
|Name |String |Default Workspace |Workspace name. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "Items": [
            {
                "Id": "ws-12345",
                "Name": "Default Workspace"
            }
        ]
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListCozeloopWorkspaces",
        "Version": "2024-07-30",
        "Service": "apmplus_server",
        "Region": "cn-north-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the API call returns an exception, you can troubleshoot by referring to the API error codes and the [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) below.


|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|500 |ErrInternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
