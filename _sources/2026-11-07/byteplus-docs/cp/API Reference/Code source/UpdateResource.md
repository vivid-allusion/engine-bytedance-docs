---
title: "UpdateResource"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/UpdateResource"
---

Update the code source.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region of your resources. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=UpdateResource&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateResource |The API name. The name of the current API is `UpdateResource`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |000ce713ebd2487a9b4666c7ed81\*\*\*\* |Workspace ID |
|Id |String |Yes |1bfc821c23594ebbb7df1ae6b636\*\*\*\* |Code source ID. |
|Name |String |no |Gitee\-demo\-new |The code source name.<br><br><br>* Supports any character; length must be between 2 and 50 characters.<br><br>* Names must be unique within the same workspace. |
|Configuration |Object of [ResourceConfiguration](https://docs.byteplus.com/en/docs/292/73427#resourceconfiguration) |no |\- |Code source configuration information |
|Description |String |no |Description |The code source description |


<span id="resourceconfiguration"></span>
### ResourceConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Git |Object of [GitConfiguration](https://docs.byteplus.com/en/docs/292/73427#gitconfiguration) |no |\- |Code source configuration details. |


<span id="gitconfiguration"></span>
### GitConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Url |String |Yes |https://gitee.com/\*\*\*\* |Code repository URL |
|UserToken |String |no |0f6832949f31ef77\*\*\*\* |User token |
|UserName |String |no |user |Username. |
|Password |String |no |pwd\*\*\*\* |Password. |
|CloneDepth |Long |no |0 |Code clone depth: the default value or minimum value is 0. |
|AccessKey |String |no |qAfR\*\*\*\*\*\*\*\*\*\*\*\* |The AccessKey for third\-party cloud. |
|SecretKey |String |no |Qtlc\*\*\*\*\*\*\*\*\*\*\*\* |Third\-party cloud SecretKey. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=UpdateResource&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "000ce713ebd2487a9b4666c7ed81****",
    "Id": "1bfc821c23594ebbb7df1ae6b636****",
    "Name": "Gitee-demo-new",
    "Description": "this is a test",
    "Configuration": {
        "Git": {
            "Url": "https://gitee.com/****",
            "UserToken": "0f6832949f31ef77****"
        }
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "2024040318000935E3789440C7C089****",
        "Action": "UpdateResource",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have independent error codes. If an exception occurs when calling the API, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
