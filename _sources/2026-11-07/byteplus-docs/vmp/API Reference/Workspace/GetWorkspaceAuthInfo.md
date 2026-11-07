---
title: "GetWorkspaceAuthInfo"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/GetWorkspaceAuthInfo"
---

Obtain workspace authentication information.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=GetWorkspaceAuthInfo&Version=2021\-03\-03


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetWorkspaceAuthInfo&serviceCode=vmp&version=2021-03-03&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetWorkspaceAuthInfo |The name of the API. The current API name is `GetWorkspaceAuthInfo`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Id |String |Yes |0d80054b\-f0f5\-4289\-ad4a\-ea5f6f9d\*\*\*\* |The workspace ID. You can obtain the workspace ID by calling the [GetWorkspaceAuthInfo](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces) API. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=GetWorkspaceAuthInfo&Version=2021-03-03
Content-Type: application/json
{
    "Id": "0d80054b-f0f5-4289-ad4a-ea5f6f9d****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AuthType |String |BasicAuth |The workspace authentication type. Valid values:<br><br><br>* **BasicAuth**: basic authentication<br><br>* **BearerToken**: token authentication<br><br>* **None**: Custom authentication is not configured. In this case, BytePlus AK/SK authentication is used by default. |
|Username |String |admin |BasicAuth username of the workspace. |
|BearerToken |String |Bearer 123456\*\*\*\* |The token used for workspace BearerToken authentication. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetWorkspaceAuthInfo",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "AuthType": "BasicAuth",
        "Username": "admin",
        "BearerToken": "Bearer 123456****"    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no exclusive error codes. For public error codes, see [Public error code](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).
