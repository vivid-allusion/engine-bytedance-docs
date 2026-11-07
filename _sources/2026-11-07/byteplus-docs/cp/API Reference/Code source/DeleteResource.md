---
title: "DeleteResource"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/DeleteResource"
---

Delete the code source.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the service address that corresponds to the region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=DeleteResource&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteResource |The API name. The name of the current API is `DeleteResource`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current API version is `2023-05-01`. |
|WorkspaceId |String |Yes |000ce713ebd2487a9b4666c7ed81\*\*\*\* |Workspace ID. |
|Id |String |Yes |1bfc821c23594ebbb7df1ae6b636\*\*\*\* |Code source ID |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=DeleteResource&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "000ce713ebd2487a9b4666c7ed81****",
    "Id": "1bfc821c23594ebbb7df1ae6b636****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have any unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "DeleteResource",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have independent error codes. If the API returns an error, refer to [common error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
